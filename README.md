## Commerce.js Unnecessary Storefront 🎉

[![Join Us on Slack](https://github.com/chec/example-unnecessary-storefront/blob/master/src/assets/demo.gif)](http://slack.commercejs.com)

### Notice: Due to the expermental/one-off nature of this example storefront we cannot provide any code support and this repo is *not* maintained.
I started this storefront during one of our hack days @ Commerce.js (Commercejs.com)  to get designers & developers creative juices flowing around what can be done and experimented with at the checkout. 

This store is fully functional, you can switch out the API keys and start using this store in the wild.

This storefront was developeed ontop of our Commmerce.js Vuejs Boilerplate (https://github.com/chec/commercejs-vuejs-boilerplate). 

Uses:
- Vue.js
- Tailwind
- Tilt.js
- Confetti.js
- Commerce.js

## Installation

### Download

Clone the git repo into the folder of your choice - `git clone https://github.com/chec/example-unnecessary-storefront.git`

Alternatively, you can [download](https://github.com/chec/example-unnecessary-storefront/archive/master.zip) the project as a zip file to your computer.

### Project setup

Simply run `npm install` or `yarn install` if you use [Yarn Package Manager](https://yarnpkg.com/) from the root of your project folder. This will install all the necessary packages required to run the boilerplate. 

### Copy example env and add Chec credentials

This demo ships with an example.env file that you will need to copy and fill with your Commerce.js credentials.   

First create a copy of the example.env file named .env in the root of your project.  You can do this by running cp example.env .env in the root folder.  The .env will look something like this:

```
NODE_ENV=local
VUE_APP_CHEC_PUBLIC_KEY={YOUR_API_KEY}
VUE_APP_CHEC_API_URL=https://api.chec.io`
```

Add in your Commerce.js public API key which can be found in the developer's settings of the [dashboard](https://dashboard.chec.io/settings/developer).

## Working with the boilerplate
 
### Compile and hot-reload for development

To aid in building your site, this boilerplate ships with a development environment which supports hot-reload on save. Run  `npm run serve` or `yarn serve` from the root of the project. After it has compiled, you will be able to view the boilerplate in your browser by visiting `http://localhost:8080/#/`.


### Compiles and minifies for production

When you are ready to ship your project, simply run `npm run build` or `yarn build` from the root of your project. This will create a production ready version of your project.


### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


### Whats next?

At this point you should have the project fully up and running ready for you to add your theme or custom integrations. We look forward to seeing what you come up with!

## Additional Resources

### Join us on Slack

Join us on Slack with other eCommerce developers and designers. 

[![Join Us on Slack](https://github.com/chec/example-unnecessary-storefront/blob/master/src/assets/slackButton.png)](http://slack.commercejs.com)


### Documentation
[Commerce.js SDK Docs](https://commercejs.com/docs/).  
[Commerce.js API Docs](https://commercejs.com/docs/api/#introduction).  

