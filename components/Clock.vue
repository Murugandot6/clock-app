<template>
  <div :class="pageBg">
    <main class="contents">
      <section class="quotes" :class='{quotes__expanded: expanded}'>
          <div class="quotes__wrapper">
            <p class="txt">{{ quote }}</p>
            <p class="author">{{ author }}</p>
          </div>
          <div>
            <button type="button" @click="getQuotes()" class="quotes__btn" :disabled="disabled">
                <img src="../assets/images/refresh.png" alt="refresh button" :class="{rotate: disabled}">
            </button>
          </div>
      </section>
      <section class="times" :class='{times__expanded: expanded}'>
        <div class="times__wrapper">
          <p class="greeting">
            <span v-if="greeting == 'morning'">
              <svg width="24" height="24" xmlns="http://www.w3.org/2000/svg"><path d="M11.78 19.417c.594 0 1.083.449 1.146 1.026l.006.125v1.842a1.152 1.152 0 01-2.296.125l-.007-.125v-1.842c0-.636.516-1.151 1.152-1.151zM6.382 17.18a1.15 1.15 0 01.09 1.527l-.09.1-1.302 1.303a1.152 1.152 0 01-1.718-1.528l.09-.1 1.302-1.302a1.15 1.15 0 011.628 0zm12.427 0l1.303 1.303a1.15 1.15 0 11-1.628 1.627L17.18 18.81a1.15 1.15 0 111.628-1.628zM11.781 5.879a5.908 5.908 0 015.901 5.902 5.908 5.908 0 01-5.901 5.902 5.908 5.908 0 01-5.902-5.902 5.908 5.908 0 015.902-5.902zm10.63 4.75a1.151 1.151 0 110 2.303h-1.843a1.151 1.151 0 110-2.303h1.842zm-19.418 0a1.151 1.151 0 01.126 2.296l-.125.007H1.15a1.151 1.151 0 01-.125-2.296l.125-.007h1.842zm1.985-7.268l.1.09 1.303 1.302a1.151 1.151 0 01-1.528 1.718l-.1-.09L3.45 5.08A1.15 1.15 0 014.978 3.36zm15.133.09c.45.449.45 1.178 0 1.628L18.808 6.38a1.151 1.151 0 11-1.628-1.628l1.303-1.303c.449-.449 1.178-.449 1.628 0zM11.781 0c.636 0 1.151.515 1.151 1.151v1.843a1.152 1.152 0 01-2.303 0V1.15C10.63.515 11.145 0 11.781 0z" fill="#FFF" fill-rule="nonzero"/></svg>
              good morning
            </span>
            <span v-if="greeting === 'afternoon'">
              <svg width="23" height="24" xmlns="http://www.w3.org/2000/svg"><path d="M22.157 17.366a.802.802 0 00-.891-.248 8.463 8.463 0 01-2.866.482c-4.853 0-8.8-3.949-8.8-8.8a8.773 8.773 0 013.856-7.274.801.801 0 00-.334-1.454A7.766 7.766 0 0012 0C5.382 0 0 5.382 0 12s5.382 12 12 12c4.2 0 8.02-2.134 10.218-5.709a.805.805 0 00-.061-.925z" fill="#FFF" fill-rule="nonzero"/></svg>
              good afternoon
            </span>
            <span v-else>
              <svg width="23" height="24" xmlns="http://www.w3.org/2000/svg"><path d="M22.157 17.366a.802.802 0 00-.891-.248 8.463 8.463 0 01-2.866.482c-4.853 0-8.8-3.949-8.8-8.8a8.773 8.773 0 013.856-7.274.801.801 0 00-.334-1.454A7.766 7.766 0 0012 0C5.382 0 0 5.382 0 12s5.382 12 12 12c4.2 0 8.02-2.134 10.218-5.709a.805.805 0 00-.061-.925z" fill="#FFF" fill-rule="nonzero"/></svg>
              good evening
            </span>
            <span v-if="windowSize >= 394">
              , it's currently
            </span>
          </p>
          <h1 class="time">{{ time }}<span>{{ abbreviation }}</span></h1>
          <p class="location">In {{ location }}</p>
        </div>
        <div>
          <div v-show="!showDetails">
            <button @click="openModal(true)" class="times__btn">
              <span class="times__btn--txt">more</span>
              <span class="times__btn--icon">
                <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#FFFFFF"><path d="M0 0h24v24H0z" fill="none"/><path d="M16.59 8.59L12 13.17 7.41 8.59 6 10l6 6 6-6z"/></svg>              </span>
            </button>
          </div>
          <div v-show="showDetails">
            <button @click="openModal(false)" class="times__btn">
              <span class="times__btn--txt">less</span>
              <span class="times__btn--icon">
                <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#FFFFFF"><path d="M0 0h24v24H0z" fill="none"/><path d="M12 8l-6 6 1.41 1.41L12 10.83l4.59 4.58L18 14z"/></svg>              </span>
            </button>
          </div>
        </div>
      </section>
      <section class="details" :class="[detailBg, {details__expanded: expanded}]">
        <div class="details__first">
          <div>
            <p>current timezone</p>
            <h2>{{ timezone }}</h2>
          </div>
          <div>
            <p>day of the year</p>
            <h2>{{ dayOfTheYear }}</h2>
          </div>
        </div>
        <span class="details__line"></span>
        <div  class="details__second">
          <div>
              <p>day of the week</p>
            <h2>{{ dayOfTheWeek }}</h2>
          </div>
          <div>
            <p>week number</p>
            <h2>{{ weekNumber }}</h2>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data () {
      return {
        greeting: null,
        time: "00:00",
        abbreviation: null,
        location: null,
        timezone: null,
        dayOfTheYear: null,
        dayOfTheWeek: null,
        weekNumber: null,
        quote: "“The science of operations, as derived from mathematics more especially, is a science of itself, and has its own abstract truth and value.”",
        author: "Ada Lovelace",
        pageBg: "bg-noon",
        detailBg: "details__noon",
        showQuotes: true,
        showDetails: false,
        greeting: "morning",
        styleObject: "added",
        expanded: false,
        windowSize: 0,
        disabled: false
      }
    },
    created () {
      this.getData()
      this.getQuotes()
      this.windowSize = window.innerWidth
    },
    mounted () {
      let timerID = setInterval(this.updateTime, 1000);
    },
    methods: {
      async getData () {
        await axios.get("https://api.freegeoip.app/json/?apikey=" + process.env.API_KEY)
          .catch((error) => {
            console.log(error)
            alert("Oops! Something went wrong. Please try again.")
            return
          })
          .then((res) => {
            this.timezone = res.data.time_zone
            this.location = res.data.city + ",  " + res.data.country_code
          })
        await axios.get("https://worldtimeapi.org/api/timezone/" + this.timezone)
          .catch((error) => {
            console.log(error)
            alert("Oops! Something went wrong. Please try again.")
            return
          })
          .then((res) => {
            this.abbreviation = res.data.abbreviation
            this.dayOfTheYear = res.data.day_of_year
            this.dayOfTheWeek = res.data.day_of_week
            this.weekNumber = res.data.week_number
          })
      },
      updateTime () {
        const preTime = new Date()
        const hours = preTime.getHours()
        if (hours > 5 && hours < 12) {
          this.greeting = "morning"
          this.pageBg = "bg-noon"
          this.detailBg = "details__noon"
        } else if (hours >= 12 && hours < 18) {
          this.greeting = "afternoon"
          this.pageBg = "bg-noon"
          this.detailBg = "details__noon"
        } else if (hours < 5 || hours >= 18) {
          this.greeting = "evening"
          this.pageBg = "bg-night"
          this.detailBg = "details__night"
        }
        const minutes = ("0" + preTime.getMinutes()).slice(-2)
        this.time = hours + ":" + minutes
      },
      async getQuotes () {
        this.disabled = true
        await axios.get("https://programming-quotes-api.herokuapp.com/Quotes/random")
        .catch((error) => {
          console.log(error)
          alert("Oops! Something went wrong. Please try again.")
          return
        })
        .then((res) => {
          this.quote = res.data.en
          this.author = res.data.author
          this.disabled = false
        })
      },
      openModal (modal) {
        if (modal) {
          this.showDetails = true
          this.expanded = true
        } else {
          this.showDetails = false
          this.expanded = false
        }
      }
    }
  }
</script>
