# Starbucks
A Javascript interface to the (private) Starbucks ordering API


## Usage

### Example

Every method on the client returns a promise, so they can be chained together. You can order stuff, like this:

```js
const Client = require('starbucks-api');
const Bluebird = require('bluebird');

const client_id = '<YOUR_CLIENT_ID>';
const client_secret = '<YOUR_CLIENT_SECRET>';
const username = '<YOUR_USERNAME>';
const password = '<YOUR_PASSWORD>';

const starbucks = new Client(client_id, client_secret);

starbucks.authenticate(username, password).then(result => {
    return Bluebird.props({
        profile: starbucks.getProfile(),
        nearbyStores: starbucks.getNearbyStores(38.3, -0.5, 10, 4)
    }).then(result => {
        let profile = result.profile;
        let nearbyStores = result.nearbyStores;
        // Show results in console
        console.log(profile, nearbyStores);
        if(profile){
            let card = profile[0];
            console.log("Current balance for card n°" + card['cardNumber'] + ": " + card['balance'] + " " + card['balanceCurrencyCode'])
        }
    });
});
```
## License

MIT


> Antoine de Chassey