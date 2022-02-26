# moneryze

**Currently only supports vault transactions, more will be added soon**

[![NPM version](https://img.shields.io/npm/v/moneryze.svg)](https://www.npmjs.com/package/moneryze)&nbsp;
[![Build Status](https://travis-ci.org/Wuon/moneryze.svg?branch=master)](https://travis-ci.org/Wuon/moneryze)&nbsp;
[![Coverage Status](https://coveralls.io/repos/github/Wuon/moneryze/badge.svg?branch=master)](https://coveralls.io/github/Wuon/moneryze?branch=master)&nbsp;
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A wrapper to access the Moneris API, forked from AlejandroEsquivel's great work (AlejandroEsquivel/moneris-js), forked from shaynair's great work (shaynair/moneris-js)

> The hope for this module is to create clean, robust, promise wrapped queries that extend just beyond payments. Shaynair's work supported generalized queries to Moneris, Alejandro's work handled the imperfect formatting. My hope is to extend and complete the wrapper, transforming the project into something easy to implement by any developer.

[Installation](#installation) |
[Usage](#usage) |
[Example](#example) |
[License](#license)

## Installation

With [npm](https://npmjs.org/):

```bash
npm install moneryze --save
```

Note: You need **an engine that supports ES6 (e.g. Babel or Node 4.0+)**.

## General Usage

**`const moneris = require('moneryze');`**

Queries the Moneris API with the information provided.

- `config`: **Required.** An object with the following fields.
  - `app_name`: Optional. If given, will add `app_name` as a prefix to receipt names.
  - `api_token`: **Required.** Your API token.
  - `store_id`: **Required.** Your store ID.
  - `crypt_type`: Optional. If given, will set the default crypt_type for all transactions. `7` by default.
  - `test`: Optional. If true, uses Moneris Test endpoints. You can get a `api_token` and `store_id` for this endpoint from Moneris's Documentation. `false` by default.

.init() must be called before any other operation, otherwise an error will be thrown

## Examples

### .init()

```bash
moneris.init({
  app_name: 'Test',
  store_id: 'store5',
  api_token: 'yesguy',
  crypt_type: '7',
  test: true,
});
```

### .resAddCC()

- `pan`: **Required.** Card number.
- `expdate`: **Required.** Expiry date of the card.

```bash
moneris.resAddCC({
  pan: '4242424242424242',
  expdate: '2011',
});
```

### .resPurchaseCC()

- `token`: **Required.** Customer's moneris token.
- `amount`: **Required.** Amount to charge.
- `description`: Optional. A short message attached to the purchase.

```bash
moneris.resPurchaseCC({
  token: 'D8WyyItuNb6mHn4biiPqAwM42',
  amount: 11.98,
  description: 'bubble tea',
});
```

### .purchase()

- `pan`: **Required.** Card number.
- `expdate`: **Required.** Expiry date of the card.
- `amount`: **Required.** Amount to charge.
- `description`: Optional. A short message attached to the purchase.

```bash
moneris.purchase({
  pan: '4242424242424242',
  expdate: '2011',
  amount: 11.98,
  description: 'bubble tea',
});
```

### .refund()

- `order_id`: **Required.** The ID of the order from the transaction.
- `txn_number`: **Required.**. The number from the transaction.
- `amount`: **Required.** Amount to refund.

```bash
moneris.refund({
  order_id: 'mvt2713618548',
  txn_number: '911464-0_10',
  amount: 11.98,
});
```

### .preauth()

- `order_id`: **Required.** The ID of the order for the preauthorization.
- `amount`: **Required.** Amount to preauthorize.
- `pan`: **Required.** Card number.
- `expdate`: **Required.** Expiry date of the card.

```bash
moneris.refund({
  order_id: 'mvt2713618548',
  amount: 11.98,
  pan: '4242424242424242',
  expdate: '2011'
});
```

### .completion()

- `order_id`: **Required.** The ID of the order for the preauthorization.
- `amount`: **Required.** Completion amount.
- `txn_number`: **Required.**. The number from the transaction.

```bash
moneris.completion({
  order_id: 'mvt2713618548',
  amount: 11.98,
  txn_number: '911464-0_10',
});
```

## License

[MIT](http://g14n.info/mit-license)

## Notes

With love and passion,

wuon
