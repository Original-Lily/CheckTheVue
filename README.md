# CheckTheVue

Check the Vue is a weather application I made utilising open weather map API and Open Ai API to generate images of the current weather in verified locations throughout the world. In its current state it utilizes web requests however in future I plan for this to be held within a docker image to generate its own images server side, saving time and money.

## Installation & Setup

To install and run CheckTheVue yourself, you need to setup VueJS as well as create your own API keys for [Open Weather Map](https://openweathermap.org/api) & [Open Ai API](https://https://openai.com/) and input them into the designated code below.

1. Clone the repository:

   ```
   git clone https://github.com/Original-Lily/CheckTheVue.git
   ```

2. Navigate to the project directory:

   ```
   cd CheckTheVue
   ```

3. Input the API keys on line 31 & 32 in the file:

   ```
   cd src/components/HelloWorld.vue
   ```
   Note: the boolean value "dangerouslyAllowBrowser" is to be used exclusively and only in development friendly environments
   
   ```
   line 30# const openai = new OpenAI({ apiKey: 'YOUR KEY HERE', dangerouslyAllowBrowser: true });
   line 31# const openweathermapApiKey = 'YOUR KEY HERE';
   ```

5. Run CheckTheVue:

   ```
   cd CheckTheVue
   npm run serve
   ```

## Usage

Simply input the city of your choice in the box on the right & it will give you the necessary information below; a few seconds later so will the image, provided you setup the API keys correctly.

When ran locally, it costs roughtly £0.02 for every image generated, with the billing information configured with the weather info being recieved pretty much for free.

## TODO

As mentioned before I plan for this to become an online service, however right now there is no way for me to reliably host this without it costing a fortune in API requests, I have placed this project on the backburner so I may continue with others. On a later date I intent to update the system being used to generate imaged using docker, however you are more than welcome to do so yourself should you wish!
