# silencio-gtm
Our stock Google Tag Manager configuration for our Silencio Wordpress theme.

https://github.com/viastudio/Silencio

## Quickstart

>The following assumes you have a Google Analytics property set up

1. Create a new Google Tag Manager (v2) container
2. Download and import https://github.com/benATvia/silencio-gtm/blob/master/silencio-gtm.json into this container (Container > Admin > Import Container)
3. Add your Google Analytics UA identifier to the config, by changing the {{Google Analytics UA}} variable under "Variables"

Voila!

## What's Inside

Our stock configuration includes configuration to track the following:

* Basic Google Analytics pageviews
* Events generated from the "Google Tag Manager for Wordpress" plugin (http://www.duracelltomi.com/google-tag-manager-for-wordpress/)
* Events from our custom VIA.Event and VIA.VirtualPageView

### Events Generated from "Google Tag Manager for Wordpress" plugin

* File downloads
* Scroll Tracking
* Outbound link tracking

>Note these events must be enabled in the plugin settings to be received as events in Google Analytics.

### Custom VIA.Event and VIA.VirtualPageViews Events

#### VIA.Event

If you need to convert old Universal Analytics _gaq.push calls, we have a VIA.Event that utilizes the dataLayer to push events to Google Analytics:

```
dataLayer.push({
     'event':'VIA.Event',
     'eventCategory':'Sidebar',
     'eventAction' : 'Click',
     'eventLabel' : 'Button 1'
     'eventValue' : '0.05'
     });
```

#### VIA.VirtualPageViews

Similarly, old Universal Analytics pageview calls can be converted to dataLayer pushes with VIA.VirtualPageview

```
dataLayer.push({
     'event':'VIA.VirtualPageview',
     'virtualPageURL':'/plan/contact-us/thank-you/',
     'virtualPageTitle' : 'Plan Your Visit - Contact Us - Thank You'
     });
```
