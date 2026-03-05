# Activation

> **YouTube**
>
> Watch videos which show how to activate the [JS components](https://www.youtube.com/watch?v=pMb07Sq_Q_Y&list=PL-72PPAq-3SXppExw44xlnkEo3kVV1iC7&index=3). Subscribe to the [Stimulsoft channel](https://www.youtube.com/user/StimulsoftVideos) to find out about the new video lessons uploaded. Leave your questions and suggestions in the comments to the video.

After purchasing a Stimulsoft product, you need to activate the license for the components you are using. You can do this by specifying a license key or by downloading a file with the license key. Below is an example of activating the **StiDesigner** or **StiViewer** components.


**index.html**

```html
...
function Start() {

    //Activation with using license code
    Stimulsoft.Base.StiLicense.Key = "Your activation code...";
        
    //Activation with using license file
    Stimulsoft.Base.StiLicense.loadFromFile("license.key");    
}
...
```

You can get a license key or download a file with [a license key in the user's account](https://devs.stimulsoft.com/). To log in to your account, please use the username and password specified when purchasing the product.


> **Information**
>
> Please note that, due to security policies of the web browser, downloading the license file from the local storage will not be possible.
