<template>
    <div>
        <h2>{{ name }}</h2>
        <ul class="list-group">
            <li class="list-group-item">{{ country.id}}</li>
            <li class="list-group-item">{{ country.name}}</li>
            <li class="list-group-item">{{ country.capital}}</li>
            <li class="list-group-item">
                <img :src="getImgUrl(country.img)"
                     :alt="country.img"
                     class="img-fluid">
            </li>
            <li class="list-group-item">{{ country.details}}</li>
            <li class="list-group-item" v-if="isExpensive">
                <span class="badge badge-danger badge-pill">Expensive!</span>
            </li>
            <li class="list-group-item" v-if="isOnSale">
                <span class="badge badge-warning badge-pill">On Sale!</span>
            </li>
        </ul>
    </div>
</template>

<script>
	export default {
		name: "CountryDetail",
		props: {
			// example props, including validation types
			country: {
				type: Object,
				required: true
			},
			name: {
				type:
				String, required: true,
			},
            id:{
				type: Number,
                required:true,
                validator:function (value) {
					// validator function is executed *before* component is created
                    return [1, 2, 3, 4, 5, 6].includes(value)
				}
            }
		},
		methods: {
			getImgUrl(img) {
				console.log(img);
				return require('../assets/countries/' + img);
			}
		}
		,
		computed: {
			isExpensive() {
				return this.country.cost > 4000;
			}
			,
			isOnSale() {
				return this.country.cost < 1000;
			}
		}
	}
</script>

<style scoped>

</style>
