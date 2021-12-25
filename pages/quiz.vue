<template>
  <b-container style="padding: 50px;">
    <div v-if="show_form">
      <b-row>
        <h1 style="margin-left: 30%; color: #f8f3ef; font-size: 75px; font-family: 'Mountains of Christmas';">Make a decision</h1>
      </b-row>
      <br>
      <b-row>
        <b-form-select v-model="cuisine_selected" :options="cuisine_options"></b-form-select>
      </b-row>
      <br><br>
      <b-row>
        <b-form-select v-model="speed_selected" :options="speed_options"></b-form-select>
      </b-row>
      <br><br>
      <b-row>
        <b-form-select v-model="health_selected" :options="health_options"></b-form-select>
      </b-row>
      <br><br>
      <b-row>
        <b-button @click="get_recs" variant="outline-light" style="margin: auto; width: 40%;font-family: 'Mountains of Christmas';">
            <h2>Let's go!</h2>
        </b-button>
      </b-row>
    </div>
    <div v-if="show_form == false">
      <h1 style="color: #f8f3ef; font-size: 75px; font-family: 'Mountains of Christmas';">
        Here are your recommendations!
      </h1>
      <br>
      <b-row>
        <h3 style="color: #f8f3ef; font-size: 1.6vw;">
          Name: {{recommendations[rec_index].name}}
        </h3>
      </b-row>
      <br>
      <b-row>
        <p class="rec">
          Description: {{recommendations[rec_index].description}} 
        </p>
      </b-row>
      <br>
      <b-row>
        <p class="rec">
          Location: {{recommendations[rec_index].location}} 
        </p>
      </b-row>
      <br>
      <b-row>
        <p class="rec">
          Contact: {{recommendations[rec_index].contact}} 
        </p>
      </b-row>
      <br>
      <b-row>
        <p class="rec">
          Menu link: <NuxtLink style="color:#33BEFF" :to="recommendations[rec_index].menu"> {{recommendations[rec_index].menu}} </NuxtLink>
        </p>
      </b-row>
      <br>
      <b-row>
        <p class="rec">
          Cuisines: {{recommendations[rec_index].cuisine}} 
        </p>
      </b-row>
      <br>
      <b-row>
        <p class="rec">
          Healthy? {{recommendations[rec_index].healthy}} 
        </p>
      </b-row>
      <br>
      <b-row>
        <p class="rec">
          Speed: {{recommendations[rec_index].speed}} 
        </p>
      </b-row>
      <br>
      <b-row>
        <b-button @click="move_index" variant="outline-light" style="margin: auto; width: 40%;font-family: 'Mountains of Christmas';">
          <h2>Let's go!</h2>
        </b-button>
      </b-row>
      <br>
      <b-row>
          <b-button @click="show_form = true" variant="outline-light" style="margin: auto; width: 30%;font-family: 'Mountains of Christmas';">
            <h2>Make a decision for me!</h2>  
          </b-button>
      </b-row>
    </div>
  </b-container>
</template>

