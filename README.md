# Fixed v.2.3 OpenDAX BaseApp UI (forked https://github.com/openware/baseapp)
## Branch named "mobidax" adapted to using with Peatio v.2.4.19 and Barong v.2.4.12

1. Clone this repository.

```
git clone https://github.com/MobiDAX/baseapp.git
```

2. Goto repository's directory and switch to 'mobidax' branch:

```bash
git checkout mobidax
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