# OBSConnect
This project provides a basic authentication page to make using a password on your OBS Websocket easier, by saving it once on the auth page and providing it to other pages after you allow it.
## For Developers
Send your users to the page `https://sugoidogo.github.io/obsconnect?redirect_uri=yourpageurlencodedhere` to prompt for acces to OBS-Websocket. If they allow the connection, this page will sort out gathering the connection info, testing that it works, and then returning the user to your page with the query string `?obsurl=ws://localhost:4455&obspassword=examplepassword&userChoice=allow` or `?userChoice=deny`, depending on what they chose. You can now save that info using something like [localStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) and connect to obs with something like [obs-websocket-js](https://github.com/obs-websocket-community-projects/obs-websocket-js) for a fully abstracted connection method.
## For Users
Send [this page](https://github.com/sugoidogo/obsconnect) (THE LINK, NOT A SCREENSHOT) to the developer of whatever web-based obs tool you want to use it.

( If you user sent you this in a screenshot anyways, it's at github.com/sugoidogo/obsconnect )
## Support
- Get support via [Discord](https://discord.gg/PbGT9tVWTC)
- Give support via [Ko-Fi](https://ko-fi.com/sugoidogo)
## Security
This project stores your OBS Websocket password in `localStorage` for re-use whenever a new web app wants to connect to OBS. Depending on your browser, that means your password is stored unencrypted somewhere in your browser data. That would be a possible security concern, if obs-websocket weren't already [storing your password in plain text](https://github.com/obsproject/obs-websocket/discussions/766#:~:text=via%20this%20dialog.-,%5BTechnical%20Note%3A%5D,-This%20feature%20has).
## Licence
This project is licenced under the AGPL, meaning any forks of this software must also be AGPL, and provide their source code to their users with the program. Being that this software is a single web page, that should be easy, as this type of program is distributed in source form. Using this project as described in the "For Developers" section above does not constitute a derivative work, so you can still use whatever licence you please for your original work.
## Contributing
Feel free to submit any and all pull requests. This type of software works best if everyone uses the same instance of it anyways, since the password and url this project stores are only accessible to the domain it was stored on, so it's a better user experience for any forks to merge back into this one than for a fork to be used for each project that wants changes, that way the end user only has to input their generated password once.
## WebSocket Secure
Due to security limitations enforced by browsers, an https website cannot connect to an 'insecure' websocket like the one provided by obs-websocket on any host besides `localhost`, and a 'secure' websocket would require that obs-websocket be reachable from a domain name the connecting device trusts (aka: buying a domain name and putting your obs websocket on the internet, or circumventing the web trust system entirely). That means if you want to develop a web app that uses features like [MediaDevices](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices), which require https, you cannot connect to obs-websocket on a remote device, even in the local network. For now, you can use [adb reverse tcp:4455 tcp:4455](https://linuxcommandlibrary.com/man/adb-reverse) to make the connection on Android devices.
