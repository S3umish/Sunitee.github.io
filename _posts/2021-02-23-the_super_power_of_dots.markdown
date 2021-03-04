---
layout: post
title:      "The Super Power of . Dots !!"
date:       2021-02-23 12:27:40 -0500
permalink:  the_super_power_of_dots
---




You must have seen dots , also known as "bindi" on forheads , it means I am **focussed** , I am **committed** and I have a **purpose**.



Dots are also known as period, fullstop , in connection with , etc . Dots are powerful in mathematical contexts too , remember, we use dots to show multiplication (2 . 3 = 6) and decimals , the famous" pi", 3.141592653589793238.


In the Ruby world, I have learnt dots are equally powerful and widely used to fetch information, chain methods.and what not !!

In the below snippet , you will find the super powerfull dots in full action. 

**Dot notation** is fantastic for readability, as we can just reference the bare key name (e.g., .username or .email ). Because of this simple syntax, it should be your go-to strategy for accessing the properties of an Object.


See below, the omniauth method , the active record association like find_or_create is to find the user instance, u.username , u.email , u.password  and ultimate method  user.errors.full_messages.to_sentence in full glory.  


In the "request.env[omniauth.auth]" , the key in the environment hash provides an Authentication Hash which will contain information about the just authenticated user including a unique id, the strategy they just used for authentication, and personal details such as name and email address as available. 

A small mighty Dot can accomplish huge tasks.




```
def omniauth
      user = User.find_or_create_by(provider: auth['provider'], uid: auth['uid']) do |u|
        u.username = auth['info']['name']
        u.email = auth['info']['email']
        u.password = SecureRandom.hex(16)
      end
      
      if user.valid?
        session[:user_id] = user.id 
        redirect_to user_path(user)
        flash[:message] = "Hello and Welcome Google User!"
      else
        flash[:error] = user.errors.full_messages.to_sentence
        redirect_to login_path
      end
    end
		
		private 

  def auth 
    request.env['omniauth.auth']
		
  end

```




The Rails server call $ rails s also runs on dots ........

```

=> Booting Puma
=> Rails 6.1.2.1 application starting in development 
=> Run `bin/rails server --help` for more startup options
Puma starting in single mode...
* Puma version: 5.2.1 (ruby 2.6.1-p33) ("Fettisdagsbulle")
*  Min threads: 5
*  Max threads: 5
*  Environment: development
*          PID: 47491
* Listening on http://127.0.0.1:3000
* Listening on http://[::1]:3000
Use Ctrl-C to stop
```


Like " dot notation " I am highly impressed with "self " in Ruby. 

In case you are wondering what is Omniauth?? , **Omniauth** is a gem which provides an interface to your application to login through third party authentication system. It helps gain access to the user’s data from the provider in the Sessions Controller .
* Typically, if a matching User exists in your database, the client will be logged in to your application. If no match is found, a new User will be created using the data received from the provider.
* From User’s standpoint, the User tries to access a page on yoursite.com that requires them to be logged in. 
* They are redirected to the login screen.
* The login screen offers the options of creating an account or logging in with third party authenticators called provider like Google ,Facebook, Gituhub etc .
* The user clicks, the button” Log in with Google”. This momentarily sends the user to yoursite.com/auth/google, which quickly redirects to the Google sign-in page.
* If the user is not already signed in to Google, they sign in normally. More likely, they are already signed in, so Google simply asks if it's okay to let yoursite.com access the user's information. 
* The user agrees and are hopefully quickly redirected to yoursite.com/auth/google/callback and, from there , to the page they initially tried to access.


I am hopeful that in the next mod, I will find more interesting connections with the real world !! Thanks for reading .


