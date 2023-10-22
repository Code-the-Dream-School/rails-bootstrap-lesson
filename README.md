# Specifications for the Bootstrap Lesson

To create attractive web applications, it is necessary to apply styling. You have taken a previous course on HTML and CSS.  Bootstrap is a commonly used library of CSS styles that ease the creation of attractive applications.  In this lesson, you will use Bootstrap classes to style the application you have created. This lesson builds on the previous ones. You will use the same github repository, R7-validations, but for this lesson, you should create a new branch called bootstrap. Make sure that the full-assignment branch is active when you create the bootstrap branch, so that your work adds to what you did before.

The specifications for the lesson are below.  There are instructions for each part of the specification.  In addition, please review this site: [https://www.w3schools.com/bootstrap5/](https://www.google.com/url?q=https://www.w3schools.com/bootstrap5/&sa=D&source=editors&ust=1697683383982154&usg=AOvVaw1UlAU7u8TcRbo-WQUPtTgQ) .  It gives a tutorial on the use of Bootstrap.  Also, refer to this site: [https://getbootstrap.com/](https://www.google.com/url?q=https://getbootstrap.com/&sa=D&source=editors&ust=1697683383982593&usg=AOvVaw2wrGMB1cWsq0VuHTpUkVMZ) .  It includes complete documentation on the use of Bootstrap.

## Here is the specification:

1.  Install and configure Bootstrap on your Rails application.  Then run the server to verify that the appearance has changed.
2.  Change the background to a light color.
3.  Create a banner in your layout, with a title and text.
4.  Add an image to your configuration, and make it the background image for your banner.
5.  Add a font to your configuration, and make it the font for your banner.
6.  Add a navigation bar below the banner, with pulldowns for Customers and Orders.  The Customer pulldown should have the choices Customer List and New Customer.  Similarly, the Orders pulldown should have the choices Order List and New Orders.
7.  Add Bootstrap classes to the links and buttons within the Customers index view, so that all appear as buttons.  Optionally, change all the other links and buttons within the application to have the same style.
8.  Change the Orders index view.  Each Order should appear as a card within a grid.  The grid should be responsive, in that if the browser window is made too narrow, the cards should stack.  Each card should have as a title the product name and content that includes the customer name, the product count, and edit and delete buttons.  Each card should have a border, and there should be margins to each side and above the card, and of course the edit and delete buttons should work.
9.  Add Bootstrap alert divs to the layout.  If these are shown, they should appear below the banner and above the navigation bar.  There should be a danger one for a flash alert (if it is present) and a success one for a flash notice (if it is present.)
10.  Review the instructions on how to change the “are you sure” message for delete operations into a Bootstrap modal window. Optionally, complete those instructions.
11.   Optionally, make any other changes you like that might make the application attractive.

Step 1: Install and configure Bootstrap

1.  Run `bin/bundle add bootstrap`
2.  Rename `app/assets/stylesheets/application.css` to `application.scss`.  Then add the line `@import "bootstrap"`
3.  Edit `app/assets/javascript/application.cs` and add these lines:
    import "popper"
    import “bootstrap”
4.  Edit `config/importmap.rb` and add these lines:
    pin "popper", to: 'popper.js', preload: true
    pin "bootstrap", to: 'bootstrap.min.js', preload: true
5.  Add the following line to `config\initializers\assets.rb`:
    Rails.application.config.assets.precompile += %w( bootstrap.min.js popper.js)

Then run the server, or restart it if it is already running.  Verify that the appearance of the application has changed.  Note – the precompile step does cause your application to start slowly.  You should see something like this:

Step 2: Changing the background color

Bootstrap documents variables that you can set within your CSS to affect the color.  At the moment we will just use one of these.  Add these lines to your app/assets/stylesheets/application.css: :root {

   --bs-body-bg: #e7a3f0;

 }

This value is for light purple, but you can choose any light color you like. Also,, change the app/views/layouts/application.html.erb file to add a div with class “container-fluid”.  The yield statement should be inside the div.  This makes your application responsive to window sizes.  Then refresh your browser to check that the color has changed.

Step 3: The banner is done as is described at the W3schools Bootstrap Jumbotron link.  The jumbotron is no longer a Bootstrap class, but you can do the equivalent.  You can use the example from W3schools, but use your own title and text.  Refresh your browser page and verify that the banner is there.

Step 4: Find an image (jpg, gif, or png), and store it in app/assets/images.  Then, in your application.scss, create a class .banner-background as follows:

  .banner-background {

    background-image: url('s-l1600.jpg');

    background-size: cover;

  }

Then refresh the page and verify that the image shows in the banner.

Step 5: Create the directory app/assets/fonts.  Find a font.  There are free ones on the net.  Store it in app/assets/fonts.  You will typically have to unpack it from a zip file.  You should delete the zip file, and you will typically be left with a tff file or something like that.  Then, edit config/application.rb, and within the class Application section, add the line config.assets.paths << Rails.root.join('app', 'assets', 'fonts').  Then restart the server, so that the fonts directory is added to the asset pipeline.  After that, you need to add the following lines to your application.scss:

@font-face {

    font-family: 'Canterbury';

    src: url('Canterbury.ttf');

 }

Except that you give it a family name and file name corresponding to the font you installed.  This stanza should be added above .banner-background style class.  Then change the .banner-background class to add the line font-family: 'Canterbury'; Except that you need to use the name of the font-family you used.  Refresh your browser page to verify that the font shows.

Step 6. Add a navigation bar.  This should be in your layout, within the main div, below the banner but above the yield statement.  You can copy the one from the W3schools Bootstrap tutorial, modifying it as you like.  The list entries in this bar should be dropdowns, and they should have the choices described in the spec, configured with links that work.  You can copy the dropdown example from W3schools, except they make it a button element that is styled as a button.  I think that looks ugly.  You could instead make it a paragraph element and add the ms-3 class so that it is appropriately spaced.  Then refresh the page to verify that the navigation bar shows.  Verify also that each of the dropdown options works.  Note: Sometimes there is a problem that the dropdowns don’t work, because the required Popper JavaScript somehow didn’t get set up right.  If this is the issue, take a look at the page using your browser developer tools to see if you can tell why, and also check that you did all the parts of Step 1.  Contact a mentor if it still doesn’t work.

Step 7. Here you configure the links and buttons in the Customer index view to have the same appearance.  The classes you want are “btn btn-primary”.  You change the link\_to and button\_to statements to add class: “btn btn-primary”.  Then check to see that it looks right.  Optionally, you can change the other buttons and links in the application to match.  You don’t want to set the style of all buttons and links in your application.scss, because then the links in the navigation bar will look ugly.  Also, change the wording on the buttons as you like.  

A tip here: we do not want a button that says Destroy.  We are not trying to destroy a customer, only to delete a record.  Software developers have a bad habit of using the wrong words.  For example, a medical monitoring application, in the event of network problems, would put up a message that said “Client died”.  Doctors found this to be alarming.

Step 8.  You want a responsive grid of cards for your Order index view.  The outer div should have the classes “container-fluid  row”.  Inside this you have a loop for each of the orders.  First you set up a responsive grid column, by creating a div with class “col-sm”.  This causes the cards to stack if the screen window is too narrow. Then you create a card for the order. That is a div with the attributes class="card border border-2 border-success p-1 mt-3" style="width: 18rem;".  This creates fixed width cards with borders.  The border-success class gives the borders a Bootstrap color, in this case the $success color.  The p-1 class causes the cards to be separated with gutters.  The mt-3 class puts a margin at the top of each card, which makes them look ok when they are stacked, if the window is not wide enough.  Now, inside this card, you want at least two divs.  The first one should have class “card-header”, and the second should have class “card-body”.  You can put appropriate stuff in each as you choose, but be sure that you include the order product name, the order product count, the order customer full name, and edit and delete buttons, and the edit and delete buttons should work.  You can play with the various options here to get an appearance you like.  Then, in your browser, select the Order List view.  Check that it looks ok.  Check that it is responsive if you shrink your browser width.  Check that the buttons work.

Step 9.  In the previous lesson, you put a red alert paragraph in the layout to handle the error that occurs if the user attempts to get an order or customer that doesn’t exist, for example by going to /customers/999.  Change this so that if the flash\[:alert\] has a value, a Bootstrap danger alert is shown.  Also, Rails is automatically creating a flash\[:notice\] to display if an entry is created or updated.  Add code to the layout to display a Bootstrap success alert in this case.  The show views for Order and Customer have green paragraphs at the top that display the notice.  Take those out.  Then test to see that the alerts work, for example by trying /customers/999 or by creating a new order.

Step 11.  This is the optional step to use a modal window for the “Are you sure?” message.  You don’t have to do this, because it’s a little complicated, but be sure you understand how to do modal windows.  Here are the steps.

1.  Change the button for delete so that instead of triggering the “Are you sure?” prompt followed by a delete, it looks like this instead: <button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#myModal" data-id=<%= order.id %> >  This is a little different from the example at W3Schools, in that we have to pass the order.id (or customer.id) to the modal.  It can also be useful (see below) to pass other data, such as the customer name, the product name, and the product count.
2.  Next, create the modal form itself.  This should be a partial that you use wherever you intend to do a delete.  It should be an erb file.  You would create app/views/orders/\_deleteModal.html.erb, for example, and you would render it in the Orders index and show views.
3.  You can do various things in the form.  For example, you could collect additional information from the user, maybe a password to make sure they are authorized to do a delete, or whatever you like.  But the form has to have a submit button for the operation to proceed, and another button that is not a submit button to dismiss the dialog.  In our case, these would be Delete and Cancel, and the Delete might have btn-danger.  The Delete button would have type “submit”, the Cancel button would have type “button”, and both would have an attribute data-bs-dismiss="modal" so that the modal gets dismissed.  There is also a third button in the header for the x that dismisses the modal.
4.  A problem with the modal example at W3Schools is that the example does not have a form.  We are going to put a form in.  Actually it is our old delete button, which is a form that looks like a button.
5.  Another problem is that the W3Schools example does not explain how to pass data to the modal.  We have to attach it to the button that opens the modal, and then we use JavaScript to retrieve it from the button.  Clearly this is necessary if the right customer or order record is to be deleted.
6.  We can also give a nice message, more than just “Are you sure?”.  It might say, “Are you sure you want to delete the order from Frank Smith for 50 chairs?”  In order to do that, though, we have to attach more data to the button that triggers the modal.  For example, data-customer=”Frank Smith”, data-product-name =”chair”, and data-product-count=”50”.  Then, we use JavaScript to retrieve that data from the button and to display it in the modal.
7.  So, here’s an example of such a modal:

<div class\="modal" id\="myModal"\>

  <div class\="modal-dialog"\>

    <div class\="modal-content"\>

      <!-- Modal Header -->

      <div class\="modal-header"\>

        <h4 class\="modal-title"\>Are you sure?</h4\>

        <button type\="button" class\="btn-close" data-bs-dismiss\="modal"\></button\>

      </div\>

      <!-- Modal body -->

      <div class\="modal-body"\>

       <p\>Are you sure you want to delete the order from <span id\="customerName"\></span\>

        for <span id\="productCount"\></span\>

        of our <span id\="productName"\></span\> product?</p\>

      </div\>

      <!-- Modal footer -->

      <div class\="modal-footer"\>

      <%= button\_to("Delete", nil, method: :delete, class: "btn btn-danger",

      data: { "bs-dismiss" => "modal" }, form: {id: "doDelete"})  %>

<button type\="button", class\="btn btn-primary" data-bs-dismiss\="modal"\>Cancel</button\>       

      </div\>

    </div\>

  </div\>

</div\>

<script\>

document.addEventListener("DOMContentLoaded", () \=> {

const myModal = document.getElementById("myModal")

myModal.addEventListener("show.bs.modal", (e) \=> {

const triggerButton = e.relatedTarget

const customerName = document.getElementById("customerName")

const productName = document.getElementById("productName")

const productCount = document.getElementById("productCount");

const doDelete = document.getElementById("doDelete")

customerName.textContent = triggerButton.getAttribute("data-customer")

productName.textContent = triggerButton.getAttribute("data-productname")

productCount.textContent = triggerButton.getAttribute("data-productcount")

doDelete.action = ("/orders/" + triggerButton.getAttribute("data-id"))

})

})

</script\>
