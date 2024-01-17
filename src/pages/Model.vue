<template>
  <div class="background-section">
    <div class="content-overlay">
      <table class="overlay-table">
        <tr>
          <td class="text-column">
            <h1 class="overlay-text">
              Find the perfect employee in our database of more than 25,000 new multilingual candidates each month.
            </h1>
          </td>
          <td class="td-icon">
            <img src="src/statics/icons/group-white.png" alt="icon-group" class="icon" />
          </td>
          <td colspan="2">
            <h1 class="first-number">+ 2,500</h1>
            <p class="first-text">companies posting in more than 48 countries</p>
          </td>
        </tr>
        <tr>
          <td>
            <button class="post-job-button">POST A JOB</button>
          </td>
          <td>
            <div class="second-icon-container">
              <img src="src/statics/icons/clock-white.png" alt="icon-clock" class="icon" />
            </div>
          </td>
          <td colspan="2">
            <h1 class="second-number">Post with ease</h1>
            <p class="second-text">Publish a job advert in just 2 minutes</p>
          </td>
        </tr>
        <tr>
          <td></td>
          <td>
            <div class="second-icon-container">
              <img src="src/statics/icons/file-white.png" alt="icon-clock" class="icon" />
            </div>
          </td>
          <td colspan="2">
            <h1 class="second-number">+ 50,000</h1>
            <p class="second-text">candidate applications per month</p>
          </td>
        </tr>
      </table>
      <div class="q-pa-md">
        <q-carousel
          class="custom-carousel"
          animated
          v-model="slide"
          navigation
          infinite
          :autoplay="autoplay"
          arrows
          transition-prev="slide-rigth"
          transition-next="slide-left"
          @mouseenter="autoplay = false"
          @mouseleave="autoplay = true">
          <q-carousel-slide :name="1" class="column no-wrap">
            <div class="row fit justify-start items-center q-gutter-xs q-col-gutter no-wrap">
              <q-img class="rounded-borders col-6 custom-img2" src="https://static.europelanguagejobs.com/contents/banners/logo-ttec-611-874.svg" />
              <q-img class="rounded-borders col-6 custom-img2" src="https://static.europelanguagejobs.com/contents/banners/top-companies-posting-foundever-portugal-610-9042.svg" />
            </div>
          </q-carousel-slide>
          <q-carousel-slide :name="2" class="column no-wrap">
            <div class="row fit justify-start items-center q-gutter-xs q-col-gutter no-wrap">
              <q-img class="rounded-borders col-6 custom-img" src="https://static.europelanguagejobs.com/contents/banners/logo-agoda-607-4993.svg" />
              <q-img class="rounded-borders col-6 custom-img" src="https://static.europelanguagejobs.com/contents/banners/airproducts-logo-612.svg" />
              <q-img class="rounded-borders col-6 custom-img" src="https://static.europelanguagejobs.com/contents/banners/logo-top-company-apple-609-1600.svg" />
            </div>
          </q-carousel-slide>
        </q-carousel>
      </div>
    </div>
  </div>
  <div class="second-div">
    <h1 class="elj-text">ELJ's <span class="bold-text">Hiring Solutions</span></h1>
    <table class="second-table">
      <tr>
        <td class="td-second-table">
          <img src="https://www.europelanguagejobs.com/statics/images/job-posting.svg" alt="">
        </td>
        <td class="td-second-table">
          <img src="https://www.europelanguagejobs.com/statics/images/cv-search.svg" alt="">
        </td>
        <td class="td-second-table">
          <img src="https://www.europelanguagejobs.com/statics/images/exposure-features.svg" alt="">
        </td>
        <td class="td-second-table">
          <img src="https://www.europelanguagejobs.com/statics/images/outreach-features.svg" alt="">
        </td>
      </tr>
      <tr>
        <td class="td-second-table">
          <h1 class="elj-text bold-text">JOB POSTING</h1>
        </td>
        <td class="td-second-table">
          <h1 class="elj-text bold-text">CV SEARCH</h1>
        </td>
        <td class="td-second-table">
          <h1 class="elj-text bold-text">WEBSITE VISIBILITY</h1>
        </td>
        <td class="td-second-table">
          <h1 class="elj-text bold-text">OUTREACH FEATURES</h1>
        </td>
      </tr>
    </table>
  </div>
  <div class="third-div">
    <h1 class="elj-text-white">Find more about our basic and personalized hiring solutions</h1>
    <button class="post-job-button">LEARN MORE</button>
  </div>
  <div class="fourth-div">
    <h1 class="elj-text"><span class="bold-text">Tell us about </span>your needs!</h1>
    <div class="q-pa-md" style="max-width: 500px; background-color: rgb(244, 244, 244); margin: 0 auto">
      <q-form
        @submit="onSubmit"
        @reset="onReset"
        class="q-gutter-md">
        <table>
          <tr>
            <td>
              <q-input
                filled
                v-model="name"
                label="Your name"
                lazy-rules
                :rules="[ val => val && val.length > 0 || 'Please fill your name']"
                outlined/>
            </td>
            <td>
              <q-input
                filled
                v-model="additionalText"
                label="Your message"
                lazy-rules
                :rules="[
                  val => val !== null && val !== '' || 'Please fill your message'
                ]"
              />
            </td>
          </tr>
          <tr>
            <td>
              <q-input
                filled
                v-model="company"
                label="Your company"
                lazy-rules
                :rules="[
                val => val !== null && val !== '' || 'Please fill your company']"/>
            </td>
            <td>
              <q-checkbox v-model="accept" label="I accept the Legal Conditions" />
            </td>
          </tr>
          <tr>
            <td>
              <q-input
                filled
                v-model="email"
                label="Your Email"
                lazy-rules
                :rules="[
                val => val !== null && val !== '' || 'Please fill your email']"/>
            </td>
            <td>
              <q-btn label="SEND MESSAGE" type="submit"
                     style="border-radius: 40px; background-color: rgb(85, 112, 145); color: white"/>
              <p>or post a job</p>
            </td>
          </tr>
        </table>
      </q-form>
    </div>
    <h1 class="elj-text"><span class="bold-text">ATS Partners & API Solutions</span></h1>
    <div class="q-pa-md">
      <q-carousel
        class="custom-carousel"
        animated
        v-model="slide"
        navigation
        infinite
        :autoplay="autoplay"
        arrows
        transition-prev="slide-rigth"
        transition-next="slide-left"
        @mouseenter="autoplay = false"
        @mouseleave="autoplay = true">
        <q-carousel-slide :name="1" class="column no-wrap">
          <div class="row fit justify-start items-center q-gutter-xs q-col-gutter no-wrap">
            <q-img class="rounded-borders col-6 custom-img3" src="https://www.europelanguagejobs.com/statics/images/broadbean.svg" />
            <q-img class="rounded-borders col-6 custom-img3" src="https://www.europelanguagejobs.com/statics/images/hrlink.svg" />
            <q-img class="rounded-borders col-6 custom-img3" src="https://www.europelanguagejobs.com/statics/images/logicmelon.svg" />
          </div>
        </q-carousel-slide>
        <q-carousel-slide :name="2" class="column no-wrap">
          <div class="row fit justify-start items-center q-gutter-xs q-col-gutter no-wrap">
            <q-img class="rounded-borders col-6 custom-img" src="https://www.europelanguagejobs.com/statics/images/equest.png" />
            <q-img class="rounded-borders col-6 custom-img" src="https://www.europelanguagejobs.com/statics/images/recruitly.png" />
            <q-img class="rounded-borders col-6 custom-img" src="https://www.europelanguagejobs.com/statics/images/lever.png" />
          </div>
        </q-carousel-slide>
      </q-carousel>
    </div>
  </div>
  <div class="third-div">
    <h1 class="elj-text-white">Together, your hires, our goal!</h1>
  </div>
  <div class="fifth-div">
    <table class="custom-table">
      <tr>
        <td rowspan="2">
          <img class="icon-europe" src="https://www.europelanguagejobs.com/statics/images/logo-elj-no-bg.png" alt="">
        </td>
        <td>
          <p class="elj-text"><span class="bold-text">FOR JOBS SEEKERS</span></p>
        </td>
        <td>
          <p class="elj-text"><span class="bold-text">FOR EMPLOYERS</span></p>
        </td>
        <td>
          <p class="elj-text"><span class="bold-text">EUROPE LANGUAGE JOBS</span></p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Find a job</p>
        </td>
        <td>
          <p>Post a job</p>
        </td>
        <td>
          <p>About us</p>
        </td>
      </tr>
      <tr>
        <td rowspan="2">
          <p>We help expats find jobs in Europe using their
            native language and gain international experience
            by working in a foreign country.</p>
        </td>
        <td>
          <p>Create an account</p>
        </td>
        <td>
          <p>Create an account</p>
        </td>
        <td>
          <p>FAQ</p>
        </td>
      </tr>
      <tr>
        <td>
          <p>Career advice</p>
        </td>
        <td>
          <p>Hiring solutions</p>
        </td>
        <td>
          <p>Legal conditions</p>
        </td>
      </tr>
      <tr>
        <td rowspan="2">
          <p style="color: blue">Europe Language Jobs - the job board for expat jobs abroad</p>
        </td>
        <td>
          <h1 class="elj-text bold-text">STAY CONNECTED</h1>
        </td>
        <td>
          <h1 class="elj-text bold-text">DOWNLOAD THE APP</h1>
        </td>
      </tr>
      <tr>
        <td>
          <img class="icon-socials" src="src/statics/icons/linkedin.png" alt="">
          <img class="icon-socials" src="src/statics/icons/facebook.png" alt="">
          <img class="icon-socials" src="src/statics/icons/tik-tok.png" alt="">
          <img class="icon-socials" src="src/statics/icons/youtube.png" alt="">
          <img class="icon-socials" src="src/statics/icons/twitter.png" alt="">
          <img class="icon-socials" src="src/statics/icons/discord.png" alt="">
        </td>
        <td>
          <img style="margin-right: 5px" src="https://static.europelanguagejobs.com/contents/images/go-places-application/google-white-button.svg" alt="">
          <img style="margin-right: 5px" src="https://static.europelanguagejobs.com/contents/images/go-places-application/apple-white-button.svg" alt="">
        </td>
      </tr>
    </table>
  </div>