<script>
  export default {
    data() {
      return {
        rec_index: 0,
        show_form: true,
        restaurants: [
            {
              name: 'Bistro-2-Go',
              description: 'As busy students, we know you don’t always have time to get to the grocery store for your weekly food shop. Bistro-2-Go offers convenient shopping for students on the go, offering a wide range of snacks, light meals and beverages. Located in the Mary Keyes Residence Building, Bistro-2-Go also offers a selection of fast and healthy pitas from Needa Pita and a menu of delicious coffees and pastries from Tim Hortons. For those seeking speed, convenience and variety, Bistro-2-Go is the perfect one-stop shop.',
              location: 'Mary E. Keyes Residence, 1st Floor',
              contact: '905-525-9140 ext. 26500',
              menu: 'https://hospitality.mcmaster.ca/locations/on-campus/east-meets-west/',
              cuisine: ['american'],
              healthy: ['no'],
              speed: 'fast'
            },
            {
              name: 'LA Piazza',
              description: 'Located in the hub of the Student Centre, La Piazza encapsulates the essence of campus dining and student activity. With diverse food stations that offer Halal options, homemade comfort foods, all-day breakfast specials, a salad bar and even a popcorn station, this one-stop shop has something for everyone. La Piazza accepts cash, debit, credit and the flex dollars from your McMaster Meal Plan.',
              location: 'McMaster University Student Centre (MUSC), 1st Floor',
              contact: '905-525-9140 ext. 24240',
              menu: 'https://hospitality.mcmaster.ca/locations/on-campus/la-piazza/',
              cuisine: ['middle-eastern', 'american', 'indian', 'east-asian', 'italian', 'mexican'],
              healthy: ['yes', 'no'],
              speed: 'slow'
            },
            {
              name: 'Bistro at MKR',
              location: 'Mary E. Keyes Residence, 1st Floor',
              contact: '905-525-9140 ext. 26500',
              menu: 'https://hospitality.mcmaster.ca/locations/on-campus/east-meets-west/',
              cuisine: ['american', 'italian', 'mexican', 'chinese', 'japanese'],
              healthy: ['yes','no'],
              speed: 'slow'
            },
            {
              name: 'Starbucks Coffee',
              description: 'Conveniently located in the McMaster University Student Centre (MUSC), this on-campus Starbucks offers a wide variety of healthy snacks, freshly-prepared sandwiches and a great selection of hot and cold beverages. Pair a handcrafted coffee with a delicious pastry to snack on as you head to class. Or, take advantage of MUSC’s extensive seating areas and treat yourself to a caffeinated study break. Starbucks is open every weekday to accommodate your busy schedule.',
              location: 'McMaster University Student Centre (MUSC), 1st Floor',
              contact: '905-525-9140 ext. 24243',
              menu: 'https://www.starbucks.ca/menu',
              cuisine: ['american'],
              healthy: ['no'],
              speed: 'fast'
            },
            {
              name: 'IAHS Cafe',
              description: 'This popular Cafe in the Institute for Applied Health Sciences has several food stations to satisfy your every craving. In the mood for cozy comfort food? Our “Hot on the Go” section features a menu of your favourite hot meals like homemade lasagna, mac and cheese and mini pizzas from our Pizza Pizza oven. If you’re in the mood for something light and nutritious, our “Greens on the Go” station offers delicious specialty bowls and fresh, build-your-own salads. Our “PASTAbilities” section offers you the choice to try our daily pasta specials or create your own. With other options of grab-and-go snacks, fresh fruit and even a self-serve Tim Hortons coffee and baked goods section, the IAHS Cafe has everything you need to feed your appetite!',
              location: 'Institute for Applied Health Science (IAHS), 1st Floor',
              contact: '905-525-9140 ext. 26936',
              menu: 'https://hospitality.mcmaster.ca/locations/on-campus/iahs-cafe/',
              cuisine: ['american'],
              healthy: ['no'],
              speed: 'fast'
            },
            {
              name: 'CENTRO@Commons',
              description: 'Located in the heart of the Commons Building, this diverse marketplace offers an extensive menu that is sure to satisfy your appetite. With healthy food options, international cuisine nights and delectable dessert options, it’s no wonder CENTRO is one of our most popular campus dining halls. With stations featuring delicious Asian-inspired cuisine, a variety of artisan sandwiches, Italian and Mediterranean dishes and an a la carte station offering hot entrées, it’s hard to pass up this prime dining experience!',
              location: 'Commons Building, 2nd Floor',
              contact: '905-525-9140 ext. 24245',
              menu: 'https://hospitality.mcmaster.ca/locations/on-campus/centro/',
              cuisine: ['east-asian', 'indian', 'middle-eastern', 'american', 'italian'],
              healthy: ['yes', 'no'],
              speed: 'slow'
            },
            {
              name: 'Second Cup',
              description: '(no description)',
              location: 'Peter George Centre for Living and Learning',
              contact: '(no contact)',
              menu: 'https://secondcup.com/menu',
              cuisine: ['american'],
              healthy: ['no'],
              speed: 'fast'
            },
            {
              name: 'Tim Hortons',
              description: 'We know that Tim Hortons is a staple of your Canadian university dining experience. Located in the Student Centre, Tim Hortons is one of our most popular places on campus to grab a coffee or a quick snack on the go. Specialized in serving fresh, delicious foods that are prepared daily and a wide selection of beverages, stopping by Tim Hortons is sure to become the best part of your daily routine.',
              location: 'McMaster University Student Centre (MUSC), 1st Floor',
              contact: '905-525-9140 ext. 24240',
              menu: 'timhortons.ca/menu/picker-picker_7407',
              cuisine: ['american'],
              healthy: ['no'],
              speed: 'fast'
            },
          ],
        cuisine_options: [
          { value: null, text: 'Please select a cuisine' },
          { value: 'american', text: 'American'},
          { value: 'mexican', text: 'Mexican' },
          { value: 'italian', text: 'Italian' },
          { value: 'east-asian', text: 'East Asian'},
          { value: 'middle-eastern', text: 'Middle Eastern'},
          { value: 'indian', text: 'Indian'}
        ],
        cuisine_selected: null,
        speed_options: [
          { value: null, text: 'Please select a speed' },
          { value: 'fast', text: 'Fast (take-out)' },
          { value: 'slow', text: 'Slow (sit-in)' }
        ],
        speed_selected: null,
        health_options: [
          { value: null, text: 'Do you want eat healthy?' },
          { value: 'yes', text: 'Yes' },
          { value: 'no', text: 'No' }
        ],
        health_selected: null,
      };
    },
    methods: {
      get_recs() {
        if (this.recommendations.length == 0) {
          alert("No restaurants found that meet the criteria don't be so picky");
        }
        else {
          this.show_form = false;
        }
        console.log("get recs");
      },
      move_index() {
        if (this.rec_index == this.recommendations.length-1) {
          alert("No more restaurants fit the criteria just choose one jesus christ");
          this.rec_index = 0;
        }
        else {
          this.rec_index ++;
        }
      }
    },
    computed: {
      recommendations() {
        var recs = [];
        for (let i=0; i<this.restaurants.length;i++) {
          var r = this.restaurants[i];
          if (r.cuisine.includes(this.cuisine_selected) && r.speed == this.speed_selected && r.healthy.includes(this.health_selected)) {
            recs.push(r);
          }
        }
        for (var i = recs.length - 1; i > 0; i--) {
          var j = Math.floor(Math.random() * (i + 1));
          var temp = recs[i];
          recs[i] = recs[j];
          recs[j] = temp;
        }
        return recs;
      }
    }
  }
</script>

<style scoped>
@font-face {
  font-family: 'Mountains of Christmas';
  font-style: normal;
  src: local("Mountains of Christmas"), local("MountainsofChristmas-Regular"), url(https://fonts.gstatic.com/s/mountainsofchristmas/v8/dVGBFPwd6G44IWDbQtPewylJhLDHyIrT3I5b5eGTHmw.woff2) format("woff2"); }
  .rec {
    color: #f8f3ef;
    font-size: 1.3vw;
  }
</style>