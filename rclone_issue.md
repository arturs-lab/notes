## Old version of rclone and Google discontinued oob (out of band) authentication method
I had an older version of rclone. Existing repos with current tokens work fine. But one of my repos had an expired token and when trying to refresh it, google would not accept API call.
Attempts to refresh token failed with follwoing error message
```
Error 400: invalid_request
The out-of-band (OOB) flow has been blocked in order to keep users secure. Follow the Out-of-Band (OOB) flow migration guide linked in the developer docs below to migrate your app to an alternative method.
Request details: redirect_uri=urn:ietf:wg:oauth:2.0:oob 
```
This is discussed in [google doc](https://developers.google.com/identity/protocols/oauth2/resources/oob-migration)

Even after following instructions in [making-your-own-client-id](https://rclone.org/drive/#making-your-own-client-id) doc and adding client ID to my config, I was still getting same response. I created the ID within [google developer console](https://console.cloud.google.com/apis/dashboard) 

Reading [this thread](https://github.com/rclone/rclone/issues/6000) I noticed that this may be fixed in latest version of rclone.

I downloaded latest release from [github](https://github.com/rclone/rclone/releases/tag/v1.60.1)

And installed it
```yum localinstall rclone-v1.60.1-linux-386.rpm```

Finally I was able to succesfully execute
```rclone config reconnect <drive name>:```
which opened a new browser window, I logged in and confirmed authenticity of the incoming request. After that rclone now can connect to affected account
```rclone ls <name>:/```

Related links<br>
https://github.com/rclone/rclone/issues/321<br>
https://rclone.org/drive/<br>
https://myaccount.google.com/<br>
https://drive.google.com/drive/
