# Vue.js + Unsplash Images - A Pinterest Like-Style Photo Gallery App

## Project setup
```
npm install
```

### Creating a Developer Account
Head over to https://unsplash.com/developers to create a developer's account to use the Unsplash API
```
https://unsplash.com/developers
```
Click on the “Register as a Developer” button. Only you have created your account and verified it.
Login to your account, Click on the “New Application” button. Check all the options, then click the “Accept Terms” button.
Your application you will be assigned a unique access key.
Copy the access key and paste it in the headers object of the axios get request, in App.vue file.
i.e
```javascript
    searchUnslash(topic){
        this.images = [];
        this.loading = true;
        axios.get(`https://api.unsplash.com/search/photos?query=${topic}&per_page=30`, {
            headers: {
                Authorization: "Client-ID <ENTER_YOUR_UNSPLASH_ACCESS_KEY>",
                "Accept-Version": "v1"
            }
        }).then((res) => {
            this.loading = false;
            this.images = res.data.results;
        }).catch((err) => {
            console.log(err)
            this.loading = false;
            this.images = [];
        });
    }
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).