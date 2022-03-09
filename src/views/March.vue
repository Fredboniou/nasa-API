<template>
    <div class="display">
        <Banner title="Nasa-API"/>
        <p>Le saviez vous : 1 jour sur Mars dure 1,0274884259259 jours terrestre, soit 1 jour 39 minutes et 35,244147 secondes</p>
        <label for="rover">Choisissez un rover</label><br />
        <select v-model="choice" name="choice-rover" id="rover" @change="test()">
            <option value="">...</option>
            <option value="perseverance">Perseverance</option>
            <option value="curiosity">Curiosity</option>
            <option value="opportunity">Opportunity</option>
            <option value="spirit">Spirit</option>
        </select>
        <p v-if="choice == 'perseverance'">Premier jour de mission : 18/02/2021.<br />
        Temps de mission en sol martien : {{ numberOfDays('2021-02-18', dayDate()) }} jours</p>
        <p v-if="choice == 'curiosity'">Premier jour de mission : 06/08/2012.<br />
        Temps de mission en sol martien : {{ numberOfDays('2012-08-06', dayDate()) }} jours</p>
        <p v-if="choice == 'opportunity'">Premier jour de mission : 25/01/2004.<br />
        Dernier jour de mission officiel : 13/02/2019.<br />
        Dernier contact : 10/06/2018.<br >
        Temps de mission en sol martien : {{ numberOfDays('2004-01-25', '2019-02-13') }} jours</p>
        <p v-if="choice == 'spirit'">Premier jour de mission : 04/01/2004.<br />
        Dernier jour de mission : 22/03/2010.<br />
        Temps de mission en sol martien : {{ numberOfDays('2004-01-04', '2010-03-22') }} jours</p>

        <p v-if="choice !== ''">Choisissez une date, elle sera convertie en jours martiens</p>
        <input type="date" v-if="choice == 'perseverance'" v-model="dateChoice" name="picDate" id="picDate" min="2021-02-18" :max="dayDate()" @change="changeDate('2021-02-18', dateChoice)" />
        <input type="date" v-if="choice == 'curiosity'" v-model="dateChoice" name="picDate" id="picDate" min="2012-08-06" :max="dayDate()" @change="changeDate('2012-08-06', dateChoice)" />
        <input type="date" v-if="choice == 'opportunity'" v-model="dateChoice" name="picDate" id="picDate" min="2004-01-25" max="2018-06-10" @change="changeDate('2004-01-25', dateChoice)" />
        <input type="date" v-if="choice == 'spirit'" v-model="dateChoice" name="picDate" id="picDate" min="2004-01-04" max="2010-03-22" @change="changeDate('2004-01-04', dateChoice)" />

        <div class="noInfos" v-if="marsInfos.length == 0">
            <p>Il n'y a pas encore de données disponibles</p>
        </div>
        <div class="marsDisplay" v-for="(infos, idx) in marsInfos" :key="idx">
            <div class="seeInfos">
                <div class="marsDay" v-if="idx == 0">
                    <p>Jour de mission {{ marsInfos[idx].sol }} (en jours martiens)</p>
                </div>
            </div>
            <div class="marsPictures">
                <img :src="marsInfos[idx].img_src" alt="photo prise par Spirit" id="picture"> 
            </div>
        </div>
    </div>
</template>



<script>
import axios from "axios";
import Banner from "@/components/Banner.vue";
export default {
    name: "March",
    components: {
        Banner,
    },
    data() {
        return {
            choice: "",
            dateChoice: "",
            marsInfos: [],

        }
    },
    mounted() {
        // this.dayDate();
        // console.log(this.dayDate());
        // this.numberOfDays();
        // console.log(this.numberOfDays());
    },
    methods: {
        test() {
            console.log(this.choice);
        },
        dayDate() {
        let today = new Date();
        let day = today.getDate();
        let month = today.getMonth()+1;
        let year = today.getFullYear();

        if (day < 10) {
            day = "0" + day;
        }
        if (month < 10) {
            month = "0" + month;
        }
        return today = year + "-" + month + "-" + day;
        },
        numberOfDays(day1, day2) {
            const dayOne = new Date(day1);
            const finalDay = new Date(day2);
            console.log(dayOne);
            console.log(finalDay);

            const differenceTime = finalDay.getTime() - dayOne.getTime();
            const differenceDays = differenceTime / (1000 * 3600 * 24);
            console.log(Math.round((differenceDays)/1.0274884259259));
            return Math.round((differenceDays)/1.0274884259259);
        },
        changeDate(day1, day2) {
            const self = this;
            const rover = this.choice;

            axios.get("https://api.nasa.gov/mars-photos/api/v1/rovers/" + rover + "/photos?sol=" + self.numberOfDays(day1, day2) + "&api_key=9JKnUxPcyCGeQrgjiZBWWVs3daiFomUmy4kIMWsg")
                .then(function(response) {
                    self.marsInfos = response.data.photos;
                    console.log(self.marsInfos);
                })
                .catch(function(error) {
                    console.log(error);
                })
        },
    }
    
}
</script>



<style lang="scss" scoped>
label, p {
    color: white;
}

img {
    width: 500px;
}
</style>