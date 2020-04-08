<template>
  <div class="section section-basic" id="basic-elements">
	  <h2 class="title mb-4 text-center">Découvrez votre impact personnel</h2>
	  <div class="container">

      <p class="category mb-4">Combien de fois changez vous de téléphone ?</p>
      <div class="row">
		  <div class="col-md-10">
		  	<slider v-model="sliders.simple" type="primary" class="mb-2" style="max-width: 300px" @input="onFocusOutSlider"></slider>
			<p>{{ getFirstSliderValue }}</p>
			  <div class="container" v-show="focusOutSlider">
				  <div class="row">
					  <div class="col-md-10">
						  <p>
							  Vous et {{ getPourcentPeopleBuyingSmartphone }} % de français changez de téléphone à la même fréquence<br>
							  Par an vous faites extraire {{ Math.round(70 / getSliderYear) }} matériaux différents pour construire votre smartphone<br>
							  Vous utilisez 40 000 enfants du Congo pour récupérer les matériaux pour construire la batterie de votre nouveau smartphone
						  </p>

						  <small class="text-muted">
							  source: <a href="https://fr.statista.com/statistiques/764235/media-technologie-frequence-achat-un-nouveau-smartphone-france/">Statista</a>
						  </small>
					  </div>
				  </div>
			  </div>
		  </div>
      </div>
      <p class="category">Supprimez vous vos mails régulièrement ?</p>
      <div class="row">
        <div class="col-md-10">
			<n-radio v-model="radios.radioOn" label="true">Oui</n-radio>
			<n-radio v-model="radios.radioOn" label="false">Non</n-radio>
			<div v-show="radios.radioOn === 'true'">
				oui
			</div>
			<div v-show="radios.radioOn === 'false'">
				non
			</div>
        </div>
      </div>

		  <div class="row">
			  <div class="col-ms-10">

			  </div>
		  </div>

    </div>
  </div>
</template>
<script>
import {
  Button,
  Checkbox,
  Radio,
  FormGroupInput,
  Slider,
  Switch
} from '@/components';

export default {
  components: {
    [Checkbox.name]: Checkbox,
    [Radio.name]: Radio,
    [FormGroupInput.name]: FormGroupInput,
    [Option.name]: Option,
    Slider
  },
  data() {
    return {
      radios: {
        radioOn: null,
        radioOff: '2'
      },
      focusOutSlider: false,
		timer: null,
      sliders: {
        simple: null,
        rangeSlider: [20, 60]
      }
    };
  },
	computed: {
        getFirstSliderValue() {
            let prefix = 'Je change de téléphone tout les '

			if (this.sliders.simple === null)
			    return 'Jamais'
            else if (this.sliders.simple < 10)
                return prefix + '5 ans ou plus'
			else if (this.sliders.simple > 10 && this.sliders.simple < 25)
			    return prefix + '4 ans'
			else if (this.sliders.simple > 25 && this.sliders.simple < 50)
			    return prefix + '3 ans'
			else if (this.sliders.simple > 50 && this.sliders.simple < 75)
			    return prefix + '2 ans'
			else if (this.sliders.simple > 75)
			    return prefix + 'ans'
		},
		getSliderYear() {
            if (this.sliders.simple === null)
                return 0
            else if (this.sliders.simple < 10)
                return 5
            else if (this.sliders.simple > 10 && this.sliders.simple < 25)
                return 4
            else if (this.sliders.simple > 25 && this.sliders.simple < 50)
                return 3
            else if (this.sliders.simple > 50 && this.sliders.simple < 75)
                return 2
            else if (this.sliders.simple > 75)
                return 1
		},
        getPourcentPeopleBuyingSmartphone() {
            if (this.getSliderYear === 1)
                return 7
			else if (this.getSliderYear === 2)
			    return 31
            else if (this.getSliderYear === 3 || this.getSliderYear === 4)
                return 33
            else if (this.getSliderYear === 5)
                return 15
		}
	},
	methods: {
      onFocusOutSlider() {

          if (this.timer != null) {
              clearTimeout(this.timer)
			  this.timer = null
		  }

          this.timer = setTimeout(() => {
              this.focusOutSlider = true
			  this.timer = null
          }, 1000)
	  }
	}
};
</script>
<style></style>
