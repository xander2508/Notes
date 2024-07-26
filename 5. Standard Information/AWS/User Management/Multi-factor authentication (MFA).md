[Enabling a Hardware TOTP token (Console)(opens in a new tab)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_physical.html)
[Enabling a FIDO Security Key (Console)(opens in a new tab)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_fido.html)
[Enabling a Virtual Multi-Factor Authentication (MFA) Device (Console)(opens in a new tab)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html)
[Multi-Factor Authentication for IAM(opens in a new tab)](https://aws.amazon.com/iam/features/mfa/)

![[Pasted image 20240726164513.png]]

MFA requires two or more authentication methods to verify an identity.

If you activate MFA on your root user, you must present a piece of identifying information from both the something you know category and the something you have category. The first piece of identifying information the user enters is an email and password combination. The second piece of information is a temporary numeric code provided by an MFA device.

Using MFA adds an additional layer of security because it requires users to use a supported MFA mechanism in addition to their regular sign-in credentials. Activating MFA on the AWS root user account is an AWS best practice.

### Supported MFA devices

AWS supports a variety of MFA mechanisms, such as virtual MFA devices, hardware time-based one-time password (TOTP) tokens, and FIDO security keys. To learn more, take a look at the table below. For instructions on how to set up each method, see the Resources section.

|**Device**|**Description**|**Supported Devices**|
|---|---|---|
|**Virtual MFA**|A software app that runs on a phone or other device that provides a one-time passcode. These applications can run on unsecured mobile devices, and because of that, they might not provide the same level of security as hardware or FIDO security keys.|Twilio Authy Authenticator, Duo Mobile, LastPass Authenticator, Microsoft Authenticator, Google Authenticator, Symantec VIP|
|**Hardware TOTP token**|A hardware device, generally a key fob or display card device, that generates a one-time, six-digit numeric code based on the time-based one-time password (TOTP) algorithm.|Key fob, display card|
|**FIDO security keys**|FIDO-certified hardware security keys are provided by third-party providers such as Yubico. You can plug your FIDO security key into a USB port on your computer and enable it using the instructions that follow.|[FIDO Certified products](https://fidoalliance.org/certification/fido-certified-products)|