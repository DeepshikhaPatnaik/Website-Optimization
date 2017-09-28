## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository and inspect the code.

### Getting started

#### Part 1: Optimize PageSpeed Insights score for index.html

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to the top-level of your project directory to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ./ngrok http 8080
  ```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! Optional: [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

#### Part 2: Optimize Frames per Second in pizza.html

To optimize views/pizza.html, you will need to modify views/js/main.js until your frames per second rate is 60 fps or higher. You will find instructive comments in main.js.

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>



# Steps to view the website
- The folder consists of two directories named src and dist.
- Open the dist folder. It contains the optimized files and images.
- In the web browser (eg google chrome) press ctrl + O and select the index.html file from the dist directory.
- This loads the website(portfolio). The links on the portfolio redirects you to other pages providing information regarding the same.


# Optimizations

## Optimizations in index.html
- Added the async attribute to the javascript file analytics.js.
- Added the async attribute to the javascript file perfmatters.js.
- For non-render blocking of the CSS, added media type print (media="print") to print.css.
- Compressed all the images.
- Removed the google web font.
-CSS styles are inlined.

## Optimizations in views/js/main.js
- randomPizzas variable was used instead of document.querySelectorAll(".randomPizzaContainer") to reduce code repeatability.
- Changes made to changePizzaSizes() function. It caused forced synchronous layout as the layout and the style was recalculated repeatedly by the loop.
- The layout property was removed as it was unnecessary and caused FSL. The value for the 'newwidth' is taken from the switch case and randomPizzas is calculated to set the width of the pizza when the slider is moved.
- pizzasDiv was moved out of the loop as it was not required inside the loop and caused extra work by accesing the DOM again and again.
- The updatePositions() function was refactored. The loop for the layout calculation and style calculations caused forced synchronous layout.
- The images size were Compressed and greatly reduced to improve performance.
- In the switch case, in the function changeSliderLabel() the document.querySelector("#pizzaSize") was replaced by document.getElementById("pizzaSize").
- In the fucntion changePizzaSizes() document.querySelectorAll(".randomPizzaContainer") was replaced by document.getElementsByClassName("randomPizzaContainer")
- In the function changePizzaSizes() save array length, which is part of the condition statement, in a local variable i.e randomPizzasLength, so the array's length property is not accessed to check its value at each iteration. (i.e. more efficiency).
- In line 523, declaring the elem variable (var elem;) in the initialisation of the for-loop will prevent it from being created every time the loop is executed.
- The DOM call is moved outside the for statement (in line 524) and saving it into a local variable(movingPizzas), which can be used inside the loop.

## Optimizations in views/css/style.css
- Added transform: translateZ(0) and backface-visibility: hidden to the class .mover to improve site performance.
