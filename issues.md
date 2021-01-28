## Disclaimer

Any issues listed were found on OpenCart 3.0.1.1 using the publically accessible demo. The OpenCart git repository is currently on version 3.0.3.6. Not all problems listed are guaranteed to still be relevant on an up to date platform.

## Bugs / concerns encountered on the administration platform

#### Extensions filter mismatches page content under certain conditions.

When using the "back" feature in your web browser on a subpage for a module, the page contents will load content that is not currently selected in the filter. 

**Steps to reproduce:**

1. sign in at https://demo.opencart.com/admin/ with default demo credentials
2. using the navigation on the left, select "Extensions" > "Extensions"
3. Opens to the default "Analytics" information pre-filtered
4. Change the dropdown under the extension type to the heading that contains "Modules" 
5. wait for the filter to update the page contents and then select the edit button on banner 1 (Installed banner module heading)
6. wait for page load to finish and then click back in your web browser to return to the previous page
7. filter pulls information from "Analytics" heading while displaying that it's currently using the "Modules" heading and will not update until the filter selection is changed to a different value.

**Suggested Solution:**

1. When pressing back from step 6 to return to the extension list, the extension type dropdown should update to display the name of the extension that the page is currently showing filtered data for.
2. The page should load with the data that the dropdown shows on page load. In the case of the reproduction steps, it would show filtered data based on the Modules heading. Unfortunately doing this will create an inconsistency in navigation that would require addressing other buttons on the extensions page to be updated to function the same.

#### Modules that can have children elements do not update their status correctly

when signed into the admin platform, using the navigation on the left, select "Extensions" > "Extensions" and update the filter to show "Modules".

Installed Modules that include an "add new" button in the action column will have their status shown as "Disabled" instead of "Enabled". This is also relevant when the given module has children that are currently enabled.

**Suggested Solutions:**

1. Set status value to enabled if the module has been installed
2. Apply new logic that's able to interpret the amount of enabled / disabled children for the module and show that in the status column instead. "3 enabled, 2 disabled" as an example.

## Bugs / concerns encountered on the storefront

#### Email validation has 2 different sets of limitations applied

**Expectations:** Emails are accepted as long as they conform to email syntax and don't already exist within the system when used for registration. 

**Problems encountered:**

The Email input field validation fails non-English characters in the address local-name and restricted special characters in the full address. https://en.wikipedia.org/wiki/Email_address#Internationalization

1. Latin alphabet with diacritics: Pelé@example.com
2. Greek alphabet: δοκιμή@παράδειγμα.δοκιμή
3. Traditional Chinese characters: 我買@屋企.香港
4. Japanese characters: 二ノ宮@黒川.日本
5. Cyrillic characters: медведь@с-балалайкой.рф
6. Devanagari characters: संपर्क@डाटामेल.भारत

**Root cause:**

Account email is validated in 2 parts during registration. 

1: regular expression that does a general formatting check.
2: a php filter called FILTER_VALIDATE_EMAIL that is only invoked on registration form submission.

There isn't a need for an email address to be validated more than once. 

The first validator has a limited support for valid email special characters as well as not supporting non-English characters in the address local-name. https://www.w3.org/Bugs/Public/show_bug.cgi?id=15489

The second validator verifies that the address conforms to IETF standards with the exception of CFWS and dotless domain names. More information can be found here: https://tools.ietf.org/html/rfc822

**Suggested Solution:**

Don't use `type="email"` on input fields. https://justmarkup.com/articles/2015-02-13-input-type-email-better-dont-use-it/

#### Account Telephone number allows users to provide values that can't be called.

**Expectations:** 

If the field is set as required, then phone numbers are accepted in the formats that users are likely to supply as input. 

**Problems encountered:**

The input field has no validation aside from the content needing to be between 3 - 32 in length.

**Suggested Solution:**

The input can be validated with the following rules to accept common formats with which users would provide their telephone number.
| Accepted Values | Count | Where |
| --- | --- 	|  --- |
| ( 	| 0 - 1 | Start or after "+"
| )		| 0 - 1 |	After "(" and at least 1 number 
| +		| 0 - 1 | Start or after "("
| 0		| 0 - 1 | Start or after "(" if "+" is not present
| -		| *			|	Must be between 2 numbers or space
| 0-9	|	7 - 15	| Anywhere

This would support users that enter data that looks similar to the following examples:

(+91) 444-444-5555, +(91) 444-444-5555, (0) 444-444-5555, +91 444-444-5555, +91444 - 444 555, 0 444 444 5555, 0444444555

Once parsed, if saving would be successful, all non-number values can be stripped from the Telephone payload and stored as that. A telephone number can be interpreted based on the first digit in the value, so it's important to keep the format intact and not have it be formatted in a way that might strip the first digit if it's a 0.

#### Password security is very poor for a commerce platform

**Expectations:** 

Being a commerce platform, basic security measures should be in place that accepts no less than 8 characters as a password.

**Problems encountered:**

The password field allows users to register with passwords that might leave their account vulnerable.

**Suggested Solution:**

Increase the minimum length of required passwords for users to at least 8 characters. 

**Additional elaboration:** 

Password entropy in computing has been established based on expecting certain types of characters within the ASCII character set. Not only won't this accomodate for languages that do not make use of ASCII, but studies have shown that longer passwords are more secure and easier to remember than complex shorter passwords. With this in mind, I have excluded needing to use a given amount of specific characters as a requirement. https://xkcd.com/936/

**The extra mile:** 

It's possible to protect users by not accepting passwords that are found in a database of most commonly used passwords. Additionally one can check to see if a password matches known weak pattern types. More information about both in the links attached.

https://en.wikipedia.org/wiki/Wikipedia:10,000_most_common_passwords

https://en.wikipedia.org/wiki/Password_strength#Examples_of_weak_passwords

**Concerns:**

It's unknown whether trying to protect your userbase will be seen as a positive step in the right direction or as an obnoxious extra step that would detract users from the platform. At which stage can you say you put in a good amount of security measures with the lowest impact on the UX.

#### Name and Last name acceptance criteria too weak

**Expectations:**

Is accepted as long as it starts with either an alphabetic, syllabic or logographic character and is not longer than 32 characters.

**Problems encountered**

As long as the name fields contained any non-whitespace character, it was accepted by the system. This leads to entries like "_" being accepted as valid. 

#### System vulnerable to email indexing

**Problem:**

Pages that allow users to enter an email that provides feedback regarding whether that email can be used or not will show a message that reaffirms whether an address is in the system. During account registration, users are shown that the provided email exists in the system and on password reset users are told when an email is found to have a password reset for. This can allow malicious users to create a database of known clients.

**Suggested Solution:**

Apply rate limiting on a per device basis for pages that have access to doing checks against email addresses that exist within the system. 

[Return to README](https://github.com/seth-rah/OC-HA/blob/main/README.md)