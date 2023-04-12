[![Netlify Status](https://api.netlify.com/api/v1/badges/781e6c88-32f4-45d2-add3-7d3757661a7a/deploy-status)](https://app.netlify.com/sites/alt-gpt/deploys)

# Alt-GPT
Multi-model and multi-vendor playground for developing ChatGPT plugins (for OAI and other LLMs).  
Inspired by the paper of [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401).

![alt-gpt-demo](https://user-images.githubusercontent.com/246724/231473145-2ead9902-fc46-4de4-b71e-a0021a6e973c.gif)

<!-- <img width="1166" alt="image" src="https://user-images.githubusercontent.com/246724/228156015-62950718-9062-4de0-80ae-02e039980a00.png"> -->

## Features:
- 🌟 Plugins: Support AI plugins, discover and use and combine plugins and develop locally your new ones! 
- BYOK: Bring-your-own-key. Soon: Use API-keys from multiple vendors.
- Privacy: All logic and network requests are on client-side, including usage of your API keys, no keys send to any server other than the LLM provider.
- Local Persistance: Messages and settings are saved in locally on your device's LocalStorage

## Caveats:
1. No support for auth-based plugins yet, though, you can specify in the prompt to use an API key in the HTTP request.

## How it works:
### Without plugins: 
When performing completion without any plugins selected, your API key is used directly with the API, via HTTP request, of the relevant LLM vendor (OpenAI for example). No other backend services involved.

### With Plugins:
When selecting one or more plugins, our IntentSDK attempts to classify the intention of the user to picks up one or more plugins and defines how each plugin will be used. Then we fetch the OpenAPI definition of the plugin and IntentSDK dynamically figures out how to use the plugin's API. Then it executes an HTTP call to the API's server, though, if the plugin is marked as CORS-protected (meaning the service owner did not allow HTTP calls from any website), we'll funnel the call through a simple proxy server to overcome this. You can start your own local instance of this proxy. Finally, all the information collection as an augmented context and a final prompt combining user's initial prompt + plugin's generated context and sending to LLM for final completion. The operation of plugin augmented retrieval might be chained if intended.

### Flow:
v0.1 (current):
<img width="962" alt="image" src="https://user-images.githubusercontent.com/246724/231468275-57c70ada-d9a3-4e0f-ad69-90395d821794.png">

<details>
  	<summary>v0.0 (obsolete):</summary>
	<img width="750" alt="image" src="https://user-images.githubusercontent.com/246724/228149571-d2059e02-78d1-4724-8be8-8513feddbd2f.png">
</details>

## Creating new API keys
It is recommended to create a dedicated key so it could be revoked easily later.
- **OpenAI**: Create new api key [here](https://platform.openai.com/account/api-keys)
- **cohere**: [TBD]
- **Anthropic**: [TBD]
- **AI21**: [TBD]


## Develop
### Setup
1. Clone locally
1. Run `$ yarn install`

### Start web:
1. Run `$ yarn watch`
2. Open browser on `http://0.0.0.0:3010/`

### Optional: Start plugin-executer service:
1. Run `$ cd functions && yarn serve`
2. Set in your browser devtools `localStorage.isLocal = true`, to let the FE request your local function.


## Contribute

Contributions welcome! Read the [contribution guidelines](CONTRIBUTING.md) first and submit a Pull Request after Fork this repository.

## Contact
Please use GitHub [Issues](https://github.com/Feedox/alt-gpt/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc) to contact us.