</template>

<style scoped>
.background-section {
  position: relative;
  width: 100%;
  height: 550px;
  background-image: url('src/statics/images/negocio.jpeg');
  background-size: cover;
  background-position: center;
}

.content-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(16, 98, 155, 0.84);
  display: flex;
  color: white;
  flex-direction: column;
  justify-content: flex-start;
}

.overlay-table {
  width: 100%;
}

.icon-container,
.second-icon-container {
  position: relative;
}

.icon {
  width: 60px;
  height: 60px;
}

.overlay-text {
  color: white;
  text-align: left;
  max-width: 80%;
  margin-top: 30px;
  margin-left: 40px;
  font-size: 2em;
  line-height: 1.2;
  font-family: 'Roboto', sans-serif;
}

.button-container {
  text-align: left;
  margin-top: 20px;
}

.post-job-button {
  background-color: white;
  color: rgba(16, 98, 155);
  padding: 15px 30px;
  border: none;
  margin-left: 40px;
  font-weight: bold;
  font-size: 1.5em;
  cursor: pointer;
  font-family: 'Roboto', sans-serif;
  border-radius: 50px;
  width: 250px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.first-number,
.second-number {
  font-size: 2em;
  font-weight: bold;
  margin-top: -20px;
  height: 40px;
}

.first-text,
.second-text{
  margin-top: 1px;
  font-size: 1.2em;
}

.text-column {
  width: 50%;
}

.td-icon {
  width: 5%;
}

.custom-carousel {
  background: transparent !important;
  height: 150px;
}

.custom-img {
  width: 450px;
  height: 150px;
}

.custom-img2 {
  width: 600px;
  height: 150px;
}

.second-div {
  text-align: center;
}

.elj-text {
  color: darkblue;
  font-size: 1.5em;
}

.elj-text-white {
  color: white;
  font-size: 1.5em;
}

.bold-text {
  font-weight: bold;
}

.second-table {
  width: 100%;
  text-align: center;
}

.td-second-table {
  width: 5%;
}

.third-div {
  background-color: rgb(0, 124, 192);
  text-align: center;
  display: flex;
  align-items: center;
  padding: 20px;
  justify-content: center;
}

.fourth-div {
  text-align: center;
}

.custom-img3 {
  max-width: 400px;
  width: 100%;
  height: auto;
}

.custom-table {
  margin: 40px 60px;
  width: calc(100% - 120px);
  border-collapse: collapse;
  border-top: 2px solid black;
  border-bottom: 2px solid black;
}

.icon-europe {
  width: 90px;
  height: 90px;
}

.custom-table td:first-child {
  max-width: 300px;
  word-wrap: break-word;
  white-space: normal;
}

.icon-socials {
  width: 30px;
  height: 30px;
  margin-right: 5px;
}
</style>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue';

export default {
  setup () {
    const $q = useQuasar();

    const name = ref(null);
    const company = ref(null);
    const email = ref(null);
    const accept = ref(false);
    const additionalText = ref(null);

    return {
      slide: ref(1),
      autoplay: ref(true),
      name,
      company,
      email,
      additionalText,
      accept,
      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'You need to accept the license and terms first'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
      },
      onReset () {
        name.value = null
        company.value = null
        accept.value = false
      }
    };
  }
};
</script>
