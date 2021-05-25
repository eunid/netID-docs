---
extra_css:
  - 'stylesheets/netid-button.css'
  - 'stylesheets/button-generator.css'
extra_js:
  - 'javascripts/alpine.js'
  - 'javascripts/button-generator.js'
---
# Styleguide

On the partners' side (technical term Relying Party) netID provides a smooth login experience for the user - besides the usual login or registration. This is done using the netID button.

The netID button is - like all other SSO services - clearly separated from the usual login / registration mask. Amplified by the brand specific netID green the netID Button should be clearly perceived as an alternative login possibility.

## Integration of the login button

Different buttons are available for integration in the frontend. netID currently offers four "Call to Action" buttons. These are available in three different sizes (small / medium / large). The integration is done via the code snippets provided [below](#netid-login-buttons).  

If you have additional requirements for a netID "Call to Action" button for your app or website, please do not hesitate to contact us. Please indicate the size and the button text you would like to use, to evaluate alternatives feel free to use the [Button Configurator](#netid-button-configurator). We will check your requirements against our specifications and you can use the code snippet provided by the configurator. Please send your special requirements to: info@enid.eu

You want to inform your users - beyond the netID button - with further short information about netID? For this purpose we have created a short description which you can use - please do not change it. Shortened versions of the text are possible.

Alternatives are indicated with brackets `< >`.

!!! info ""
    netID – `<Ihr/Der>` Universal-Login fürs Internet:
    `<Die persönliche>` netID ist der neue europäische Standard für den einfachen, bequemen und sicheren Login bei immer mehr Internetdiensten `</auf immer mehr Webseiten>`. Nur noch ein Passwort merken, persönliche Daten und Zustimmungen selbst zentral im netID Privacy Center organisieren und so jederzeit den Überblick behalten! Mehr Infos auf netid.de

You are also welcome to link to the netID website. On this page users will find all further information about netID. Furthermore, they can register for netID and log in to their individual netID Privacy Center.

<https://netid.de>

## netID login buttons

### CTA text: "Login mit netID"

![netID login Buttons](../images/styleguide/20200312_netid_buttons_1.png)

=== "#1 Small"
    ```html
    <button data-button-size="small"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">Login mit netID</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=small]{font-size:12px;line-height:24px}</style></button>
    ```

=== "#2 Medium"
    ```html
    <button data-button-size="medium"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">Login mit netID</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=medium]{font-size:14px;line-height:32px}</style></button>
    ```

=== "#3 Large"
    ```html
    <button data-button-size="large"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">Login mit netID</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=large]{font-size:16px;line-height:40px}</style></button>
    ```

### CTA text: "netID Login"

![netID login Buttons](../images/styleguide/20200312_netid_buttons_2.png)

=== "#4 Small"
    ```html
    <button data-button-size="small"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">netID Login</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=small]{font-size:12px;line-height:24px}</style></button>
    ```

=== "#5 Medium"
    ```html
    <button data-button-size="medium"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">netID Login</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=medium]{font-size:14px;line-height:32px}</style></button>
    ```

=== "#6 Large"
    ```html
    <button data-button-size="large"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">netID Login</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=large]{font-size:16px;line-height:40px}</style></button>
    ```

### CTA text: "Mit netID anmelden"

![netID login Buttons](../images/styleguide/20200312_netid_buttons_3.png)

=== "#7 Small"
    ```html
    <button data-button-size="small"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">Mit netID anmelden</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=small]{font-size:12px;line-height:24px}</style></button>
    ```

=== "#8 Medium"
    ```html
    <button data-button-size="medium"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">Mit netID anmelden</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=medium]{font-size:14px;line-height:32px}</style></button>
    ```

=== "#9 Large"
    ```html
    <button data-button-size="large"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">Mit netID anmelden</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=large]{font-size:16px;line-height:40px}</style></button>
    ```

### CTA text: "netID"

![netID login Buttons](../images/styleguide/20200312_netid_buttons_4.png)

=== "#10 Small"
    ```html
    <button data-button-size="small"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">netID</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=small]{font-size:12px;line-height:24px}</style></button>
    ```

=== "#11 Medium"
    ```html
    <button data-button-size="medium"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">netID</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=medium]{font-size:14px;line-height:32px}</style></button>
    ```

=== "#12 Large"
    ```html
    <button data-button-size="large"><svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 40 40"><polygon fill="#fff" points="19.14 11.43 21.63 8.99 26.33 13.69 39.59 .5 42.01 2.85 26.25 18.61"></polygon><path fill="#fff" d="M38.22,11.17 L36.22,13.17 C37.35,17 37.09,20 33.1,24 L28.45,28.64 L11.55,11.73 L16.23,7.05 C21.23,2.05 25.33,2.45 30.12,5.4 L32,3.53 C26.07,-0.47 20.47,-0.76 14.4,5.31 L0.67,19 L21.15,39.5 L34.87,25.79 C39.93,20.72 40.32,16.3 38.22,11.17 Z"></path></svg> <span data-button-text="">netID</span><style>@font-face{font-family:'IBM Plex Sans';font-style:normal;font-weight:600;src:local('IBM Plex Sans SemiBold'),local('IBMPlexSans-SemiBold'),url(https://image.netid.de/ci/netid/global/fonts/ibmplex/IBMPlexSans-SemiBold-webfont.woff) format('woff');unicode-range:U+0000-00FF,U+0131,U+0152-0153,U+02BB-02BC,U+02C6,U+02DA,U+02DC,U+2000-206F,U+2074,U+20AC,U+2122,U+2191,U+2193,U+2212,U+2215,U+FEFF,U+FFFD}button{display:flex;flex-wrap:nowrap;justify-content:center;align-items:center;width:100%;max-width:400px;margin:auto;padding:0 1em 0 .875em;border:0 solid transparent;border-radius:3px;background-color:#76b82a;cursor:pointer;font-family:'IBM Plex Sans',Courier;color:#fff;text-decoration:none;text-transform:none;white-space:nowrap;outline:0}@media screen and (min-width:768px){button{width:auto;margin:0}}button svg{width:1.25em;height:1.25em;margin-right:.438em}</style><style size-style="">button[data-button-size=large]{font-size:16px;line-height:40px}</style></button>
    ```

## netID Button Configurator

<div class="generator" x-data="{ text: 'Login mit netID', customText: 'Login mit netID', size: '', fontSize: '', buttonWidth: '', buttonHeight: '', buttonRadius: '', code: 'embedded', full: false, expert: false, style: '' }">
<svg display="none">
  <symbol id="netid-logo" viewBox="0 0 40 40">
    <path fill="#fff" d="M30.3 4.1a14.5 14.5 0 00-6-2.7C20.7 1 17 2 13.6 5.3L7 12.1l-6.9 7 19.8 19.8 8.8-8.9 5-4.9c3-3.1 4.2-6.7 3.8-10a12.9 12.9 0 00-1-3.8l-2 2a10 10 0 01.6 2c.3 2.7-.5 5.4-3.2 8l-4.9 5-16.3-16.4L15.5 7c3-3 5.7-3.6 8.3-3.1 1.6.2 3.2 1 4.7 2z" />
    <path fill="#fff" d="M37.7 1.1l-12.9 13-4.6-4.7-2.3 2.3 6.9 7L40 3.5z"/>
  </symbol>
</svg>
  <div class="grid">
    <div class="grid__cell grid__cell--6">
      <p>CTA button text</p>
      <p>
        <label class="radio" @click="$nextTick(() => { customText = text })">
          <input class="radio__input" type="radio" x-model="text" value="Login mit netID"/>
          <i class="radio__border">
            <span class="radio__checker"></span>
          </i>
          <span class="radio__label">Login mit netID</span>
        </label>
      </p>
      <p>
        <label class="radio" @click="$nextTick(() => { customText = text })">
          <input class="radio__input" type="radio" x-model="text" value="netID Login"/>
          <i class="radio__border">
            <span class="radio__checker"></span>
          </i>
          <span class="radio__label">netID Login</span>
        </label>
      </p>
      <p>
        <label class="radio" @click="$nextTick(() => { customText = text })">
          <input class="radio__input" type="radio" x-model="text" value="Mit netID anmelden"/>
          <i class="radio__border">
            <span class="radio__checker"></span>
          </i>
          <span class="radio__label">Mit netID anmelden</span>
        </label>
      </p>
      <p>
        <label class="radio" @click="$nextTick(() => { customText = text })">
          <input class="radio__input" type="radio" x-model="text" value="netID"/>
          <i class="radio__border">
            <span class="radio__checker"></span>
          </i>
          <span class="radio__label">netID</span>
        </label>
      </p>
      <p>
        <label class="radio">
          <input class="radio__input" type="radio" x-model="text" value="custom"/>
          <i class="radio__border">
            <span class="radio__checker"></span>
          </i>
          <span class="radio__label">Custom text</span>
        </label>
      </p>
    </div>
    <div class="grid__cell grid__cell--6">
      <p>Button size</p>
      <p>
        <label class="radio">
          <input class="radio__input" type="radio" x-model="size" value="-small"/>
          <i class="radio__border">
            <span class="radio__checker"></span>
          </i>
          <span class="radio__label">Small</span>
        </label>
      </p>
      <p>
        <label class="radio">
          <input class="radio__input" type="radio" x-model="size" value=""/>
          <i class="radio__border">
            <span class="radio__checker"></span>
          </i>
          <span class="radio__label">Normal</span>
        </label>
      </p>
      <p>
        <label class="radio">
          <input class="radio__input" type="radio" x-model="size" value="-large"/>
          <i class="radio__border">
            <span class="radio__checker"></span>
          </i>
          <span class="radio__label">Large</span>
        </label>
      </p>
      <p>
        <label class="radio">
          <input class="radio__input" type="radio" x-model="size" value="custom"/>
          <i class="radio__border">
            <span class="radio__checker"></span>
          </i>
          <span class="radio__label">Custom size</span>
        </label>
      </p>
      <p>
        <label class="checkbox" @click="$nextTick(() => { if (full) buttonWidth = ''; } )">
          <input class="checkbox__input" type="checkbox" x-model="full" value="true">
          <i class="checkbox__border">
            <i class="checkbox__checker"></i>
          </i>
          <span class="checkbox__label">Full width</span>
        </label>
      </p>
    </div>
  </div>
  <div class="grid">
    <template x-if="text == 'custom'">
      <div class="grid__cell grid__cell--12">
        <label for="generator-logo-text" class="label">Custom button text</label>
        <input placeholder="Text für netID Logo" id="generator-logo-text" type="text" class="input" x-model="customText">
      </div>
    </template>
    <template x-if="size == 'custom'">
      <div class="grid__cell grid__cell--12">
        <div class="grid">
          <div class="grid__cell grid__cell--s6 grid__cell--3">
            <label for="generator-font-size" class="label">Font size (px, pt, rem, re)</label>
            <input placeholder="20" id="generator-font-size" type="text" class="input" x-model="fontSize">
          </div>
          <div class="grid__cell grid__cell--s6 grid__cell--3">
            <label for="generator-button-width" class="label">Width (px, %)</label>
            <input placeholder="320" id="generator-button-width" type="text" class="input" x-model="buttonWidth" @keyup="if (buttonWidth) full = false">
          </div>
          <div class="grid__cell grid__cell--s6 grid__cell--3">
            <label for="generator-button-height" class="label">Height (px)</label>
            <input placeholder="40" id="generator-button-height" type="text" class="input" x-model="buttonHeight">
          </div>
          <div class="grid__cell grid__cell--s6 grid__cell--3">
            <label for="generator-button-radius" class="label">Border radius (px)</label>
            <input placeholder="4" id="generator-button-radius" type="text" class="input" x-model="buttonRadius">
          </div>
        </div>
      </div>
    </template>
    <div class="grid__cell grid__cell--12">
      <h4>Preview</h4>
      <div class="card-panel">
        <button class="netid-button" x-bind:class="{'-large': size == '-large', '-small': size == '-small', '-full': full && !buttonWidth}" x-bind:style="netidButton.style({size, fontSize, buttonWidth, buttonHeight, buttonRadius})">
          <svg><use xlink:href="#netid-logo" /></svg>
          <span x-html="netidButton.escape(customText)"></span>
        </button>
      </div>
    </div>
    <div class="grid__cell grid__cell--12">
      <h4>HTML code generation</h4>
      <label class="checkbox" @click="$nextTick(() => { code = expert ? 'expert' : 'embedded'; })">
        <input class="checkbox__input" type="checkbox" x-model="expert" value="true">
        <i class="checkbox__border">
          <i class="checkbox__checker"></i>
        </i>
        <span class="checkbox__label">Expert mode with external CSS and SVG assets</span>
      </label>
      <pre class="source"><code x-text="netidButton.code({text: customText, size, full, code, fontSize, buttonWidth, buttonHeight, buttonRadius})"></code></pre>
      <div x-show="code == 'expert'">
        <div class="admonition info">
          <p>In expert mode, the specified CSS and SVG symbol definition must be implemented into your project accordingly.</p>
          <p>This mode is useful if you are a web developer and multiple netID buttons need to be implemented.</p>
        </div>
        <p>CSS stylesheet</p>
        <pre class="source"><code x-text="netidButton.css()"></code></pre>
        <p>SVG icon as symbol</p>
        <pre class="source"><code x-text="netidButton.svg()"></code></pre>
      </div>
    </div>
  </div>
</div>