<template lang="pug">
ion-page
	ion-header(:translucent='true')
		ion-toolbar
			ion-buttons(slot='start')
				ion-menu-button
			ion-title {{ folder }}
	ion-content(:fullscreen='true')
		ion-header(collapse='condense')
			ion-toolbar
				ion-title(size='large') {{ folder }}
		#container
			h1 {{ folder }}
</template>

<script lang="ts">
import { IonButtons, IonContent, IonHeader, IonMenuButton, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { useRoute } from 'vue-router';
import { ref, computed, watch } from 'vue';

export default {
	name: 'Folder',
	components: {
		IonButtons,
		IonContent,
		IonHeader,
		IonMenuButton,
		IonPage,
		IonTitle,
		IonToolbar,
	},
	setup() {
		const route = useRoute();
		const folder = ref(route.params.id || 'Co mmunication');
		const matchedFolder = computed(() => route.params.id);
		
		watch(matchedFolder, () => {
			folder.value = matchedFolder.value as string;
		})
		
		return { folder }
	}
}
</script>

<style scoped>

		ion-title {
			font-family: 'News Cycle', sans-serif !important;
			font-weight: 300 !important;
			font-style: normal !important;
		}


ion-menu-button {
	color: var(--ion-color-primary);
}

#container {
	text-align: center;
	position: absolute;
	left: 0;
	right: 0;
	top: 50%;
	transform: translateY(-50%);
}

#container strong {
	font-size: 20px;
	line-height: 26px;
}

#container p {
	font-size: 16px;
	line-height: 22px;
	color: #8c8c8c;
	margin: 0;
}

#container a {
	text-decoration: none;
}
</style>