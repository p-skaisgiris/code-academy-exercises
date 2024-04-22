# HTMl and CSS exercises

## CSS

### Using colors

- Create 4 paragraphs and colour the text using inline CSS in different colours using:
  - CSS colour names (e.g. red, range, green, etc.); 
  - CSS RGB colours rgb (red, green, blue) or rgba (red, green, blue, alpha); 
  - CSS HEX values #rrggbb (where rr (red), gg (green) and bb (blue) are hexadecimal values between 00 and ff); 
  - CSS HSL values hsl (hue, saturation, lightness).

### Style a Basic Website:

- Create a simple HTML file with elements like heading (`<h1>`), paragraph (`<p>`), and an image (`<img>`) tag.
- Using a separate CSS file, style the following:
  - Change the font color and size of the heading. 
  - Add a background color and padding to the paragraph. 
  - Set a border and adjust the width and height of the image.

### Center an Image

- Create an HTML document with an image tag (`<img>`) displaying your favorite picture. 
- CSS to:
  - Center the image horizontally and vertically on the page.
  - Add a small border or a drop shadow to make the image stand out.

### Style a Colorful List:

- Create an unordered list (`<ul>`) with several list items (`<li>`). 
- Use CSS to:
  - Change the background color of each list item to alternate between two different colors (e.g., blue and green). Try doing this manually first by creating `even` and `odd` CSS classes.
  - Now, take a look at the [n-th child](https://developer.mozilla.org/en-US/docs/Web/CSS/:nth-child) documentation and implement this automatically, without the need to add a class to your HTML elements
  - Add a small border and some padding to each list item for better readability.

## HTML Forms

### Library Book Checkout Form

This form is used at a library for patrons to check out books.

Fields:
- Library Card Number: This is a text field where the user enters their unique library card number to identify themselves.
- Name: This is a text field where the user enters their full name.
- Book Title: This is a text field where the user enters the title of the book they are checking out.
- Author: This is a text field where the user enters the author's name (optional, as some libraries might use a barcode scanner for the book itself).
- Due Date: This is a date picker field where the user selects the date the borrowed book is due for return.
- Email Address: This is a text field where the user can enter their email address (optional, but useful for sending reminders or overdue notices).
- Phone Number: This is a text field where the user can enter their phone number (optional, another way for the library to contact them).

### Create Your Workout Routine!

Create an interactive form to help users design their personalized workout routine.

Form:
- Workout Focus (Radio Buttons):
  - Cardio (improves heart health)
  - Strength Training (builds muscle)
  - Flexibility (improves range of motion)
  - All of the Above
- Equipment Availability (Checkboxes): (Select all that apply)
  - Gym Membership 
  - Free Weights at Home 
  - Resistance Bands 
  - Yoga Mat 
  - No Equipment
- Preferred Activities (Select Tag - Multiple Choices): (Hold "Ctrl" or "Command" to select multiple options)
  - Running 
  - Swimming 
  - Biking 
  - Weight Lifting 
  - Yoga 
  - Pilates 
  - Dancing
- Experience Level (Datalist):
  - Start typing to see options:
  - Beginner 
  - Intermediate 
  - Advanced
- Upload a Sample Workout (File): (Optional)
  - Upload a .txt or .pdf file containing a sample workout routine you found online (or created yourself!).
- Submit Button

**Bonus**: use CSS to style your for form. Make the labels look nicer, adjust the font size, make the buttons look more colourful and bigger, etc.

### Create a Movie Review Website

This is an exercise to create a simple HTML form for a movie review website.

Instructions:
- Design a form using HTML that allows users to submit movie reviews. 
  - Include at least 7 fields to capture relevant information about the movie and the review. 
  - Use a variety of form elements to practice with different input types.

Here are some ideas for the form fields, but feel free to get creative and add more!

- Movie Title 
- Release Year 
- Review Title 
- Rating: Allow users to choose a rating from 1 to 5 stars.
- Review Text
- Recommend: for users to indicate if they recommend the movie.
- Genre: Allow users to select genres (e.g., Comedy, Action, Drama, etc.).
- Bonus: You can add an additional field for the user's name (text field) or email address (text field) if they want to be credited for the review.

**Bonus:** Style the form using CSS for a better user experience.