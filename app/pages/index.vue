<template>
  <section class="home">
    <div class="py-24 md:py-36 mx-auto flex flex-wrap flex-col md:flex-row items-center">
      <div class="flex flex-col w-full xl:w-3/5 justify-center lg:items-start overflow-y-hidden">
        <div v-html="$md.render(welcomeText)" class="home__welcome markdown" />
      </div>
      <div class="flex flex-col w-full xl:w-2/5">
        <div class="mb-12 xl:mb-0">
          <h3 v-if="isSignedUp">Thank you - your participation is much appreciated.</h3>
          <p v-if="isSignedUp">{{form.selectedState}}</p>
          <div v-if="isSignedUp" v-for="selected in form.selectedMethod">
           {{selected}}
          </div>
          <form
            v-else
            @submit.prevent="handleSubmit"
            name="signups"
            netlify
            class="flex items-center border-b border-b-2 border-blue-400 py-2"
          >
          <div class="grid grid-flow-row auto-rows-max">
            <div>
              <input
                ref="nameInput"
                v-model="form.name"
                class="appearance-none mb-36 bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
                type="text"
                name="name"
                placeholder="Your Name"
                aria-label="Your name"
              />
              <input
              ref="emailInput"
              v-model="form.email"
              class="appearance-none mb-36 bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
              type="text"
              name="email"
              placeholder="Your@email.com"
              aria-label="Email address"
            />
            </div>
            <div>
              <select 
              class="appearance-none mb-36 bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"  v-model="form.selectedState"
              ref="selectedState"
              name="state"
              placeholder="Resident State"
              aria-label="Resident state"
              >
                <option v-for="state in states" v-bind:value="state.value">
                  {{ state.text }}
                </option>
              </select>
            </div>
            <div>
              <select 
              class="appearance-none mb-36 bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
              ref="selectedMethods"
              name="methods"
              placeholder="Contact Method"
              aria-label="Contact method"
              v-model="form.selectedMethods" multiple>
                <option>E-mail</option>
                <option>Call</option>
                <option>Mail</option>
              </select>
            </div>
            <div>
              <button
                class="flex-shrink-0 bg-blue-500 hover:bg-blue-700 border-blue-500 hover:border-blue-700 text-sm border-4 text-white py-1 px-2 rounded"
                type="submit"
              >
                Next
              </button>
            </div>
          </div>
          </form>
        </div>
      </div>
    </div>


    <div class="py-12 md:py-36 mx-auto flex flex-wrap flex-col md:flex-row items-center">
      <div class="flex flex-col w-full xl:w-2/5">
        <img
          alt="Hero"
          class="rounded"
          src="@/static/images/uploads/elder1.jpg"
        />
      </div>
      <div class="flex flex-col w-full xl:w-3/5 justify-center lg:items-start overflow-y-hidden">
        <div v-html="$md.render(section1)" class="home__welcome markdown" />
      </div>
    </div>

    <div class="py-12 md:py-36 mx-auto flex flex-wrap flex-col md:flex-row items-center">
      <div class="flex flex-col w-full xl:w-3/5 justify-center lg:items-start overflow-y-hidden">
        <div v-html="$md.render(section2)" class="home__welcome markdown" />
      </div>
      <div class="flex flex-col w-full xl:w-2/5 focus-visible:translate-x-12">
        <img
          alt="Hero"
          class="rounded"
          src="@/static/images/uploads/elder2.jpg"
        />
      </div>
    </div>

    <div class="py-12 md:py-36 mx-auto flex flex-wrap flex-col md:flex-row items-center">
      <div class="flex flex-col w-full xl:w-2/5">
        <img
          alt="Hero"
          class="rounded"
          src="@/static/images/uploads/elder3.jpg"
        />
      </div>
      <div class="flex flex-col w-full xl:w-3/5 justify-center lg:items-start overflow-y-hidden">
        <div v-html="$md.render(section3)" class="home__welcome markdown" />
      </div>
    </div>

  </section>
</template>

<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
import settings from '@/content/settings/general.json';

@Component({
  // Called to know which transition to apply
  transition() {
    return 'slide-left';
  },
})
export default class Home extends Vue {
  welcomeText = settings.welcomeText;
  section1 = settings.section1;
  section2 = settings.section2;
  section3 = settings.section3;

  get posts(): Post[] {
    return this.$store.state.posts;
  }

  isSignedUp = false;

  form = {
    email: '',
    selectedState: '',
    selectedMethods: []
  };

  states = [
    {"text":"Alabama", "value":"AL"},
    {"text":"Alaska", "value":"AK"},
    {"text":"Arizona", "value":"AZ"},
    {"text":"Arkansas", "value":"AR"},
    {"text":"California", "value":"CA"},
    {"text":"Colorado", "value":"CO"},
    {"text":"Connecticut", "value":"CT"},
    {"text":"Delaware", "value":"DE"},
    {"text":"Florida", "value":"FL"},
    {"text":"Georgia", "value":"GA"},
    {"text":"Hawaii", "value":"HI"},
    {"text":"Idaho", "value":"ID"},
    {"text":"Illinois", "value":"IL"},
    {"text":"Indiana", "value":"IN"},
    {"text":"Iowa", "value":"IA"},
    {"text":"Kansas", "value":"KS"},
    {"text":"Kentucky", "value":"KY"},
    {"text":"Louisiana", "value":"LA"},
    {"text":"Maine", "value":"ME"},
    {"text":"Maryland", "value":"MD"},
    {"text":"Massachusetts", "value":"MA"},
    {"text":"Michigan", "value":"MI"},
    {"text":"Minnesota", "value":"MN"},
    {"text":"Mississippi", "value":"MS"},
    {"text":"Missouri", "value":"MO"},
    {"text":"Montana", "value":"MT"},
    {"text":"Nebraska", "value":"NE"},
    {"text":"Nevada", "value":"NV"},
    {"text":"New Hampshire", "value":"NH"},
    {"text":"New Jersey", "value":"NJ"},
    {"text":"New Mexico", "value":"NM"},
    {"text":"New York", "value":"NY"},
    {"text":"North Carolina", "value":"NC"},
    {"text":"North Dakota", "value":"ND"},
    {"text":"Ohio", "value":"OH"},
    {"text":"Oklahoma", "value":"OK"},
    {"text":"Oregon", "value":"OR"},
    {"text":"Pennsylvania", "value":"PA"},
    {"text":"Rhode Island", "value":"RI"},
    {"text":"South Carolina", "value":"SC"},
    {"text":"South Dakota", "value":"SD"},
    {"text":"Tennessee", "value":"TN"},
    {"text":"Texas", "value":"TX"},
    {"text":"Utah", "value":"UT"},
    {"text":"Vermont", "value":"VT"},
    {"text":"Virginia", "value":"VA"},
    {"text":"Washington", "value":"WA"},
    {"text":"West Virginia", "value":"WV"},
    {"text":"Wisconsin", "value":"WI"},
    {"text":"Wyoming", "value":"WY"}
  ];

  encode(data): string {
    return Object.keys(data)
      .map((key) => `${encodeURIComponent(key)}=${encodeURIComponent(data[key])}`)
      .join('&');
  }

  validEmail(email): boolean {
    // eslint-disable-next-line
    const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(email);
  }

  async handleSubmit(): Promise<void> {
    if (!this.validEmail(this.form.email)) {
      //this.$refs.emailInput.focus();
      return;
    }

    try {
      await fetch('/', {
        method: 'POST',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        body: this.encode({ 'form-name': 'signups', ...this.form }),
      });

      this.isSignedUp = true;
    } catch (error) {
      console.error(error);
    }
  }
}
</script>
