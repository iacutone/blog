+++
title = "refactoring client side validations"
date = "2014-01-21"
slug = "2014/01/21/refactoring-client-side-validations"
Categories = []
+++

<p> I have been working on refactoring my client side JavaScript validations on an application.  My tech lead gave me some illuminating tips on how to refactor my non-DRY code.  Here is an example of the pre-refactored code.</p>

{% codeblock _form.html.erb lang:erb %}
<%= form_for(@order) do |f| %>
  <div class='your_info'>
    <h3>2. Your Information</h3>
    <div class="clearfix">
      <%= f.label :first_name, 'First name*' %>
      <div class="input">
        <%= f.text_field :first_name %>
        <span id="first_name_error"></span>
      </div>
      <div class="input">
        <%#= f.hidden_field :customer_id, value: current_user.id unless current_user.id == nil %>
      </div>
    </div>
    <div class="clearfix">
      <%= f.label :last_name, 'Last name*' %>
      <div class="input">
        <%= f.text_field :last_name %>
        <span id="last_name_error"></span>
      </div>
    </div>
    <div class="clearfix">
      <%= f.label :email, 'Email*' %>
      <div class="input">
        <%= f.text_field :email %>
        <span id="email_error"></span>
      </div>
    </div>
  </div>
  <%= f.submit "Submit your Order", class: 'btn btn-primary btn-lg', id: 'button', data: { confirm: "Place order?" } %>
<% end %>
{% endcodeblock %}

<p>So, let's start with this basic form and sprinkle it with some JQuery and Javascript for client side validations.</p>

{% codeblock users.js lang:js %}
// Initial State for Form
$('.your_info').hide();

// validations
var first_name = $('input#order_first_name');
var last_name = $('input#order_last_name');
var email = $('input#order_email');

// event listeners
first_name.keyup(function(){
  validateFirstName();
});

last_name.keyup(function(){
  validateLastName();
});

email.keyup(function(){
  validateEmail();
});

function validateFirstName(){
  var first_name_val = first_name.val();
  if(first_name_val.length == 0) {
    first_name_error.show().text("First name needed.").addClass('error_class');
    return false;
  }
  else {
    first_name_error.hide();
    return true;
  }
}

function validateLastName(){
  var last_name_val = last_name.val();
  if(last_name_val.length == 0) {
    last_name_error.show().text("Last name needed.").addClass('error_class');
    return false;
  }
  else {
    last_name_error.hide();
    return true;
  }
}

function validateEmail(){
  var email_val = email.val();
  if(email_val.length == 0) {
    email_error.show().text("Email needed.").addClass('error_class');
    return false;
  }
  else {
    email_error.hide();
    return true;
  }
}
{% endcodeblock %}

<p>Clearly, this is not DRY and will easily get out of comtrol.  However, using HTML data attributes solves this problem.  Here is a good <a href='http://ejohn.org/blog/html-5-data-attributes/'>summary</a> about data attributes by John Resig.</p>

{% codeblock _form.html.erb lang:erb %}
<%= form_for(@order) do |f| %>
  <div class='your_info'>
    <h3>2. Your Information</h3>
    <div class="clearfix">
      <%= f.label :first_name, 'First name*' %>
      <div class="input">
        <%= f.text_field :first_name, :data => {:error => 'First name'} %>
        <span id="first_name_error"></span>
      </div>
    </div>
    <div class="clearfix">
      <%= f.label :last_name, 'Last name*' %>
      <div class="input">
        <%= f.text_field :last_name, :data => {:error => 'Last name'} %>
        <span id="last_name_error"></span>
      </div>
    </div>
    <div class="clearfix">
      <%= f.label :email, 'Email*' %>
      <div class="input">
        <%= f.text_field :email, :data => {:error => 'Email'} %>
        <span id="email_error"></span>
      </div>
    </div>
  <%= f.submit "Submit your Order", class: 'btn btn-primary btn-lg', id: 'button', data: { confirm: "Place order?" } %>
<% end %>
{% endcodeblock %}

{% codeblock users.js lang:js %}
$('input').keyup(function(){
  blankValidation.call(this);
});

function blankValidation(){
  var error_name = $(this).data('error');
  console.log(error_name);
  var value = $(this).val();
  console.log(value);
  if(error_name !== undefined){
    var error_id = ('#' + error_name.toLowerCase().replace(' ', '_') + ('_error'));
    var error_message = $(error_id);
    if(value.length === 0) {
      error_message.show().text(error_name + " needed.").addClass('error_class');
      return false;
    }
    else {
      error_message.hide();
      return true;
    }
  }
}
{% endcodeblock %}

<p>We can dynamically call the data attribute for each element.  For example, the error_name value the keyup event(m) will console.log (=> First name, m). The call method allows us to refactor all of our keyup event listeners into one method.  The call method as defined by the Mozilla guide "calls a function with a given this value and arguments provided individually."</p>
<p>h/t Dan Porter</p>

<p>Reference</p>
<ul>
  <li><a href='http://yehudakatz.com/2011/08/11/understanding-JavaScript-function-invocation-and-this/'>Understanding JavaScript Function Invocation and this</a></li>
  <li><a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call'>Function.prototype.call()</a></li>
  <li><a href='https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply'>Function.prototype.apply()</a></li>
</ul>
