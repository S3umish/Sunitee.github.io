---
layout: post
title:      "What triggers model validations in Rails"
date:       2021-02-27 11:29:56 -0500
permalink:  what_triggers_model_validations_in_rails
---


Model-level validations are the best way to ensure that only valid data is saved into your database. 

Rails provides built-in helpers for common needs, and allows you to create your own validation methods as well.

If any validations fail, the object will be marked as invalid and Active Record will not perform the INSERT or UPDATE operation. This avoids storing an invalid object in the database. You can choose to have specific validations run when an object is created, saved, or updated.

The following methods trigger validations, and will save the object to the database only if the object is valid:

* create
* create!
* save
* save!
* update
* update!

The bang versions (e.g. save!) raise an exception if the record is invalid. The non-bang versions don't: save and update return false, and create returns the object.

In my Music Enrollments App, I have used model level validation by calling **.valid?**  and **.save** in the create method written in app/enrollments_controller.rb , this triggers validations written in app/ models/ enrollment.rb. 

When user clicks  button "Create Enrollment" , the browser sends a **Post** request to the server , rails follows the route **/enrollments** and finds the matching controller action  **enrollments#create** , and method **def create** . 

The user gets to insert the information in the database and clicks button"Create Enrollment", if it gets inserted(saved) in the database, the user sees the message :"Success Enrollment Added".

In case the required parameters are not filled in properly, the model validation gets triggered and User sees the errors messages ,the, explicit **render :new** will display the form to take the necessary actions to create the record.

app/models/enrollment.rb

```
class Enrollment < ApplicationRecord
    belongs_to :instrument
    belongs_to :user


    validates :level, :duration, presence: true
    validates :price, numericality: {greater_than: 0, message:  "should be $39, $49, $89 only !!"}
    validates :student, presence: true, uniqueness: { message: "Name is already taken." }

```

app/controllers/enrollments_controller.rb

```
def create
  
     @enrollment = current_user.enrollments.build(enrollment_params)
      if @enrollment.valid?
        @enrollment.save
        redirect_to enrollments_path(@enrollment)
        flash[:message]= "Success,Enrollment Added."
      else
        @enrollment = Instrument.find_by_id(params[:instrument_id]) if params[:instrument_id]
        render :new
    end
  end
```

See the below snippet, **"Enrollment.errors.full_messages"**, shows the validations required to save  **new enrollment** in the database.

```
2.6.1 :032 > Enrollment
 => Enrollment(id: integer, startdate: datetime, student: string, level: string, duration: integer, price: integer, user_id: integer, instrument_id: integer, created_at: datetime, updated_at: datetime) 
2.6.1 :033 > Enrollment.new(student:"Jack Welch")
 => #<Enrollment id: nil, startdate: nil, student: "Jack Welch", level: nil, duration: nil, price: nil, user_id: nil, instrument_id: nil, created_at: nil, updated_at: nil> 
2.6.1 :034 > e=_
 => #<Enrollment id: nil, startdate: nil, student: "Jack Welch", level: nil, duration: nil, price: nil, user_id: nil, instrument_id: nil, created_at: nil, updated_at: nil> 
2.6.1 :035 > e.valid?
  Enrollment Exists? (0.4ms)  SELECT 1 AS one FROM "enrollments" WHERE "enrollments"."student" = ? LIMIT ?  [["student", "Jack Welch"], ["LIMIT", 1]]
 => false 
2.6.1 :036 > e.errors.full_messages
 => ["Instrument must exist", "User must exist", "Instrument can't be blank", "Level can't be blank", "Duration can't be blank", "Price should be $39, $49, $89 only !!"] 
2.6.1 :037 > 

```
