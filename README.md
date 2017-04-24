SmartPass
=========

SmartPass is a Chrome/Chromium extension that automatically fills login forms with passwords encrypted using OpenPGP-enabled smart card. The encrypted password files are fetched from Google Drive and decrypted on the smart card using the [Smart Card Connector](https://chrome.google.com/webstore/detail/smart-card-connector/khpfeaanjngmcnplbdlpegiifgpfgdco) extension. As all operations run either directly on the smart card or in the browser, the extension can be used in cases where a full gpg/smart card stack cannot be installed, e.g., under Chrome OS or without admin/root privileges.
Password stores can be maintained with [zx2c4's pass](https://www.passwordstore.org) and uploaded to Google Drive using the web UI or a command line tool such as [drive](https://github.com/odeke-em/drive).

SmartPass is based on [browserpass](https://github.com/dannyvankooten/browserpass) and compatible with one of its two storage formats for passwords.

## Requirements
  * An OpenPGP-enabled smart card such as
    * a [YubiKey](https://www.yubico.com/products/yubikey-hardware/)
    * a [Nitrokey](https://www.nitrokey.com/)
    * a [Fellowship smart card](https://fsfe.org/fellowship/card.en.html)
    * ...
  * A password store on Google Drive, consisting of `gpg`-encrypted password files adhering to the format outlined below


#### Password file format
Passwords for the domain `www.a.example.com` or `a.example.com` can be stored in any Google Drive folder with the name `a.example.com`. Password files in such a folder will also be used for subdomains such as `foo.a.example.com` and `mail.a.example.com`, but not for domains like `evil.example.com` or `example.com`.

In such a folder, a username/password combination is stored as a `.gpg`-file containing the password encrypted with the user's public key. The name of the file (minus the `.gpg`) will be taken as the username.

Example: If the user `john@doe.com` uses the password `123457` on `mail.example.com`, `smart-pass` would look for a folder `mail.example.com` containing a file `john@doe.com.gpg` with the encrypted password.

## Installation
  1. Install the [Smart Card Connector](https://chrome.google.com/webstore/detail/smart-card-connector/khpfeaanjngmcnplbdlpegiifgpfgdco) extension from the web store.
  2. Install [smart-pass](https://chrome.google.com/webstore/detail/smart-pass/hlbkkfgplamgidcmijjcglabmiekfech) from the web store.

## Usage
On first use, both Google Drive and the Smart Card Connector extension will show a warning dialog outlining the permissions requested by the extension.

  1. Click on the extension icon in the toolbar or press Ctrl+Shift+L (Mac: Cmd+Shift+L) to open a list of logins for the current page.
  2. Select a login or search for logins for a different domain by pressing Enter. You can optionally choose to copy the corresponding password to the clipboard instead of filling a login form by clicking on the copy icon.
  3. Enter your smart card's PIN and press Enter. You can optionally choose to cache your PIN until you have either been inactive for 60 seconds or have locked your device. The PIN cache can always be cleared manually from the extension icon's context menu.
  4. After possibly confirming the decryption operation on your smart card reader, you will be logged in automatically.

## Contributing
See [CONTRIBUTING.md](https://github.com/FabianHenneke/smart-pass/blob/master/CONTRIBUTING.md).

## Possible improvements
  * Support inserting, editing and generating passwords
    * Use random numbers generated by the hardware RNG on the smart card
  * Offer to fill one-time passwords generated from TOTP secrets stored on the smart card

## License
[MIT](https://github.com/FabianHenneke/smart-pass/blob/master/LICENSE)

