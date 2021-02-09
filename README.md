# SpaceX - Management

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run build production
- Install package NPM serve:
```
npm install -g serve
```
- Run build (only to see):
```
serve dist
```


### Lints and fixes files
```
npm run lint
```

### Details:

- First I consult the API documention on: [SpaceX API V4 Docs](https://github.com/r-spacex/SpaceX-API/tree/master/docs/v4)

- Then I import the collecions to Postman for testing the End-Points, as you can see below.

    ![Collection SpaceX](collection-spacex.png?raw=true "Title")

- With the collection imported I inspect the End-Points that are of my interest.

- I use VueJS and the plugin Vuetify to show the data on the browser, I make this choice because of the quick setup, I could use ReactJS or another.

- Then I use NPM package <b>axios</b> and <b>vue-axios</b> to consult the data from the API End-Points.

- Finally I assemble the UI in a SPA with the information.
