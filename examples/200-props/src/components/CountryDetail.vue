<template>
    <div>
        <h2>{{ country.name }}</h2>
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
		// Props are like a public 'API' for the component
        // Option 1. Props as a named array:
		props: ['country'],
        // Option 2. Extended props: as object notation. Extra options:
		// props: {
		// 	country: {
		// 		type: Object,
		// 		required: false,
		// 		default() {
		// 			return {
		// 				id: -1,
		// 				name: 'Unknown',
		// 				capital: 'Unknown',
		// 				img: '',
		// 				details: '',
		// 				cost: -1
		// 			}
		// 		}
		// 	}
		// },
		beforeUpdate() {
			console.log('Component updated!');
		},
		methods: {
			getImgUrl(img) {
				if (img) {
					console.log(img);
					return require('../assets/countries/' + img);
				}
			}
		},
		computed: {
			isExpensive() {
				return this.country.cost > 4000;
			},
			isOnSale() {
				return this.country.cost < 1000;
			}
		}
	}
</script>
