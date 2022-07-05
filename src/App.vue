<template>
  <v-app>
    <v-app-bar app flat>
	<div class="d-flex align-center">
	Third-party Built-in Browser Detector
	</div>

	<v-spacer></v-spacer>

	<v-btn icon @click="toggleDisplayMode"><v-icon>mdi-brightness-4</v-icon></v-btn>

    </v-app-bar>

    <v-main>
		<v-card
			elevation="10"
		>
			<div
				class="d-flex justify-center align-center py-10"
			>
				<v-icon 
					v-if="isThirdPartyBuiltInBrowser"
					x-large
					color="red darken-1"
				>
					mdi-close
				</v-icon>
				<v-icon 
					v-else
					x-large
					color="green darken-1"
				>
					mdi-check
				</v-icon>
	
				<v-divider
					inset
					vertical
					class="pr-3"
				></v-divider>
	
				<v-icon
					x-large
					class="pl-3"
				>0
					mdi-{{browserType}}
				</v-icon>
				<v-icon
					x-large
					class="pl-3"
				>
					mdi-{{osType}}
				</v-icon>
			</div>
			<p class="text-caption text--secondary text-center font-italic py-2"> {{isThirdPartyBuiltInBrowser ? "已被第三方浏览器封印" : "未在第三方内置浏览器牢笼中"}}</p>
		</v-card>


		<v-card elevation="5">
			<v-card-title><v-icon left>mdi-cog</v-icon>User Agent</v-card-title>
			<v-card-text class="text-subtitle-1 font-weight-light pl-8">{{userAgent}}</v-card-text>
		</v-card>
		

		<v-footer padless>
			<v-col class="text-center" cols="12">
				{{ new Date().getFullYear() }}  |  ~HelloGwkki~
			</v-col>
		</v-footer>
    </v-main>
  </v-app>
</template>

<script>

export default {
  //name: 'App',

	data: () => ({
		userAgent: ':(',
		platform: 'owo',
		isThirdPartyBuiltInBrowser: false,
		browserType: 'help-rhombus',
		osType: 'help-rhombus'
	}),

	methods: {
		toggleDisplayMode() {
			this.$vuetify.theme.dark = !this.$vuetify.theme.dark
		}
	},

	mounted: function(){
		this.userAgent = navigator.userAgent.toLowerCase();
		if (this.userAgent.match(/MicroMessenger/i) == "micromessenger"){
			this.browserType = 'wechat';
			this.isThirdPartyBuiltInBrowser = true;
		}
		else if (this.userAgent.match(/QQ/i) == "qq"){
			this.browserType = 'qqchat';
			this.isThirdPartyBuiltInBrowser = true;
		}
		else if (this.userAgent.match(/Chrome/i) == "chrome"){
			this.browserType = "google-chrome";
		}
		else if (this.userAgent.match(/Firefox/i) == "firefox"){
			this.browserType = "firefox";
		}

		this.platform = String(navigator.platform).toLowerCase();
		if (this.platform.match(/Win/i) == "win"){
			this.osType = "microsoft-windows";
		}
		else if (this.userAgent.match(/Android/i) == "android"){
			this.osType = "android";
		}
		else if (this.platform.match(/Linux/i) == "linux"){
			this.osType = "linux";
		}
	}
};
</script>
