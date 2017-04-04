<template lang="pug">
  #app
    img(src='https://platzi.github.io/platzimusic/dist/logo.png')
    h1 PlatziMusic
    select(v-model="selectedCountry")
      option(v-for="country in countries" v-bind:value="country.value") {{ country.name }}
    spinner(v-show="loading")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { name: 'Afghanistan', value: 'afghanistan' },
          { name: 'Albania', value: 'albania' },
          { name: 'Algeria', value: 'algeria' },
          { name: 'Andorra', value: 'andorra' },
          { name: 'Angola', value: 'angola' },
          { name: 'Anguilla', value: 'anguilla' },
          { name: 'Antarctica', value: 'antarctica' },
          { name: 'Argentina', value: 'argentina' },
          { name: 'Armenia', value: 'armenia' },
          { name: 'Aruba', value: 'aruba' },
          { name: 'Australia', value: 'australia' },
          { name: 'Austria', value: 'austria' },
          { name: 'Azerbaijan', value: 'azerbaijan' },
          { name: 'Bahamas', value: 'bahamas' },
          { name: 'Bahrain', value: 'bahrain' },
          { name: 'Bangladesh', value: 'bangladesh' },
          { name: 'Barbados', value: 'barbados' },
          { name: 'Belarus', value: 'belarus' },
          { name: 'Belgium', value: 'belgium' },
          { name: 'Belize', value: 'belize' },
          { name: 'Benin', value: 'benin' },
          { name: 'Bermuda', value: 'bermuda' },
          { name: 'Bhutan', value: 'bhutan' },
          { name: 'Bolivia', value: 'bolivia' },
          { name: 'Botswana', value: 'botswana' },
          { name: 'Brazil', value: 'brazil' },
          { name: 'Bulgaria', value: 'bulgaria' },
          { name: 'Burundi', value: 'burundi' },
          { name: 'Cambodia', value: 'cambodia' },
          { name: 'Cameroon', value: 'cameroon' },
          { name: 'Canada', value: 'canada' },
          { name: 'Chad', value: 'chad' },
          { name: 'Chile', value: 'chile' },
          { name: 'China', value: 'china' },
          { name: 'Colombia', value: 'colombia' },
          { name: 'Comoros', value: 'comoros' },
          { name: 'Congo', value: 'congo' },
          { name: 'Costa Rica', value: 'costa rica' },
          { name: 'Croatia', value: 'croatia' },
          { name: 'Cuba', value: 'cuba' },
          { name: 'Curaçao', value: 'curaçao' },
          { name: 'Cyprus', value: 'cyprus' },
          { name: 'Czechia', value: 'czechia' },
          { name: 'Denkmark', value: 'denmark' },
          { name: 'Djibouti', value: 'djibouti' },
          { name: 'Dominica', value: 'dominica' },
          { name: 'Ecuador', value: 'ecuador' },
          { name: 'Egypt', value: 'egypt' },
          { name: 'El Salvador', value: 'el salvador' },
          { name: 'Eritrea', value: 'eritrea' },
          { name: 'Estonia', value: 'estonia' },
          { name: 'Ethiopia', value: 'ethiopia' },
          { name: 'Fiji', value: 'fiji' },
          { name: 'Finland', value: 'finland' },
          { name: 'France', value: 'france' },
          { name: 'Gabon', value: 'gabon' },
          { name: 'Gambia', value: 'gambia' },
          { name: 'Georgia', value: 'georgia' },
          { name: 'Germany', value: 'germany' },
          { name: 'Ghana', value: 'ghana' },
          { name: 'Gibraltar', value: 'gibraltar' },
          { name: 'Greece', value: 'greece' },
          { name: 'Greenland', value: 'greenland' },
          { name: 'Grenada', value: 'grenada' },
          { name: 'Guadeloupe', value: 'guadeloupe' },
          { name: 'Guam', value: 'guam' },
          { name: 'Guatemala', value: 'guatemala' },
          { name: 'Guernsey', value: 'guernsey' },
          { name: 'Guinea', value: 'guinea' },
          { name: 'Guyana', value: 'guyana' },
          { name: 'Haiti', value: 'haiti' },
          { name: 'Honduras', value: 'honduras' },
          { name: 'Hong Kong', value: 'hong kong' },
          { name: 'Hungary', value: 'hungary' },
          { name: 'Iceland', value: 'iceland' },
          { name: 'India', value: 'india' },
          { name: 'Indonesia', value: 'indonesia' },
          { name: 'Iran', value: 'iran' },
          { name: 'Iraq', value: 'iraq' },
          { name: 'Ireland', value: 'ireland' },
          { name: 'Israel', value: 'israel' },
          { name: 'Italy', value: 'italy' },
          { name: 'Jaimaica', value: 'jamaica' },
          { name: 'Japan', value: 'japan' },
          { name: 'Jersey', value: 'jersey' },
          { name: 'Jordan', value: 'jordan' },
          { name: 'Kazakhstan', value: 'kazakhstan' },
          { name: 'Kenya', value: 'kenya' },
          { name: 'Kiribati', value: 'kiribati' },
          { name: 'Korea', value: 'korea' },
          { name: 'Kuwait', value: 'kuwait' },
          { name: 'Kyrgyzstan', value: 'kyrgyzstan' },
          { name: 'Latvia', value: 'latvia' },
          { name: 'Lebanon', value: 'lebanon' },
          { name: 'Lesotho', value: 'lesotho' },
          { name: 'Liberia', value: 'liberia' },
          { name: 'Libya', value: 'libya' },
          { name: 'Liechtenstein', value: 'lietchtenstein' },
          { name: 'Lithuania', value: 'lithuania' },
          { name: 'Luxembourg', value: 'luxembourg' },
          { name: 'Macao', value: 'macao' },
          { name: 'Macedonia', value: 'macedonia' },
          { name: 'Madagascar', value: 'madagascar' },
          { name: 'Malawi', value: 'malawi' },
          { name: 'Malaysia', value: 'malaysia' },
          { name: 'Maldives', value: 'maldives' },
          { name: 'Mali', value: 'mali' },
          { name: 'Malta', value: 'malta' },
          { name: 'Martinique', value: 'martinique' },
          { name: 'Mauritania', value: 'mauritania' },
          { name: 'Mauritius', value: 'mauritius' },
          { name: 'Mayotte', value: 'mayotte' },
          { name: 'Mexico', value: 'mexico' },
          { name: 'Micronesia', value: 'micronesia' },
          { name: 'Moldova', value: 'moldova' },
          { name: 'Monaco', value: 'monaco' },
          { name: 'Mongolia', value: 'mongolia' },
          { name: 'Montenegro', value: 'montenegro' },
          { name: 'Montserrat', value: 'montserrat' },
          { name: 'Morocco', value: 'morocco' },
          { name: 'Mozambique', value: 'mozambique' },
          { name: 'Myanmar', value: 'myanmar' },
          { name: 'Namibia', value: 'namibia' },
          { name: 'Nauru', value: 'nauru' },
          { name: 'Nepal', value: 'nepal' },
          { name: 'Netherlands', value: 'netherlands' },
          { name: 'New Zeland', value: 'new zeland' },
          { name: 'Nicaragua', value: 'nicaragua' },
          { name: 'Niger', value: 'niger' },
          { name: 'Nigeria', value: 'nigeria' },
          { name: 'Niue', value: 'niue' },
          { name: 'Norway', value: 'norway' },
          { name: 'Oman', value: 'oman' },
          { name: 'Pakistan', value: 'pakistan' },
          { name: 'Palau', value: 'palau' },
          { name: 'Palestine', value: 'palestine' },
          { name: 'Panama', value: 'panama' },
          { name: 'Paraguay', value: 'paraguay' },
          { name: 'Peru', value: 'peru' },
          { name: 'Philippines', value: 'philippines' },
          { name: 'Pitcairn', value: 'pitcairn' },
          { name: 'Poland', value: 'poland' },
          { name: 'Portugal', value: 'portugal' },
          { name: 'Puerto Rico', value: 'puerto rico' },
          { name: 'Qatar', value: 'qatar' },
          { name: 'Romania', value: 'romania' },
          { name: 'Russia', value: 'russian federation' },
          { name: 'Rwanda', value: 'rwanda' },
          { name: 'Samoa', value: 'samoa' },
          { name: 'San Marino', value: 'san marino' },
          { name: 'Senegal', value: 'senegal' },
          { name: 'Serbia', value: 'serbia' },
          { name: 'Seychelles', value: 'seychelles' },
          { name: 'Singapore', value: 'singapore' },
          { name: 'Slovakia', value: 'slovakia' },
          { name: 'Slovenia', value: 'slovenia' },
          { name: 'Somalia', value: 'somalia' },
          { name: 'South Africa', value: 'south africa' },
          { name: 'Spain', value: 'spain' },
          { name: 'Sri Lanka', value: 'sri lanka' },
          { name: 'Sudan', value: 'sudan' },
          { name: 'Suriname', value: 'suriname' },
          { name: 'Swaziland', value: 'swaziland' },
          { name: 'Sweden', value: 'sweden' },
          { name: 'Switzerland', value: 'switzerland' },
          { name: 'Syria', value: 'syrian arab republic' },
          { name: 'Taiwan', value: 'taiwan' },
          { name: 'Tajikistan', value: 'tajikistan' },
          { name: 'Tanzania', value: 'tanzania, united republic of' },
          { name: 'Thailand', value: 'thailand' },
          { name: 'Togo', value: 'togo' },
          { name: 'Tokelau', value: 'tokelau' },
          { name: 'Tonga', value: 'tonga' },
          { name: 'Tunisia', value: 'tunisia' },
          { name: 'Turkey', value: 'turkey' },
          { name: 'Turkmenistan', value: 'turkmenistan' },
          { name: 'Tuvalu', value: 'tuvalu' },
          { name: 'Uganda', value: 'uganda' },
          { name: 'Ukraine', value: 'ukraine' },
          { name: 'United Kingdom', value: 'united kingom' },
          { name: 'United States of America', value: 'united states' },
          { name: 'Uruguay', value: 'uruguay' },
          { name: 'Uzbekistan', value: 'uzbekistan' },
          { name: 'Vanuatu', value: 'vanuatu' },
          { name: 'Venezuela', value: 'venezuela' },
          { name: 'Yemen', value: 'yemen' },
          { name: 'Zambia', value: 'zambia' },
          { name: 'Zimbabwe', value: 'zimbabwe' }
      ],
      selectedCountry: 'argentina',
      loading: true
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtists() {
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
        .then(function (artists) {
          self.loading = false
          self.artists = artists
        })
    }
  },
  mounted() {
    this.refreshArtists()
  },
  watch: {
    selectedCountry() {
      this.refreshArtists()
    }
  }
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px

h1, h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983
</style>
