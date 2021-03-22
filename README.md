# Quizful - quiz app.
---
## Preview on Github Pages: 
https://constanza101.github.io/quiz/
###**NOTE: You will need to click on the printful logo on the top left side corner to go to the home page**
    
    
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

**1. Home:**

    Constist of: 
        - A form, validated using vuetify form validation with rules for each field.
        - Getting questions and answers with axios.
        - There is a loading on the "select" input, to wait for the response of the api where we get the items from. 
        - This input select is disabled if there are no items to list.
        - Saves user name to localstorage so that it can be used at the end when displaying the results.
        - VUE Router: used to navigate between views, if we try to navigate to unexisting route, it redirects to 'home'.
        - When clicking on the button, if the validation is correct, it navigates to next view using vue router.

**2. Quiz view:**

    Constist of: 
        - Loading bar which waits for the data to be fetched.
        - Getting questions and answers with axios.
        - To display the questions I have used tabs for nice simple transitions. 
        - The questions are showed in clickable components/buttons, which are responsive as required: 2 columns for big devices, one column for small devices.
        - Progress bar that shows the percentage of the questions replied as we complete the quiz - color of the bar changes accordingly as it progresses (using printful logo colors).
        - After answering the last question the user can see a button to be used to get the final results.

**3. Results view:** 
    
        NOTE: to make the excercise more interesting, I have not used the VUE router again to navigate to another route/view, instead I thought it could be better  to use a fullscreen dialog component, which appears with a bottom to top transition.
        - The results are fetched by concatenating the quiz id and all the answers id, and sending it as a GET request to the given point end using axios.
        - If the results are more than 70% positive, you will read a "Congratulations" message, if the correct answers are less than that, you will read a "try again" message.
        
        
 **4.BONUS: For extra information, as I have not had the chance to reuse components in this project, I have attached a link to a previous project where I make use of reusable components and a geolocalization library to make a mars rover game. Thank you for reading  :)**
     
     - Use the app:  https://constanza101.github.io/vue-leaflet-mars-rover/
     - Watch the code: https://github.com/constanza101/vue-leaflet-mars-rover
   


