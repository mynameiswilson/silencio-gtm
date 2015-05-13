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
* Events from our custom VIA.Event and VIA.VirtualPageView
* Outbound, email and download click events

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

### Outbound, email and download events

#### Outbound

Any click that goes to a URL that does not have your domain name will fire an event to Google Analytics:

Category: Outbound Link Click
Action: {{element url}}
Label: {{url path}} (page on site where click occurred)

Note: You need to change the "outbound link click" trigger to test against your own domain. By default, it is set to viastudio.com

#### Email 

Any click that goes to a URL that begins with "mailto:" will fire an event to Google Analytics:

Category: Email Link Click
Action: {{element url}}
Label: {{url path}} (page on site where click occurred)

#### Download

Any click that goes to a path that matches the following Regex: \.(pdf|doc|docx|xls|xlsx|ppt|pptx|zip|rar|gz|tar)$ 
... will fire an event to Google Analytics:

Category: File Download 
Action: {{element url}}
Label: {{url path}} (page on site where click occurred)