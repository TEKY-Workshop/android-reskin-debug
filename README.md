Reskinning Scribblit
===

Flavors in Android
--- 

Android handles sharing code between different builds using Flavors (gradle term)

~~~ groovy
productFlavors {
    base {
        applicationId "com.interapt.scribblit"
        buildConfigField 'String', 'HOCKEY_APP_ID', '"somestring"'
    }
    newflavor {
        applicationId "com.interapt.scribblit.newflavor"
        buildConfigField 'String', 'HOCKEY_APP_ID', '"someotherstring"'
    }
}
~~~

Change from Android view to Project view.

See folders in src include:

* main - shared code
* base - override for base scribblit
* newflavor - override for newflavor of scribblit

Overriding xml
---

XML files are merged when building with flavors. The main is kept, unless the flavor specifies a value in xml, then it is overridden for the value in the flavor.

*** Demo of merging colors in new flavor of scribblit ***

Configuring Colors
---

Go to `presentation/src/main/res/values/config-colors.xml`

Should look something like this:

~~~~ xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- Theme Colors -->
    <color name="colorTheme1">#39A29B</color>
    <color name="colorTheme2">#F0515C</color>
    <color name="colorTheme3">#3D7C7E</color>
    <color name="colorTheme4">#349791</color>
    <color name="colorTheme5">#0D0D0D</color>
    <color name="colorTheme6">#666666</color>
    <color name="colorTheme7">#9B9B9B</color>
    <color name="colorTheme8">#D7D7D7</color>
    <color name="colorTheme9">#F2F2F2</color>
    <color name="colorTheme10">#FFFFFF</color>
    <color name="colorTheme11">#E7FBFB</color>

    <!-- Specific Colors -->
    <color name="colorHint">#C4C5C4</color>
    <color name="colorTheme2Alpha50">#99F0515C</color>

    <!-- random color palette -->
    <integer-array name="palette">
        <item>0xfff48fb1</item>
        <item>0xffce93d8</item>
        <item>0xff9fa8da</item>
        <item>0xff81d4fa</item>
        <item>0xff80cbc4</item>
        <item>0xffc5e1a5</item>
        <item>0xffffe082</item>
        <item>0xffffab91</item>
    </integer-array>
</resources>
~~~~

Changing one of these colors can have a drastic effect the look of the app

Configuing View specific colors
---
In the project there are many color-* xml files. These represent view specific color configurations.

They can be modified seperately to maintain the current palette but change the colors from that palette that are displayed.

For instances the colors-fab.xml file

~~~ xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="fab">@color/colorTheme2</color>
    <color name="fab_menu_items">@color/colorTheme1</color>
    <color name="fab_menu_icons">@color/colorTheme10</color>
    <color name="fab_menu_item_labels">@color/colorTheme8</color>
    <color name="fab_menu_item_labels_font">@color/colorTheme5</color>
    <color name="fab_menu_background_opened">@color/colorTheme9</color>
</resources>
~~~

You can configure how the fab colors appear from here

*** Workshop changing fab colors ***

Also the colors-login.xml changes the colors displayed on the login screen

~~~ xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="login_bottom_of_sheet_button_font">@color/colorTheme9</color>
    <color name="login_card_place_holder_font">@color/colorTheme8</color>
    <color name="login_card_title_font">@color/colorTheme6</color>
    <color name="login_card_icons_and_inactive_lines">@color/colorTheme8</color>
    <color name="login_active_form_line">@color/colorTheme1</color>
    <color name="login_error_message_font">@color/colorTheme2</color>
    <color name="login_error_form_lines_and_icons">@color/colorTheme2</color>
    <color name="login_typed_font">@color/colorTheme5</color>
    <color name="login_welcome_screen_background">@color/colorTheme11</color>
    <color name="login_pin_code_button_fill_and_dots">@color/colorTheme1</color>
    <color name="login_log_in_buttons">@color/colorTheme1</color>
    <color name="login_create_account_buttons">@color/colorTheme2</color>
    <color name="login_reset_password_font">@color/colorTheme1</color>
</resources>
~~~

*** Workshop changing login colors ***

Configuring Strings and API specific variables
---

These string variables may change based on the customer. They also relate to how to connect to the api/mqtt.

~~~ xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- API -->
    <string name="network_topic_root">scribblit</string>
    <string name="network_mqtt_url"></string>
    <string name="network_mqtt_host"></string>
    <string name="network_mqtt_port"></string>
    <string name="network_mqtt_ports_encrypted">8883</string>
    <string name="network_mqtt_ports_unencrypted">1883</string>
    <string name="api_base_url"></string>
    <string name="log_in_sign_up_success_message">Please check your email to confirm your Scribblit Messaging account</string>

    <string name="support_email_subject">Scribblit Support</string>
    <string name="support_email_to">scribblit@interapthq.com</string>
    <string name="support_intent_chooser_title">Support and Feedback</string>
    <string name="mqtt_api_version">2</string>
    <string name="dialog_message_verify_account">To create your account, enter your valid Scribblit ID number under "Employee ID". If you don\'t know your Scribblit ID, look at your most recent pay stub.</string>
    <string name="tutorial_home_screen_two">Create your first message or topic by tapping the compose button</string>
    <string name="tutorial_home_screen_one">Welcome to Scribblit Messaging</string>
    <string-array name="support_email_copy"></string-array>
</resources>
~~~

There is also strings.xml (way to long to paste here) where other strings used in the project can be configured.

Configuring Features
---

Go to `presentation/src/main/res/values/config-features.xml`

Should look like:

~~~ xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
  <bool name="feature_high_five">true</bool>
  <bool name="feature_topics">true</bool>
  <bool name="feature_pin">true</bool>
  <bool name="feature_fingerprint">false</bool>
  <bool name="feature_welcome_message_introduction">true</bool>
  <bool name="feature_announcements">true</bool>
  <bool name="feature_attachments">true</bool>
</resources>

~~~

Toggling these features will show or hide parts of the UI

Debugging
===

Understanding the layers
---

There are three layers to the andorid Scribblit project:
* Data - Networking, storage
* Presentation - UI
* Domain - Connects Data and Presentation layers by specific logic

Often if there is an issue, the problem will be in the Data or Presentation layers, either an event isn't progated to the view or the data is being mismanaged or there is some unhandled network error.

How/Where to begin debugging
---

Data propogates in this order Presentation -> Domain -> Data and responds in the reverse order Data -> Domain - Presentation.

So determine first if the problem is with data missing or being wrong, check the view layer to make sure it is presenting the data correctly.

Second determine if the data is incorrect to start with.

Third determine if the data is being transformed in the Domain layer.

********* Show Bugged Date Code Demo ***********

