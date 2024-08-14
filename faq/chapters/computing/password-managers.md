# Which password manager should I use?

> ⚠️ DISCLAIMER: I am not a security expert. I recommend you do your research and choose the password manager that best fits your needs.

Passwords are necessary for everyone with a computer, smartphone, or other smart device. 
Some of us may struggle to remember them, and many find tips to strengthen them, but eventually, remembering them is their primary weakness. Using multiple complex passwords can be challenging, leading many people to reuse weak passwords (sometimes with slight variations) or store them insecurely.


## Why should we all use password managers?

Worryingly, studies have shown that many people have become careless with their passwords. Nearly 35 percent of us use the same password for most online logins. Worse still, 42 percent of tech users have reported having an account hacked at least once (source [YouGov](https://today.yougov.com/technology/articles/19411-28-americans-use-one-password-most-or-all-online-l)). Because of these statistics, it is essential to understand the risks associated with poor password security and that we use our laptops and email accounts to store a massive amount of sensitive and valuable data, from banking to personal life information. People are not lax about their passwords because they don't care about their data; they are lax because they are overwhelmed by the number of passwords they need to remember.

That's where password managers come in. Password managers are software applications that help you securely store and manage your passwords. They generate unique passwords for each account, store them securely, and automatically fill them in when needed. 


Password managers offer several benefits, including:

* **A password manager stores all your passwords in a single account**. The master password to your safe is the only password you’ll ever need to remember. You can also link this password to biometrics (e.g., fingerprint, facial recognition) so that even that password can be highly complex. [Is it reasonable to have it all in one place?]

* **Password managers generate strong, unique passwords for each of your accounts**, reducing the risk of password reuse and making it harder for hackers to gain unauthorized access.

* **Password managers can automatically fill in your login credentials**, saving time and effort when logging into websites and applications. Auto-fill functionality works across devices (laptop, phone, tablet) and different applications (browsers, apps, etc.)

* **Easily change your password**. If you suspect that one of your accounts has been compromised, you can quickly change the password for that account without having to remember it. Some password managers can even automatically update your passwords with a few clicks.

* **Share passwords securely**. Some password managers allow you to securely share passwords with trusted individuals, making it easier to collaborate on shared accounts without compromising security.

* **Use the same password manager across multiple devices**. Password managers are available on various platforms, including desktops, smartphones, and web browsers, allowing you to access your passwords from anywhere.

## What are my options?

Several password managers are available, each with features and security measures. First and foremost, most web browsers have a built-in password manager (e.g., Google, Apple, Mozilla). When you're logging into your online accounts, most web browsers (such as Chrome, Safari, and Edge) will offer to save them for you. But usually, you do not need to authenticate more than once in the lifetime of your device to use those passwords. Recent developments show progress in this area, with Google and Apple opting to create dedicated password manager services (still behind others). If you’re using a shared computer inside/outside your home, you should probably never save your password in a browser.
Security experts recommend using a dedicated password manager.

Some popular options include:

- [1Password](https://1password.com/)
- [Bitwarden](https://bitwarden.com/)
- [Dashlane](https://www.dashlane.com/)
- [KeePass](https://keepass.info/)
- [NordPass](https://nordpass.com/)
- [ProtonPass](https://proton.me/pass)
- [KeepassXC](https://keepassxc.org/)
- [pass](https://www.passwordstore.org/)

> ⚠️ [LastPass](https://www.lastpass.com/) is/was a popular choice for managing passwords, but its reputation has plunged after [recent security breaches](https://blog.lastpass.com/2022/12/notice-of-recent-security-incident/).

All manager have their pros and cons. Some are free, while others require a subscription. Some are cloud-based, while others store your passwords locally. Some offer features like secure sharing, password auditing, and two-factor authentication. Researching and choosing a password manager that aligns with your specific needs and preferences is essential. Regularly update your password manager and use strong, unique master passwords to ensure maximum security.

### Opinionated view on available password managers

_This section is opinionated and may not reflect the views of the entire community. I wrote this part to share how I picked my current password manager._

My main driver for choosing a password manager was the ability to use it across multiple devices, e.g., laptop and phone. I also wanted one dealing with console-based credentials (e.g., SSH keys). [I discuss the 2FA token feature below; this was a plus.] Navigating the options was a bit overwhelming, especially when you are not a security expert.

Some will lead you toward [Pass](https://www.passwordstore.org/), [KeepassXC](https://keepassxc.org/), or [KeePass](https://keepass.info/), which are open-source and locally stored. They are great options if you are looking for a free and secure solution with all information stored locally. However, they require more technical knowledge to set up and maintain. [KeeWeb](https://keeweb.info/) is an option if you want to synchronize your passwords with file storage cloud services (Dropbox, Google Drive, etc.). However, I could not find a simple, practical solution for mobile devices.   

Out of those with CLI (command-line interface) features, [1Password](https://1password.com/) and [Bitwarden](https://bitwarden.com/) were the most recommended and for which the CLI installation was simple (no need for root privilege, no specific libraries), and they are directly compatible with all system architectures (Intel, ARM, M2 chips, etc).

My choice was [Bitwarden](https://bitwarden.com/). 

What made me pick it?
* Open-source: its code is publicly available for anyone to review and audit. I feel that transparency is a good sign of trust. 
* No one at Bitwarden can access my data. It is silly, but some companies can access your data or your master password, and I wanted to avoid that.
* CLI: I can log in and retrieve my passwords from the terminal; this is very handy when working on a remote server.
* Stores more than passwords: I can store my passwords, SSH keys, API tokens, secure notes, and other sensitive information.
* Cloud-based synchronization: I can access my passwords from any device with an internet connection, but also when offline (useful if you store sensitive notes or documents).
* Multiple vaults: I can separate and organize my personal and professional passwords in folders.
* Biometric authentication: I can use my fingerprint to unlock the vault on my phone, Mac laptop, etc.
* Free version: There is a free tier that has most of the features I need.
* Reasonable price: The premium tier is affordable ($1/month) and offers additional features like 2FA token storage, secure file storage, and password health reports.

I hesitated about [1Password](https://1password.com/). It is a great password manager with a polished UI (better than BitWarden) and excellent features. However, I did not choose it for the following reasons:
* Price. I am not against a subscription, but their price ($3/month) is higher than Bitwarden for the same features.
* Closed-source. I am not against closed-source software, but it's a plus when a security company is fully transparent.
However, 1Password is an excellent choice if you are looking for a polished UI and are willing to pay for it. Their family tier is a better choice if you plan to share passwords with family members or colleagues.

It is essential to research and choose a password manager that aligns with your specific needs and preferences. To ensure maximum security, you should regularly update your password manager and use strong, unique master passwords.


## Should I Store my 2FA Tokens in my password manager?
_This section is opinionated and may not reflect the views of the entire community. I wrote this part to share how I see this debate and maybe convince you to be careful._

Storing your 2FA TOTP tokens in your password manager has become hotly debated. While password managers are great for storing passwords, in a perfect world, you should never keep 2FA (two-factor authentication) tokens in your password manager. But let's be honest, we are not living in an ideal world.

What is 2FA? Two-factor authentication (2FA) is a security process where users provide two authentication factors to verify themselves. It is a method of confirming users' claimed identities by combining two factors: usually something they know, such as a password, and something they have (security token, phone, email, etc.). But also, let's be honest; it's very annoying for three reasons: (1) you have personal phone numbers circulating, (2) waiting for an SMS or email every time you log in to a service, and (3) at some point, you may lose access to your phone number or email account (we are all changing base regularly in our careers).

The reason you have 2FA is to protect your account when your password (1FA) is discovered. If you keep your passwords and 2FA together, a breach would provide both pieces, and the 2FA would not be helpful anymore. But it's not so black and white.

There are four main reasons why storing your 2FA inside your password manager is _fine_.
1. **Time boundary**: Time-based one-time passwords (TOTPs) change every 30 seconds, unlike static passwords. If a hacker finds your password and one 2FA token, they have 30 seconds to use it — more in this [1Password blog post](https://blog.1password.com/totp-for-1password-users/#:~:text=item%20within%201Password.-,One%2Dtimeness%3F%20Yes,-One%2Dtime%20passwords).

2. **Redundancy**: If you use a password manager and give every account a unique password, TOTP is redundant security at worst. But the truth about TOTP managers (e.g., Google Authenticator, Authy, etc.) is that they are just another password manager (even if the passwords change based on time). Many of these TOTP apps do not encrypt the secrets when stored on your phone. So, an encrypted password manager would be a security upgrade compared to many TOTP apps.

3. **Same device anyway**: If you use a password manager on your phone, you already use the same device for both your password and 2FA. So, if someone has access to your phone, they may have access to your password and 2FA. Many popular TOTP apps do not even require a password or PIN to access the codes.

4. **Convenience**: Sometimes, you do have to use 2FA. Many password manager apps like Bitwarden or 1Password will either fill in 2FA codes for you after the password or copy the code to the clipboard so you can paste it. It's convenient to have everything in one automatically backed-up place. If you lose your phone, you can still access your 2FA tokens from your password manager. It is easier to secure one place to the highest level than multiple places badly.


💡 Security Is About Trade-Offs. There will never be a perfect system. Use what works best for you. Storing your 2FA in your password manager is fine for an average person. But at the very least, you should use a password manager and give every account a unique password. Adding 2FA is just the cherry on top or an imposed curse, depending on how you see it. Adapt to best practices.
