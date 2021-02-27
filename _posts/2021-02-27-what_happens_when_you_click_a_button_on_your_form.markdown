---
layout: post
title:      "What happens when you click a button on your form:"
date:       2021-02-27 11:30:55 -0500
permalink:  what_happens_when_you_click_a_button_on_your_form
---


Here is what happens when you click a button on your form :


In my project, Music Enrollments App,  when the User clicks  button "Add New Enrollment" 


* First, the browser sends a **GET**request to the server.,http://127.0.0.1:3000/enrollments/new

* Then, Rails, gets the request and follows what method was listed (get, delete, post, etc) and tries to match it with the appropriate  path helper **new_enrollment_path**  

* Once it finds the correct route,**/enrollments/new** it maps to the appropriate method in the controller action and calls on that , **enrollments#new**  and method **def new**

* From there, it finds the associated view page(index, edit, show , and new) with that method to display the results to the user. **app/models/enrollment.rb /new.html.erb**  displays the **Add New Enrollment Form** to the user.


The controller action will render a template with the same name as the action itself. In other words, you only need to call render explicitly when the view template you want doesn’t match the action you’re rendering it from. In my application , I chose to rely on Rails magic to render the view **enrollments / new.html.erb**  instead of calling it explicitly **render  :new**

This last step occurs explicitly when you call render or redirect_to, or implicitly if you leave it out.


```
Helper     =====     new_enrollment_path 
HTTP Verb  ====   GET  
Path  ====     /enrollments/new(.:format)	          
Controller Action ==== enrollments#new


app/controllers/enrollments_controller.rb

def new
    if params[:instrument_id]
      @instrument = current_user.instruments.find_by(id: params[:enrollment_id])
      @enrollment = current_user.enrollments.build(instrument_id: params[:instrument_id])
    else
      @enrollment = current_user.enrollments.build
    end
  end
```

To find the routes Run rails routes or go to localhost:3000/rails/info/routes to see all routes your application is configured to.


In summary, Rails tries to map each controller action directly to a template. However, with actions like create, we don't want a view template –– all we want is for the action to communicate with the database and then redirect to a different page.

* The new action in the controller simply renders the new form
* The create action is what actually handles the process of inserting the form data into the database
* The edit action will handle rendering the edit form
* The update action will be the method that updates the database record itself.



















