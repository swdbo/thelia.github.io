---
layout: form
title: customer create account
form_name: thelia.front.customer.create
sidebar: form
subnav: form_list_customercreate
fields:
    - { name: "company", mandatory: "false", description: "customer's company name"}
    - { name: "title", mandatory: "true", description: "customer's title id. See [title loop](http://doc.thelia.net/en/documentation/loop/title.html)"}
    - { name: "firstname", mandatory: "true", description: "customer's first name"}
    - { name: "lastname", mandatory: "true", description: "customer's last name"}
    - { name: "address1", mandatory: "true", description: "customer's street address"}
    - { name: "address2", mandatory: "false", description: "customer's street address complement"}
    - { name: "address3", mandatory: "false", description: "customer's street address complement"}
    - { name: "zipcode", mandatory: "true", description: "customer's zip code"}
    - { name: "city", mandatory: "true", description: "customer's city"}
    - { name: "country", mandatory: "true", description: "customer's country id"}
    - { name: "phone", mandatory: "false", description: "customer's phone"}
    - { name: "cellphone", mandatory: "false", description: "customer's cell phone"}
    - { name: "email", mandatory: "true", description: "customer's email address"}
    - { name: "password", mandatory: "true", description: "customer's password. min length : 4"}
    - { name: "password_confirm", mandatory: "true", description: "customer's password verification. Check if password and password_confirm are the same"}
    - { name: "agreed", mandatory: "true", description: "for the customer to accept the terms and conditions"}
    - { name: "newsletter", mandatory: "false", description: "for saving the customer in the newsletter subscriber list"}
    - { name: "auto_login", mandatory: "false", description: "customer auto log in"}
lang: en

---
```
{form name="thelia.front.customer.create"}
<form id="form-register" class="form-horizontal" action="{url path="/register"}" method="post">
    {form_field form=$form field='success_url'}
        <input type="hidden" name="{$name}" value="{url path="/account"}" /> {* the url the user is redirected to on registration success *}
    {/form_field}

    {form_field form=$form field='error_message'}
        <input type="hidden" name="{$name}" value="{intl l="missing or invalid data"}" />
    {/form_field}
    {form_hidden_fields form=$form}
    {if $form_error}<div class="alert alert-danger">{$form_error_message}</div>{/if}
    <fieldset id="register-info" class="panel">
        <div class="panel-heading">
            1. {intl l="Personal Information"}
        </div>

        <div class="panel-body">
            {form_field form=$form field="title"}
                <div class="form-group group-title{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <select name="{$name}" id="{$label_attr.for}" class="form-control"{if $required} aria-required="true" required{/if}{if !$value || $error} autofocus{/if}>
                            <option value="">-- {intl l="Select Title"} --</option>
                            {loop type="title" name="country.list"}
                                <option value="{$ID}" {if $value == $ID}selected{/if} >{$LONG}</option>
                            {/loop}
                        </select>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {elseif !$value}
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}
            {form_field form=$form field="firstname"}
            <div class="form-group group-firstname{if $error} has-error{/if}">
                <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                <div class="control-input">
                    <input type="text" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder firstname"}" value="{$value}" {if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                    {if $error }
                        <span class="help-block">{$message}</span>
                        {assign var="error_focus" value="true"}
                    {/if}
                </div>
            </div><!--/.form-group-->
            {/form_field}
            {form_field form=$form field="lastname"}
                <div class="form-group group-lastname{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="text" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder lastname"}" value="{$value}" {if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}
            {form_field form=$form field="email"}
            <div class="form-group group-email{if $error} has-error{/if}">
                <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>

                <div class="control-input">
                    <input type="email" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder email"}" value="{$smarty.get.email|default:$value}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                    {if $error }
                        <span class="help-block">{$message}</span>
                        {assign var="error_focus" value="true"}
                    {/if}
                </div>
            </div><!--/.form-group-->
            {/form_field}
            {form_field form=$form field="phone"}
                <div class="form-group group-phone{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="text" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="20" placeholder="{intl l="Placeholder phone"}" value="{$value}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}
            {form_field form=$form field="cellphone"}
                <div class="form-group group-cellphone{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="text" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="20" placeholder="{intl l="Placeholder cellphone"}" value="{$value}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}
        </div>
    </fieldset>

    <fieldset id="register-delivery" class="panel">
        <div class="panel-heading">
            2. {intl l="Delivery Information"}
        </div>

        <div class="panel-body">
            {form_field form=$form field="company"}
                <div class="form-group group-company{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="text" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder company"}" value="{$value}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}

            {form_field form=$form field="address1"}
                <div class="form-group group-address1{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="text" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder address1"}" value="{$value}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}

            {form_field form=$form field="address2"}
                <div class="form-group group-address2{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="text" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder address2"}" value="{$value}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}

            {form_field form=$form field="zipcode"}
                <div class="form-group group-zip{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="text" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="10" placeholder="{intl l="Placeholder zipcode"}" value="{$value}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}

            {form_field form=$form field="city"}
                <div class="form-group group-city{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="text" name="{$name}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder city"}" value="{$value}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}



            {form_field form=$form field="country"}
                <div class="form-group group-country{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <select name="{$name}" id="{$label_attr.for}" class="form-control"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                            <option value="">-- {intl l="Select Country"} --</option>
                            {loop type="country" name="country.list"}
                                <option value="{$ID}"
                                        {if $value != ""}
                                            {if $value == $ID}selected{/if}
                                        {else}
                                            {if $IS_DEFAULT}selected{/if}
                                        {/if}

                                >{$TITLE}</option>
                            {/loop}
                        </select>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}
        </div>
    </fieldset>
    <fieldset id="register-login" class="panel">
        <div class="panel-heading">
            3. {intl l="Login Information"}
        </div>

        <div class="panel-body">
            {form_field form=$form field="password"}
                <div class="form-group group-password{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="password" name="{$name}" id="{$label_attr.for}" class="form-control" autocomplete="off"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}

            {form_field form=$form field="password_confirm"}
                <div class="form-group group-password_confirm{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <input type="password" name="{$name}" id="{$label_attr.for}" class="form-control" autocomplete="off"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}
        </div>
    </fieldset>

    {form_field form=$form field="newsletter"}
        <div class="form-group group-newsletter{if $error} has-error{/if}">
            <div class="control-input">
                <div class="checkbox">
                    <label class="control-label" for="{$label_attr.for}">
                        <input type="checkbox" name="{$name}" id="{$label_attr.for}" value="{$value}"{if $checked} checked{/if}  {if $required} aria-required="true" required{/if}>{$label}
                    </label>
                    {if $error }
                        <span class="help-block">{$message}</span>
                    {/if}
                </div>
            </div>
        </div><!--/.form-group-->
    {/form_field}

    {form_field form=$form field="agreed"}
    <div class="form-group group-agreed{if $error} has-error{/if}">
        <div class="control-input">
            <div class="checkbox">
                <label class="control-label" for="{$label_attr.for}">
                    <input type="checkbox" name="{$name}" id="{$label_attr.for}" value="{$value}"{if $checked} checked{/if}  {if $required} aria-required="true" required{/if}>{intl l="I've read and agreed on <a href='#'>Terms &amp; Conditions</a>"}.
                </label>
                {if $error }
                    <span class="help-block">{$message}</span>
                {/if}
            </div>
        </div>
    </div><!--/.form-group-->
    {/form_field}

    <div class="form-group group-btn">
        <div class="control-btn">
            <button type="submit" class="btn btn-register">{intl l="Register"}</button>
        </div>
    </div><!--/.form-group-->
</form>
{/form}
```