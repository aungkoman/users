# users
Firebase Auth ကို သုံးပြီး website မှာ user တွေရဲံ email verification လုပ်ဖို့ ဘာတွေလိုမလဲ? ဘယ်စာတွေ ဖတ်ရမလဲ?

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Users</title>
</head>

<body>
    <!-- Insert these scripts at the bottom of the HTML, but before you use any Firebase services -->

    <!-- The core Firebase JS SDK is always required and must be listed first -->
    <script src="https://www.gstatic.com/firebasejs/8.6.2/firebase-app.js"></script>

    <!-- TODO: Add SDKs for Firebase products that you want to use
     https://firebase.google.com/docs/web/setup#available-libraries -->
    <script src="https://www.gstatic.com/firebasejs/8.6.2/firebase-analytics.js"></script>
    <!-- all we need to add is this service (firebase-auth) -->
    <script src="https://www.gstatic.com/firebasejs/8.6.2/firebase-auth.js"></script>

    <script>
        // Your web app's Firebase configuration
        // For Firebase JS SDK v7.20.0 and later, measurementId is optional
        // this configuration can get in your firebase console project setting page.
        var firebaseConfig = {
            apiKey: "AIzaSyBgCKPiwILkebeUg0as3kRIXw8jHzXTz5k",
            authDomain: "miyabibonsaisample.firebaseapp.com",
            projectId: "miyabibonsaisample",
            storageBucket: "miyabibonsaisample.appspot.com",
            messagingSenderId: "360077871752",
            appId: "1:360077871752:web:f8d0a00edf37c69b99ed3d",
            measurementId: "G-M4DLCQLWFZ"
        };
        // Initialize Firebase
        firebase.initializeApp(firebaseConfig);
        firebase.analytics();

        // this setting refer from https://firebase.google.com/docs/auth/web/email-link-auth
        // dynamic link can get from firebase console left menu -> dynamic link and create new one
        // later , we need to verified our domain name
        var actionCodeSettings = {
            // URL you want to redirect back to. The domain (www.example.com) for this
            // URL must be in the authorized domains list in the Firebase Console.
            url: 'https://miyabibonsai.com/?email_verified=1234',
            // This must be true.
            handleCodeInApp: true,
            iOS: {
                bundleId: 'com.example.ios'
            },
            android: {
                packageName: 'com.example.android',
                installApp: true,
                minimumVersion: '12'
            },
            dynamicLinkDomain: 'miyabibonsai.page.link'
        };

        function signIn(email, actionCodeSettings) {
            console.log('signIn call with email ' + email);
            firebase.auth().languageCode = 'en'; // 'fr' for frence, 'ja' for japan, 'my' for Myanmar
            firebase.auth().sendSignInLinkToEmail(email, actionCodeSettings)
                .then(() => {
                    console.log('signInLInkToEmail sent to ' + email);
                    // The link was successfully sent. Inform the user.
                    // Save the email locally so you don't need to ask the user for it again
                    // if they open the link on the same device.
                    window.localStorage.setItem('emailForSignIn', email);
                    // ...
                })
                .catch((error) => {
                    var errorCode = error.code;
                    var errorMessage = error.message;
                    // ...
                    console.log('signInLinkToEmail error');
                    console.log(error);
                });
        }

        // hawin.jp@gmail.com
        //signIn("hawin.jp@gmail.com", actionCodeSettings);
        signIn("aungkomantech@gmail.com", actionCodeSettings);

        /*
            email verified ဖြစ်တဲ့အခါ ဒါမျိုး ရလာမယ်
            https://mmsoftware100.com/?email_verified=1234&apiKey=AIzaSyBgCKPiwILkebeUg0as3kRIXw8jHzXTz5k&oobCode=5l9aPTjtyn2V-DjBYz4PCTP85WkJFQnSIlriQrq0DGMAAAF5qMWmEw&mode=signIn&lang=en

            https://mmsoftware100.com/?email_verified=1234
            &
            apiKey=AIzaSyBgCKPiwILkebeUg0as3kRIXw8jHzXTz5k
            &
            oobCode=5l9aPTjtyn2V-DjBYz4PCTP85WkJFQnSIlriQrq0DGMAAAF5qMWmEw
            &
            mode=signIn
            &
            lang=en

            apiKey ရယ် oobCode ရယ်။
            ဒါတွေကို သုံးပြီး ဒီ email ဟာ verified ဟုတ်မဟုတ် ဆာဗာ side မှာ ဘယ်လိုပြန်စစ်ကြမလဲ?

            ဒီမှာတော့ ဒီလိုရေးထားတယ်
            https://firebase.google.com/docs/auth/custom-email-handler

            email action halder page က ဒါတွေကို ကြိုတင်ပြင်ဆင်ထားရမယ်
            mode = resetPassword || recoverEmail || verifyEmail
            oobCode	= A one-time code, used to identify and verify a request
            apiKey =	Your Firebase project's API key, provided for convenience
            continueUrl	= This is an optional URL that provides a way to pass state back to the app via a URL. This is relevant to password reset and email verification modes. When sending a password reset email or verification email, an ActionCodeSettings object needs to be specified with a continue URL for this to be available. This makes it possible for a user to continue right where they left off after an email action.
            lang = ဒါလည်းပဲ optional ပါပဲ။ ( email ကို language ပြောင်းလို့ရတယ် ဆိုတဲ့ သဘော , email action မလာခင်မှာ ဒါမျိုး သတ်မှတ်ထားလို့ရမယ်။
            firebase.auth().languageCode = 'fr';.
            )

            client side မှာတင် စစ်လို့ရတဲ့သဘော
            

        
         */
    </script>
</body>
</body>

</html>
``
