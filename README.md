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

This example supports both one-time and sustaining donations. Users can also define a minimum donation amount and give the option to cover the processing fee.

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
        formId: '1234' // Shadow form created in LO,
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

## Options

<table>
<tr>
<td>
Here
</td>
</tr>
</table>
  url: '',
  apiKey: '',
  formId: '',
  primaryCountry: 'Canada',
  locale: 'en_CA',
  displayType: "modal",
  donationMinimum: 5,
  levelSplit: [3, 3],
  supportMonthly: false,
  monthlyFirst: true,
  supportTribute: false,
  supportEcard: false,
  stationaryId: '',
  supportDonor: false,
  minimumDonation: 5,
  coverFee: false,
  feeType: "percent",
  feeAmount: 2,
  feeLabel: "I would like to help offset the transaction costs of my donation",
  pageTitles: ["Donate", "Tribute", "eCard", "Billing", "Donor", "Payment"],
  givingOptions: ["Give once", "Give monthly"],
  tributeLabel: "Give in honor or in memory",
  sameAsLabel: "Use for donor information",
  nextButton: "Continue",
  backButton: "Back",
  submitButton: "Process",
  thankYou: "<h3>Thank you!</h3><p>Thank you very much for your donation.</p><p>We are deeply grateful for your generosity and support of our efforts. Your gift has made a difference and enabled us to provide vital services to the community we serve. We count on you and people like you to ensure that we can continue providing these services.</p>",
  headline: "Donate Today",
  bodyText: "Support a great cause.",
  labels: {},
  target: "",
  container: "",
  reminder: true

## License
[MIT](https://choosealicense.com/licenses/mit/)
