# JS_Validation
A vanilla JS script to validate  forms. It is based on Google's Material Design. 

It uses the DOMContentLoaded event to set all up.

---


## How to Use


### Form Tag

In your form HTML, add the data-attribute data-validate="ok". You can also add a data-title="Some title" attribute to add a Title to the box. 
Your form tag should look like this: 
```html
<form data-validate="ok" data-title="Some Title here">
```

### Input fields 

To make your fields required using this script, you must add the data-attribute data-required="Some text to show on the alert box". You can choose between: 

* data-required: Accepts only the text that should display when the field is empty/unchecked;
* data-required-email: Accepts the text message when the field is empty and when the email is invalid;
* data-required-function: Accepts the function, giving this = input field, the message when field is empty and the message when the function returns false.
* (in development) data-required-if: I'm still trying to figure out how to set this and to define a syntax here. It will make the field required, only if a certain condition is attended to. 

The syntax are:
``` 
data-required="Some text" 
data-required-email="Some text when field is empty || Some text when email is invalid" 
data-required-function="someFunction(this); Some text when field is empty or unchecked || Some text when function returns false"
(in development) data-required-if="I'm still trying to define a syntax here": It will make the field required, only if a certain condition is attended to. 
``` 

In the end, your input tag should like this: 
```html
<input type="text" data-required="Some text to show on Box" name="fieldName" />
```

PLEASE NOTE: the ``` data-required-function ``` only accepts the field as argument. So if you need some other param on your function, add it to your input field and recover it from there on your function. 

### JS Code

You can also create a custom box anytime you like, for whatever objective you have. The Box function receives an Object, and returns itself on the button actions. 

The Object propertis are: 
* title: The title that will show up on the box header. It is optional;
* messages: The messages of the box. It can be a String or an Array of messages;
* buttons: It is the buttons that you want to be on the box. It uses {buttonKey:"Button Text"} syntax;
* actions: It is the actions that your buttons will do. It uses {buttonKey: buttonAction} syntax.


```javascript
Box(
  {
    title: "Title is optional. You can ommit it on your <form> tag",
    messages: "It can be a string, or an array - ['message 1', 'message 2']",
    buttons: {buttonKey:"Button Text",otherButtonKey:"Other Button Text"},
    actions: {buttonKey: buttonAction, otherButtonKey:otherButtonAction}
  }
)
```

PLEASE NOTE: When you're binding an action to the button, the script will give itself as a parameter. Here's an example:
```javascript
Box(
  {
    messages: "Just an example",
    buttons: {ok:"OK"},// please note the key for the button
    actions:{
      ok:function(box){ // this action will be binded to the "ok" key button
        console.log(box); // it will show the box instance
        box.close(); // it will close the box
      }
    }
  }
)
```

### Example FORM in HTML
```html 
<form data-validate="ok" data-title="My Box Title Text here">
  
  <input type="text" name="name" data-required="My required text message for this input here" />
  <input type="text" name="email" data-required-email="My text message when field is empty || My text message when email is invalid" />
  <input type="email" name="email" data-required-email="My text message when field is empty || My text message when email is invalid" />
  
  <input type="radio" name="radiobox" value="true" data-required="My text when this or none of the radios within same name are not checked" />
  <input type="radio" name="radiobox" value="false" data-required="My text when this or none of the radios within same name are not checked" />
  
  <input type="checkbox" name="checkbox" value="false" data-minimum="2" data-required="My text when this or none of the checkboxes within same name are not checked or doesn't match the minimum number of checked inputs" />
  <input type="checkbox" name="checkbox" value="false" data-minimum="2" data-required="My text when this or none of the checkboxes within same name are not checked or doesn't match the minimum number of checked inputs" />
  
  <input type="submit" value="Submit" />
  
</form>
```


---



#### And that's it! 

Just load the JS file and the CSS file on your page and you're good to go. 
