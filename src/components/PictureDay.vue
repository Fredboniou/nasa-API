<template>
    <div className="display">
            <Banner title="Nasa-API" />
            <p>Choisir une date</p>
            <input type="date" v-model="dateChoice" name="picDate" id="picDate" min="1995-06-16" :max="dayDate()" @change="changeDate()" />
            <div class="infos">
                <div class="text">
                    <p class="date">{{ picInfos.date }}</p>
                    <p class="title">{{ picInfos.title }}</p>
                    <p class="explanation">{{ picInfos.explanation }}</p>
                </div>
                <img :src="picInfos.url" :alt="picInfos.title" class="pic" />
            </div>
        </div> 
</template>



<script>
import axios from "axios";
import Banner from "@/components/Banner.vue";
export default {
    name: "PictureDay",
    components: {
        Banner,
    },
    data() {
        return {
            picInfos: [],
            dateChoice: "",
        }
    },
    mounted() {
        this.pictureDisplay();
        console.log(this.dateChoice);
    },
    computed: {
        dateDisplay(originalDate) {
            let [yyyy, mm, dd] = originalDate.split("-");
            return [dd, mm, yyyy].join("/");
        },
    },
    methods: {
        pictureDisplay() {
            const self = this;

            axios.get("https://api.nasa.gov/planetary/apod?api_key=9JKnUxPcyCGeQrgjiZBWWVs3daiFomUmy4kIMWsg")
                .then(function(response) {
                    self.picInfos = response.data;
                    console.log(self.picInfos);
                })
                .catch(function(error) {
                    console.log(error);
                })
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
        changeDate() {
            const self = this;
            const choiceDate = this.dateChoice;

            axios.get("https://api.nasa.gov/planetary/apod?api_key=9JKnUxPcyCGeQrgjiZBWWVs3daiFomUmy4kIMWsg&date=" + choiceDate)
                .then(function(response) {
                    self.picInfos = response.data;
                    console.log(self.picInfos);
                })
                .catch(function(error) {
                    console.log(error);
                })
        },
        test() {
            console.log('ok');
        }
    }
}
</script>



<style lang="scss" scoped>
p {
    color: white;
    font-size: 1.2rem;
}

.infos {
    display: flex;
    justify-content: space-around;
}

.text {
    width: 50%;
    text-align: center;
}

.explanation {
    text-align: justify;
}

.pic {
    width: 500px;
    border-radius: 10px;
}

</style>