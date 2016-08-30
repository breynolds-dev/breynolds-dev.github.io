---
layout: post
title:  "Go Big or Go Home?"
date:   2016-08-30 19:46:36 +0000
---

![code-shot](http://i.imgur.com/tlluQJ8.jpg)


As I type I’m finishing up with the requirements of my Rails Assessment and getting ready to submit my project. My total time to complete this assessment has got to be over 100 hours of work, but that’s just a rough guess.

I had a really hard time figuring out what to do for this assessment and in the end I decided to rebuild a half-finished project that I was originally building in straight PHP and MySQL. Should’ve been easy to convert right? That’s what I thought too. I already had a bootstrap styled layout that I liked and most of the css and javascript was figured out for me. All I needed to do was add a few ERB tags here and there, create my models and it should be good to go.

That’s far from what happened though. Most of it ended up being my own fault for trying to tackle such a huge project. If I’d stuck with something smaller like a multi-user notepad app or a recipe keeper app I don’t think it would’ve taken nearly as long to complete. The whole thing wasn’t that bad though, I really learned a lot about rails forms, nested forms and even nesting a form inside of ANOTHER nested form. RIGHT?!? How cool is that kind of stuff! Granted it took me forever to figure out how to do such a thing. Then forever and a day to figure out how to get my strong params to accept said double-nested content and since I needed content to write about let’s talk about that!

Double Nested Form

So I spent a decent amount of time playing around with a trying to figure out how to nest a fields_for inside of another fields_for tag. It’s probably not something that comes up very often and for good reason, however I was dead set on my current setup for my assessment so I wanted to make it work hell or high water. To set the stage I have a few different models that come into play here, a customer model, a company model and an address book model.

```
class AddressBook < ActiveRecord::Base
  has_one :customer
  has_one :company
end

class Customer < ActiveRecord::Base
  belongs_to :address_book
  has_one :company
  accepts_nested_attributes_for :address_book
  accepts_nested_attributes_for :company
end

class Company < ActiveRecord::Base
  belongs_to :customer
  belongs_to :company_address, class_name: ‘AddressBook’, foreign_key: ‘address_book_id’
  accepts_nested_attributes_for :company_address
end
```

Those seem like pretty basic models and I’ve cut out a lot of the extra validation and associations that connect other models from here.  At it’s base we have a Customer and Company who both use our AddressBook model for mailing addresses.  This works great until they are nested then it becomes `Customer.company.address_book` or in my params it became `params[:customer][:company_attributes][:address_book_attributes][:city]`. That’s crazy long! To make it worse there seemed to be a big issue when using the same model twice in the same form without changing the name via an alias. When I tried to use `f.fields_for :address_book` and `company.fields_for :address_book` it didn’t give me an error, however it also did not populate any of the company address book items, or even allow those items to be changed. Confused yet? I am.

So I guess to make it easier we need some more code examples!

```
form_for @customer do |f|
  f.text_field :first_name
  f.text_field :last_name
	
  f.fields_for :address_book do |addr|
    add.text_field :city
    add.text_field :state
  end

  f.fields_for :company do |comp|
    comp.text_field :name
    comp.text_field :contact_name
		
    comp.fields_for :address_book do |comp_addr|
      comp_addr.text_field :city
      comp_addr.text_field :state
    end
  end
end
```

So that’s a super trimmed down version of my original form idea. This was before I figured out that I couldn’t use `:address_book` twice in my forms and expect it to work. It’s all part of the game right?

Now I don’t know that it was a requirement to alias the address book association in my company model, but I do know I was having problems updating and viewing information without it. I also figured it helped to make things a little easier to read when looking at the form itself.  So in the end my form looks something like so:

```
form_for @customer do |f|
  f.text_field :first_name
  f.text_field :last_name
	
  f.fields_for :address_book do |addr|
    add.text_field :city
    add.text_field :state
  end

  f.fields_for :company do |comp|
    comp.text_field :name
    comp.text_field :contact_name
		
    comp.fields_for :company_address do |comp_addr|
      comp_addr.text_field :city
      comp_addr.text_field :state
    end
  end
end
```

This helped clear up the issues with my data loading correctly AND it helped me clean up my params when I submit my data. Now if we were just going to enter our params straight into the model I could be done with this and moving onto my next task, but we want strong params.

```
def update
  if params[:company_attributes].nil?
    @customer.update(customer_params)
  else
    @customer.update(customer_company_params)
  end
end

private

def customer_params
    params.require(:customer).permit(
      :first_name, :last_name, :email,
      address_book_attributes: [:id, :address_1, :address_2, :city, :state, :zipcode]
    )
  end

  def customer_company_params
    params.require(:customer).permit(
      :first_name, :last_name, :email,
      company_attributes: [
        :name, :contact_first_name, :contact_last_name, :billing_email,
        :contact_email, :main_number, :contact_number, :fax, :id,
        company_address_attributes: [:id, :address_1, :address_2, :city, :state, :zipcode]
      ],
      address_book_attributes: [:id, :address_1, :address_2, :city, :state, :zipcode]
    )
  end
```

So this looks super ugly, like SUPER ugly. However with our strong params it’s about the only way I could find to make it work correctly. You’ll notice that we even have nested arrays inside of our params because we have crazy nested forms. One tip to anyone looking at this, don’t do it. DON’T DO IT! It works, once I finally got everything ironed out it was ok, but bleh it was a ton of work and a headache and going back to write about it a few days later I can only shake my head.

```
if params[:customer][:company_attributes][:name].empty? &&
      params[:customer][:company_attributes][:contact_first_name].empty?
      customer.update(customer_params)
    else
      customer.update(customer_company_params)
    end
```

This code here is why I used two different strong param structures. When I had everything all included it was constantly throwing fits because all of the data was on my form even if it just showed up blank, however we needed to filter that data out and not use it if there wasn’t a company name (and I added a contact first name for good measure).  I had tried an ```all?(&:empty?)``` but rails said ```all?``` it was being depreciated out in Rails 5.1, so it left me to figure something else out that would perform a similar function.

I just ended up refactoring part of that into a separate method inside my company controller so the controller action looks like this

```
if !Company.empty_params?(params)
      customer.update(customer_company_params)
    else
      customer.update(customer_params)
    end
```

And the param checks are all inside of my company model now.  It makes my controller look a little cleaner anyways.

Now I’ve got to spend hours refactoring and cleaning up the mess I’ve created so I can submit this and move on!
