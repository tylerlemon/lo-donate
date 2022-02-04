# Luminate Online Donation Plugin

Add a 
[Luminate Online](https://www.blackbaud.com/online-marketing/luminate-online) Donation Form to any website using the Luminate Online API. 


### Table of Contents
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
    - [Basic](#basic)
    - [Advanced](#advanced)
    - [Modal vs Inline](#modal-vs-inline)
- [Options](#options)
- [License](#license)

## Prerequisites
#### API Key
In order to use the Luminate Online API, you must define an API Key for your organization's Luminate Online website. If you haven't already done so, go to Setup -> Site Options -> Open API Configuration.
#### Whitelist
For security reasons, the API and this library limit requests to a list of domains whitelisted by your organization. If you haven't already done so, go to Setup -> Site Options -> Open API Configuration, and click "Edit Javascript/Flash configuration". For the purposes of using this library, the only options you need to worry about on this page are 1. Allow JavaScript/Flash API from these domains and 2. Trust JavaScript/Flash API from these domains. Add any domains where you will use this library to these lists. As noted on the page, you can use an asterisk as a wildcard if your website has multiple subdomains, e.g. "*.myorganization.com".
#### Donation Form
The Donation API must reference a 'shadow' Donation Form on the Luminate Online web site. This shadow form is used to perform validation and to associate donations with the appropriate fundraising Campaign.

## Installation

Add the following items to the head of your page.

```
<!-- DFS CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/tylerlemon/lo-donate@v0.1.4-alpha/bundle.css">
```

```
<!-- DFS JS -->
<script src="https://cdn.jsdelivr.net/gh/tylerlemon/lo-donate@v0.1.4-alpha/bundle.js"></script>
```

## Usage

### Basic

The example below demonstrates the minimum required to install the plugin. The remaining parameters are inherited from default values.

```javascript
document.addEventListener('DOMContentLoaded', function(){
    // Create an instance of the plugin
    var form = new DFSDonationForm({
        url: 'https://secure2.convio.net/myorg/site', // Secure domain for LO Instance
        apiKey: '123456789',
        formId: '1234' // Shadow form created in LO
    });

    // Initialize
    form.init();
});
```

### Advanced

This example supports both one-time and monthly donations. Users can also define a minimum donation amount and give the option to cover the processing fee.

```javascript
document.addEventListener('DOMContentLoaded', function(){
    // Create an instance of the plugin
    var form = new DFSDonationForm({
        url: 'https://secure2.convio.net/myorg/site', // Secure domain for LO Instance
        apiKey: '123456789',
        formId: '1234' // Shadow form created in LO,
        levelSplit: [4, 4], // Define levels for [one-time, monthly]
        supportMonthly: true,
        minimumDonation: 10,
        coverFee: true,
        feeType: "percent", // "percent" or "dollar"
        feeAmount: 2,
    });

    // Initialize
    form.init();
});
```

Tribute gifts and eCards can also be adding using additional parameters. ECard and tribute fields must also be added on the shadow form. 

```javascript
document.addEventListener('DOMContentLoaded', function(){
    // Create an instance of the plugin
    var form = new DFSDonationForm({
        url: 'https://secure2.convio.net/myorg/site', // Secure domain for LO Instance
        apiKey: '123456789',
        formId: '1234', // Shadow form created in LO
        supportTribute: true,
        supportEcard: true,
        stationaryId: '4321', // One LO stationary ID is used for all notification emails
    });

    // Initialize
    form.init();
});
```

### Modal vs Inline
The plugin can be opened in a modal window with a click event or displayed inline on a page. The ```displayType``` will accept either ```"modal"``` or ```"inline"``` as a valid value. If ```"modal"``` is given a ```target``` must be defined. Alternatively, with ```"inline"``` the ```container``` option must have an element present on the page.

#### Modal
Add an element on the page with the default target selector ```[data-dfs-target]``` or define a new target

```
<button data-dfs-target>Donate Today</button>
```

#### Inline
Add an element on the page with the default container selector ```[data-dfs-container]``` or define a new container

```
<div data-dfs-container></div>
```

## Options

<table>
<tr>
<th>
Name
</th>
<th>
Type
</th>
<th>
Default
</th>
<th>
Description
</th>
</tr>
<tr>
<td>
url
</td>
<td>
string
</td>
<td>
''
</td>
<td>
Required. The secure base URL for an organization's LO instance.
</td>
</tr>
<tr>
<td>
apiKey
</td>
<td>
string
</td>
<td>
''
</td>
<td>
Required. Found in Luminate Online's site options.
</td>
</tr>
<tr>
<td>
formId
</td>
<td>
integer
</td>
<td>
''
</td>
<td>
Required.
</td>
</tr>
<tr>
<td>
primaryCountry
</td>
<td>
string
</td>
<td>
'Canada'
</td>
<td>
Default selected company for donor information. "United States" or "Canada" will impact how the "State/Province" field is sorted.
</td>
</tr>
<tr>
<td>
displayType
</td>
<td>
string
</td>
<td>
'modal'
</td>
<td>
Defines how the plugin is displayed. "modal" || "inline" are the accepted values. 
</td>
</tr>
<tr>
<td>
donationMinimum
</td>
<td>
integer
</td>
<td>
5
</td>
<td>
The minimum allowed donation. This value cannot be lower than the threshold defined in Luminate Online's site options.
</td>
</tr>
<tr>
<td>
levelSplit
</td>
<td>
array
</td>
<td>
[3, 3]
</td>
<td>
['one-time', 'monthly'] The level split controls the amount of levels are for one-time and monthly donations. This should be configured to match the level's recurring behavior.
</td>
</tr>
<tr>
<td>
supportMonthly
</td>
<td>
boolean
</td>
<td>
false
</td>
<td>
If set to false all donation levels are assumed to be one-time donations. This does not override the level's recurring behavior.
</td>
</tr>
<tr>
<td>
monthlyFirst
</td>
<td>
boolean
</td>
<td>
true
</td>
<td>
Display monthly or one-time as the default giving option.
</td>
</tr>
<tr>
<td>
supportTribute
</td>
<td>
boolean
</td>
<td>
false
</td>
<td>
Display tribute giving options. Tribute data elements must also be added to the Luminate Online form.
</td>
</tr>
<tr>
<td>
supportEcard
</td>
<td>
boolean
</td>
<td>
false
</td>
<td>
Display eCard notification options. supportEcard can only be used if supportTribute is set to true ECard data elements must also be added to the Luminate Online form.
</td>
</tr>
<tr>
<td>
stationaryId
</td>
<td>
integer
</td>
<td>
false
</td>
<td>
Required for eCard notifications. If no stationary is given, eCard support will be disabled.
</td>
</tr>
</tr>
<tr>
<td>
coverFee
</td>
<td>
boolean
</td>
<td>
false
</td>
<td>
Display checkbox for covering the processing fee.
</td>
</tr>
<tr>
<td>
feeType
</td>
<td>
string
</td>
<td>
'percent'
</td>
<td>
Define if the processing fee should be a percentage of the donation or a flat dollar amount. "percent" || "dollar" are the accepted values. 
</td>
</tr>
<tr>
<td>
feeAmount
</td>
<td>
integer
</td>
<td>
2
</td>
<td>
Define the processing fee amount in conjunction with the feeType.
</td>
</tr>
<tr>
<td>
target
</td>
<td>
string
</td>
<td>
'[data-dfs-target]'
</td>
<td>
Define a target to open a modal on click.
</td>
</tr>
<tr>
<td>
container
</td>
<td>
string
</td>
<td>
'[data-dfs-container]'
</td>
<td>
Define a container for the form be rendered in.
</td>
</tr>
</table>

## License
[MIT](https://choosealicense.com/licenses/mit/)
