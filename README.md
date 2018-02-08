# silencio-gtm
Our stock Google Tag Manager configuration for our Silencio Wordpress theme.

https://github.com/viastudio/Silencio

## Quickstart

>The following assumes you have a Google Analytics property set up

1. Create a new Google Tag Manager (v2) container
2. Download and import https://github.com/benATvia/silencio-gtm/blob/master/silencio-gtm.json into this container (Container > Admin > Import Container)
3. Add your Google Analytics UA identifier to the config, by changing the {{Google Analytics Settings}} variable under "Variables"

Voila!

## What's Inside

Our stock configuration includes configuration to track the following:

* Basic Google Analytics pageviews
* Events from our custom VIA.Event and VIA.VirtualPageView
* Many handy events: outbound, downloand and email clicks, YouTube tracking, Scroll Depth tracking

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

### User ID tracking

If you are using DuracellTomi's Google Tag Manager plugin for Wordpress, you can enable User ID tracking under Settings > Google Tag Manager > Basic Data > Visitors > Logged in User ID. This will automatically send the user ID data needed to track User ID in Google Analytics.

You will also need to enable User ID in your Google Analytics Property.

### Other Handy Events

#### Outbound Link Clicks

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

#### YouTube

If a YouTube embed is detected on the page, we will automatically begin tracking and reporting events.

Category: 'youtube'

Action: 'play', 'pause', 0%, 25%, 50%, 75%, 90%, 100%

Label: title of video

Adapted from this article: http://www.cardinalpath.com/youtube-video-tracking-with-google-tag-manager-v2-and-universal-analytics-a-step-by-step-guide/

#### Scroll Tracking

By default, we use @robflaherty's Scroll Depth plugin (v0.9.1), which will automatically send scroll events:

Category: ScrollDistance

Action: Percentage | Pixel Depth

Label: xy% | # of pixels

Code:
http://scrolldepth.parsnip.io/

Implementation: http://andygibson.us/2013/10/track-scroll-depth-using-google-tag-manager/

Optionally, if you enable DuracellTomi's Google Tag Manager plugin option "Scroll Tracking" you will also receive:

**Scroll Percentage**

Category: Scroll Tracking

Action: Scroll

Label: xy%

**Reader Type**

Category: Scroll Tracking

Action: Reader Type

Label: reader | scanner
