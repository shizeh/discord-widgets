# Discord Widget Guide for Beginners

🇬🇧 **You are in the English version** | 🇫🇷 [Cliquez ici pour accéder à la version française](https://github.com/shizeh/discord-widgets/blob/main/README.FR.md)

This guide explains how I created a custom Discord widget from scratch.

> [!NOTE]
> This guide requires **Visual Studio Code**.
>
> Node.js is **not required** for this method, as we only use the integrated terminal included in Visual Studio Code.

## 1. Create a Discord application

1. Open the [Discord Developer Portal](https://discord.com/developers/home).
2. Go to **Applications**.
3. Click **New Application**.
4. Give your application a name matching your widget.

Examples:

* `Stats`
* `Steam`
* `Letterboxd`

---

## Enable the Social SDK

Before continuing, you need to enable the Social SDK for your application.

1. Go back to the Discord Developer Portal.
2. Select your application.
3. Navigate to:

```text
Games
→ Social SDK
```

4. Fill out the required form.
5. Accept the terms if you are prompted to.
6. Submit the form.

This step is required to access the Social SDK features used by Discord Widgets.

If you skip this step, you may run into issues later during the OAuth2 setup, such as missing scopes or authorization errors.

Once the form has been submitted and accepted, you can move on to the next step of the tutorial.

## 2. Enable the widget editor

The widget editor is hidden by default.

1. Download the `widget-access.txt` file from the repository.
2. Open the page listing all of your Discord applications.
3. Press `F12`.
4. Open the **Console** tab.
5. Paste the contents of `widget-access.txt`.
6. Press `Enter`.

If it works, Discord will unlock the widget editor.

---

## 3. Open the widget editor

1. Go back to your newly created application.
2. Click the **three dots** menu.
3. Open **Games**.
4. Click **Widget**.

You can now start building your widget.

---

## 4. Design your widget

Customize the widget however you like.

Examples:

* Steam statistics
* Last.fm statistics
* Letterboxd profile
* Video game achievements
* Personal statistics

You can customize:

* Images
* Layout
* Labels
* User data fields

Once you are happy with the result, save your changes.

---

## 5. Collect the required information

Before continuing, collect the following information.

### Bot Token

Navigate to:

```text
Bot
```

Copy your Bot Token.

### Application ID

Navigate to:

```text
General Information
```

Copy your Application ID.

### Discord User ID

Enable Developer Mode:

```text
User Settings → Advanced → Developer Mode
```

Then right-click your profile and select:

```text
Copy User ID
```

---

## 6. Save all the information

Create a text file and store:

```text
Application ID:
XXXXXXXXXXXXXXX

Bot Token:
XXXXXXXXXXXXXXX

User ID:
XXXXXXXXXXXXXXX
```

Make sure everything is clearly labeled.

You will need these values later during the setup process.

## 7. Configure OAuth2

Go back to the Discord Developer Portal and open the **OAuth2** section of your application.

### Create a redirect URL

Under **Redirects**, add the following URL:

```text
https://discord.com
```

Click **Save Changes**.

---

### Generate the OAuth2 URL

Scroll down to the **OAuth2 URL Generator** section.

Select the following scopes:

```text
openid
sdk.social_layer
```

After selecting these scopes, a new option called **Select Redirect URL** should appear.

Choose:

```text
https://discord.com
```

from the dropdown menu.

---

### Edit the generated URL

Discord will generate an authorization URL similar to:

```text
https://discord.com/oauth2/authorize?client_id=YOUR_CLIENT_ID&response_type=code&redirect_uri=...
```

Copy this URL.

Before opening it, replace:

```text
response_type=code
```

with:

```text
response_type=token
```

The URL should now contain:

```text
response_type=token
```

---

### Authorize the application

Paste the modified URL into your browser and open it.

Discord will ask you to authorize the application.

Accept all the requested permissions.

This step allows the application to connect to your Discord account and later link your custom widget to your profile.

---

### Verify the authorization

Open Discord and navigate to:

```text
User Settings
→ Authorized Apps
```

Look for your application.

The application should appear with **7 permissions enabled**.

If the application is listed and all permissions have been granted, you are ready to continue the tutorial.

## 8. Publish your widget

Once your widget is finished, go back to the Developer Portal and publish your project.

After publishing:

1. Open **Visual Studio Code**.
2. Click **Terminal** in the top menu.
3. Select **New Terminal**.

You now need to run a command to create your application's identity.

### Important

Before running the command below, replace:

* `ApplicationID` with your Application ID
* `UserID` with your Discord User ID
* `BOT_TOKEN` with your Bot Token
* `Shizeh` with your Discord username

Example:

```text
Shizeh → Your Discord username
ApplicationID → Your Application ID
UserID → Your Discord User ID
BOT_TOKEN → Your Bot Token
```

### Command

```powershell
Invoke-RestMethod -Uri https://discord.com/api/v9/applications/ApplicationID/users/UserID/identities/0/profile -Method PATCH -Headers @{"Content-Type"="application/json"; "Authorization"="Bot BOT_TOKEN";"User-Agent"="DiscordBot (https://github.com/discord/discord-api-docs, 1.0.0)"} -Body '{"username":"Shizeh","data":{"dynamic":[{"type":1,"name":"full_name","value":"Shizeh"}]}}'
```

Make sure to replace `ApplicationID`, `UserID`, `BOT_TOKEN` and `Shizeh` with your own values before running the command.

Paste the command into the terminal, then press Enter.

If no error appears, the identity has been created successfully.

### Final step

Open Discord, then go to:

```text
User Settings
→ Profiles
→ Add Widget
```

Your widget should now appear in the list of widgets.

If it doesn't, try restarting Discord and adding the widget again.

If you followed every step correctly, the widget should appear.

Add it to your profile, then save your changes.

The tutorial is now complete.

> [!TIP]
> If you have any questions or run into issues while following this guide, feel free to reach out.
>
> I'll try to help as much as possible and keep the repository updated based on feedback and commonly reported problems.

---

## Credits

This guide is based on information gathered from various community guides, tutorials and personal experimentation.

The goal of this repository is not to claim credit for the original discoveries, but to provide a simpler and more beginner-friendly explanation.

Many thanks to everyone who contributed information, tutorials and research regarding Discord Widgets.

---

## Resources

Useful links:

* Original guide: [Chloe Cinders](https://chloecinders.com/blog/discord-widgets)
* Discord Developer Portal: [Discord Developer Portal](https://discord.com/developers/home)
* Additional documentation: `LINK_HERE`

---

## Author

Created by **Baptiste (Shizeh)**

GitHub: [Shizeh](https://github.com/shizeh)
