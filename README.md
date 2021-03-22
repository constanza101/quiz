# Quizful - quiz app.
---

## Install

    $ git clone https://github.com/constanza101/quiz.git
    $ cd quiz
    $ npm install
    
    
## Start & watch

    $ npm run serve

## Simple build for production

    $ npm run build

## Description of the project: 

This front-end project is developed in VUE.js, using Vuetify for styling and responsive purposes.

**1. Home:

    Constist of: 
        - A form, validated using vuetify form validation with rules for each field.
        - Saves user name to localstorage so that it can be used at the end when displaying the results.
        - There is a loading on the "select" input, to wait for the response of the api where we get the items from. 
        - This input select is disabled if there are no items to list.
        - Navigates to next view using vue router.

**2. Quiz view: 



