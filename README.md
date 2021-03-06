# MagicMirror² Module: Skyss
'MMM-Skyss' is a module based on the Ruter equivalent made by Cato Antonsen for displaying public transport information for the Hordaland region in Norway on a [MagicMirror²](https://magicmirror.builders/). It's using data from Skyss.no. Skyss is a registered trademark of Hordaland County Councile (Hordaland Fylkeskommune) which is not affiliated with this product. Content from Skyss APIs may be copyrighted.

![1](images/MMM-Skyss-1.png)
![2](images/MMM-Skyss-2.png) 

Current version is s1.3.0 See [changelog](CHANGELOG.md "Version history") for version history.

## Installation

Remote to your MM2-box with your terminal software and go to your MagicMirror's Module folder:
````bash
cd ~/MagicMirror/modules
````

Clone the repository:
````bash
git clone https://github.com/PabloDons/MMM-Skyss.git
````

Go to the modules folder:
````bash
cd MMM-Skyss
````

Install the dependencies:
````bash
npm install
````

Add the module to the modules array in the `config/config.js` file by adding the following section. You can change this configuration later when you see this works:
```javascript
{
	module: 'MMM-Skyss',
	header: 'Skyss',
	position: 'top_left',
	config: {
		showPlatform: true,
		maxItems: 8,
		stops: [
			{
				stopId: "placeId_011022"
			},
			{
				stopId: "placeId_011092"
			},
		]
	}
},
```

You also need an auth token. In order to retrieve one, I used a packet monitor and extracted the token from my phone's app.
You can either do the same or ask me personally for one. I am currently working on a way to generate a new token for each client

# Configuration options

These are the valid configuration options you can put inside the config array above:

Configuration option | Comment | Default 
---|---|---
stops | Array of stops. See below | Empty array
maxItems | Number of journeys to display | 5 
showHeader | Set this to true to show header above the journeys | false
showStopName | Display custom stop name for each stop. You can override the name by adding `stopName` to the stop you want to override (See below) | false
maxNameLength | Some stop names can be very long and ruin the layout of the module. Set this to how many characters you max want to display.  | Not set
showPlatform | Set this to true to get the names of the platforms. Set this to true to check the name of the platform if you need to filter  | false
humanizeTimeTreshold | If time to next journey is below this value, it will be displayed as "x minutes" instead of time | 15 
serviceReloadInterval | Refresh rate in MS for how often we call Skyss's web service. NB! Don't set it too low! | 30000 
timeReloadInterval | Refresh rate how often we check if we need to update the time in the GUI | 1000 
animationSpeed | How fast the animation changes when updating mirror - in milliseconds | 0  
fade | Set this to true to fade list from light to dark | true  
fadePoint | Start fading on 1/4th of the list | 0.25

## Stops
You have to configure at least one stop. The module is using the same stop ID's as Skyss does in it's API. I've added a json file with all the stops in Hordaland for your conveniece. You can find all the stops in [this file](https://raw.githubusercontent.com/PabloDons/MMM-Skyss/master/stops.json). Just do a search for the stop name and use the identifier.

Notice that you can only use stops, not addresses or areas.

Stop option | Comment 
---|---
stopId | Id of stop  
stopName | Override name of the stop if you know it by another name or want to keep it short. You have to enable `showStopName` in module configuration. 
<!-- platformFilter | The names of the platforms you want to see. Please temporarely enable `showPlatformName` in the module configuration to get the correct platform names before you configure this option. If these names aren't valid, nothing will be displayed. -->
<!-- timeToThere | How long time in minutes does it take for you to get to this stop? It's no point showing journeys that till go in 1 minute if it takes you 5 minutes to get there... -->

Example:
```
stops: [
	{
		stopId: "placeId_011098"
	},
	{
		stopId: "placeId_011094",
		stopName: "Mitt stopp"
	}
]

``` 
## Translations

This modules is translated to the following languages:

Language | Responsible
---|---
nb (Norwegian) | Cato Antonsen
en (English) | Cato Antonsen

If you add other languages, please make a PR or drop me a line!

# Future enhanchements

1. Generate a new auth token for each client
1. Show deviations
1. Add filter for platforms
1. Add filter for departures that are too close to make
