# vue-ticket

Hello, this is a Ticket Form I created using Vue.js.

I started by first reading the documents from the Vue.js site:

> https://vuejs.org/guide/introduction.html

Make sure you have Node.js installed!

> https://nodejs.org/en

## Project setup

First let's install the Vue CLI. Open a terminal/powershell in a folder (I am using npm).

```
npm install -g @vue/cli
vue --version
vue create vue-ticket
```

There will be further options through the CLI, but I defaulted to `[Vue 3] babel, eslint`.

Once the project is created, `cd` in the folder directory and enter the following commands:

```
npm install
npm run serve
```

And we are ready to go!

## Ticket Form

The ticket form allows users to create a ticket will the following information:
Submission Requirements:

1. **Category** should be a dropdown menu with the following options:
   • Hardware, Software, Network, In-Processing
2. **Type** should be a dropdown menu but will change depending on the Category
   selection.
3. **Subject** should be an input field
4. **Description** should be an input field
5. **Tickets Files & Documents** should be a button that adds a pretend file named
   ‘nameoTileattached.ext’ with a file number after it so that when you press it multiple
   times, it will increment (i.e. nameoTileattached1.ext, nameoTileattached1.ext, etc).
6. A **Cancel** button that should clear the form completely
7. **Submit** button should submit all the information and display the Ticket Details page
   with all the information you used in the previous form.

Overall, it was a greate learning experience of using a new framework.
