# Fixed v.2.3 OpenDAX BaseApp UI (forked https://github.com/openware/baseapp)
## Branch named "fixed" adapted to using with Peatio v.2.4.19 and Barong v.2.4.12

1. Clone this repository.

```
git clone https://github.com/MobiDAX/baseapp.git
```

2. Goto repository's directory and switch to 'fixed' branch:

```bash
git checkout fixed
```

3. Customize it with your color and logo.

4. If you want to check your changes:

- create temporary file: /src/public/config/env.js

```js
window.env = {
    api: {
        authUrl: 'http://localhost:9002/api/v2/barong',
        tradeUrl: 'http://localhost:9002/api/v2/peatio',
        applogicUrl: 'http://localhost:9002/api/v2/applogic',
        rangerUrl: 'ws://localhost:9011/api/v2/ranger',
    },
    minutesUntilAutoLogout: '5',
    withCredentials: false,
    captcha: {
        captchaType: 'none',
        siteKey: '',
    },
    gaTrackerKey: '',
    rangerReconnectPeriod: '1',
    msAlertDisplayTime: '5000',
    incrementalOrderBook: true,
};
```

- install npm packages and start ReactApp local (using default mock-server):

```
yarn install
yarn start-mock
```

5. Create own baseapp image

```
docker build --tag <your-docker-store/your-frontend-image-name> .
docker push <your-docker-store/your-frontend-image-name>
```

6. In your Opendax (https://github.com/openware/opendax) in file /config/app.yml in section "images" change:

```
  peatio: quay.io/openware/peatio:2.4.19
  barong: quay.io/openware/barong:2.4.12
  frontend: <your-docker-store/your-frontend-image-name>
```




# OpenDAX BaseApp UI (old README)
## FREE Open-Source UI for Trading and Wallets Management

Base React application to build a trading platform interface for use with OpenDAX: https://github.com/openware/opendax
Why React? Well - it's fresh, fast, flexible, and you can do a lot of UI magic with it without reloading the pages.

You can see an example of a live application running at: https://demo.openware.com/

## Add an npm auth token for install components library

```bash
$ echo "//registry.npmjs.org/:_authToken=${NPM_AUTH_TOKEN}" > .npmrc
```

## Install dependencies

```bash
$ yarn install
$ yarn build
```

## Run in developement mode

In `<rootDir>`

```bash
$ yarn start
```

## Execute test

In `<rootDir>`

```bash
$ yarn test
```

For more options for `jest` run `yarn test --help`.

## Obfuscate

To prepare an obfuscated build, run:

```
docker build -t baseapp:obfuscated
  --build-arg BUILD_EXPIRE=1560761577000(unix epoch seconds)
  --build-arg BUILD_DOMAIN="example.com"
  -f Dockerfile-obfuscator .
```
You can find all the available build args in the `available Docker build args` section

The resulting image would be accessible by the `baseapp:obfuscated` tag.

## Available Docker build args

While building a Docker image you can pass build-dependant arguments using `--build-arg`: 
`docker build -t baseapp:latest
  --build-arg BUILD_DOMAIN="example.com" .`

| Argument                 | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| `BUILD_EXPIRE`               |  Unix Timestamp of the build expiration date in seconds |
| `BUILD_DOMAIN`               |  Domain which you'd like to use during the deployment |
| `NPM_AUTH_TOKEN` |  The authentication token of npmjs.com used to fetch private packages |

## env.js configuration explanation

In `public/config` open `env.js`


| Argument                 | Description                                                  |
| --------------------- | ------------------------------------------------------------ |
| `api`    | URLs of `barong`, `peatio`, `applogic` and `ranger` API endpoints. You can use mockserver (<https://github.com/openware/mockserver>) with default `env.js` values |
| `minutesUntilAutoLogout`                |  Autologout time in minutes  |
| `withCredentials`               |  `false` or `true` if you want to include cookies as part of the request(https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Access-Control-Allow-Credentials)   |
| `captcha - captchaType`         |  `'recaptcha'`, `'geetest'` or `'none'`   |
| `captcha - siteKey`         |  Recaptha site key   |
| `gaTrackerKey` |  Google Analytics tracker key  |
| `rangerReconnectPeriod` |  Reconnection time for the Ranger WS service in minutes    |
| `msAlertDisplayTime` |  Alert message display duration in milliseconds    |

## Available Docker build args

While building a Docker image you can pass build-dependant arguments using `--build-arg`: 
`docker build -t baseapp:latest
  --build-arg BUILD_DOMAIN="example.com" .`

| Argument       | Description                                            |
| -------------- | ------------------------------------------------------ |
| `BUILD_EXPIRE` | Unix Timestamp of the build expiration date in seconds |
| `BUILD_DOMAIN` | Domain which you'd like to use during the deployment   |

## Happy trading with OpenDAX BaseApp UI

If you have designed something beautiful with it, we would love to see it!

And if you have any comments, feedback and suggestions - we are happy to hear from you here at GitHub or at https://openware.com

