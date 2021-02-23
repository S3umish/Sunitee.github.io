---
layout: post
title:      "The Super Power of "."  Dots !!"
date:       2021-02-23 12:27:40 -0500
permalink:  the_super_power_of_dots
---



You must have seen dots , also known as "bindi" on forheads , it means I am **focused** , I am **committed** and I have a **purpose**.



Dots are also known as period, fullstop , in connection with , etc . Dots are powerful in mathematical contexts too , remember, we use dots to show multiplication (2 . 3 = 6) and decimals , the famous" pi", 3.141592653589793238.


In the Ruby world, I have learnt dots are equally powerful and widely used to fetch information, chain methods.and what not !!

In the below snippet , you will find the super powerfull dots in full action. 

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


Like "Dots " I am highly impressed with "Self " in Ruby. 

I am hopeful that in the next mod, I will find more interesting connections with the real world !! Thanks for reading .


