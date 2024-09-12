---
tags:
  - Security
  - StandardInformation
---
Authentication, at its core, is the validation of your identity by presenting a combination of three main factors to a validation mechanism. They are;

1. Something you know (a password, passcode, pin, etc.).
2. Something you have (an ID Card, security key, or other MFA tools).
3. Something you are (your physical self, username, email address, or other identifiers.)

The process can require any or all of these authentication descriptors. These methods will be determined based on the severity of the information or systems accessed and how much protection they need. For example, doctors are often required to utilize a Common Access Card (CAC) paired with a pin-code or password to access any terminals that input or store patient data. Depending on the maturity of the organization's security posture, they could require all three types (A CAC, password, and pin from an authenticator app, for example).

Another simple example of this is access to our email address. The proof of information, in this case, would be the knowledge of the email address itself and the associated password. For example, a cell phone with `2FA` can be used. The third aspect can also play a role: the user's presence through biometric recognition such as a fingerprint or facial recognition.

In the previous example, the password is the authentication identifier that can be bypassed with different TTPs. This level is about authenticating the identity. Usually, only the owner and authenticating authority know the password. Authorization is carried out if the correct password is given to the authentication authority. Authorization, in this case, is the set of permissions that the user is granted upon successful login.

## The Use of Passwords

The most common and widely used authentication method is still the use of passwords, but what is a password? A password or passphrase can be generally defined as `a combination of letters, numbers, and symbols in a string for identity validation.` For example, if we work with passwords and take a standard 8-digit password that consists only of upper case letters and numbers, we would get a total of `36⁸` (`208,827,064,576`) different combinations of passwords.