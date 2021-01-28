## Account registration

| First Name | Last Name | E-Mail | Telephone | Password | Repeated Password | Newsletter | Privacy Policy | | Outcome |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Valid | Valid | Valid | Valid | Valid | True | On | On | | Registered with newsletter subscription |
| Valid | Valid | Valid | Valid | Valid | True | Off | On | | Registered without newsletter subscription |
| Invalid | Invalid | Invalid | Invalid | Invalid | False | Off | Off | | Reload with Invalid / Empty fields highlighted |
| empty | empty | empty | empty | empty | empty | Off | Off | | Reload with Invalid / Empty fields highlighted |
| Invalid | Invalid | Valid | Invalid | empty | False | On | On | | Reload with Invalid / Empty fields highlighted |
| Valid | empty | empty | Invalid | Invalid | True | Off | Off | | Reload with Invalid / Empty fields highlighted |
| empty | empty | Invalid | Valid | Valid | True | On | On | | Reload with Invalid / Empty fields highlighted |
| Invalid | Valid | empty | Valid | Invalid | False | On | Off | | Reload with Invalid / Empty fields highlighted |
| empty | Valid | Invalid | empty | empty | False | Off | Off | | Reload with Invalid / Empty fields highlighted |
| empty | Invalid | Valid | empty | Valid | True | Off | Off | | Reload with Invalid / Empty fields highlighted |
| Valid | Valid | Valid | Valid | empty | False | Off | On | | Reload with Invalid / Empty fields highlighted |
| Invalid | empty | empty | empty | empty | True | On | On | | Reload with Invalid / Empty fields highlighted |
| Invalid | Valid | Invalid | Invalid | Valid | False | Off | Off | | Reload with Invalid / Empty fields highlighted |
| Valid | Invalid | Invalid | empty | Invalid | False | On | On | | Reload with Invalid / Empty fields highlighted |
| empty | empty | Valid | Invalid | Invalid | False | On | On | | Reload with Invalid / Empty fields highlighted |
| empty | Invalid | empty | Valid | Valid | True | Off | On | | Reload with Invalid / Empty fields highlighted |
| Valid | Valid | Invalid | empty | Valid | True | On | Off | | Reload with Invalid / Empty fields highlighted |

All input fields are required and have their own acceptance criteria. The following circumstances are catered for, valid registration with and without newsletter subscriptions, all fields with a value but not matching minimum criteria, all fields left untouched. Then lastly using pairwise testing to see if some combination of wrong and valid inputs can cause the system to accept something it should not because of the large possiblity of input combinations. pairwise repo: https://github.com/microsoft/pict

## Log in

| E-Mail | Password | | Outcome |
| --- | --- | --- | --- |
| Valid | Valid | | User signs into their account |
| Valid | Invalid | | Error |
| Invalid | ~ | | Error |
| Empty | ~ | | Error |

A log in is used to match an email address to a password. If the Email does not exist within the system, or the email and password do not match, an error will be displayed.

## Forgot password

| E-Mail | | Outcome |
| --- | --- | --- |
| Exists |  | Sends password reset link via E-Mail |
| Doesn't Exist |  | Error |
| Empty |  | Error |

Using a Forgot Password form will allow you to provide your account E-Mail to request a link to reset the password to your account.

## Change Password

| Password | Password Again | | Outcome |
| --- | --- | --- | --- |
| Valid | Match | | Updates the password for the account to the value provided |
| Valid | No Match | | Error |
| Empty | ~ | | Error |
| Invalid | ~ | | Error |

When updating your password, the password field needs to be provided with a valid account password with an additional repeated entry to ensure that you typed it correctly the first time. 

[Return to README](https://github.com/seth-rah/OC-HA/blob/main/README.md)