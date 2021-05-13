# Hunt
![Hunt](https://user-images.githubusercontent.com/62492737/118130185-b6906d80-b41a-11eb-8b04-33faaa15e371.jpg)


🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 
🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️Description🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️🧍‍♂️

Hunt is an OSINT tool to extract information from any Google Account using an email.

It can currently extract:

🦌 Owner's name
🦘Last time the profile was edited
🐰  Google ID
🐇 If the account is a Hangouts Bot
🐿️ Activated Google services (YouTube, Photos, Maps, News360, Hangouts, etc.)
🦔Possible YouTube channel
🦇Possible other usernames
🐻Public photos (P)
🐨Phones models (P)
🐰  Phones firmwares (P)
🐇 Installed softwares (P)
🐰 Google Maps reviews (M)
🐇 Possible physical location (M)
🐿️The features marked with a (P) require the target account to have the default setting of Allow the people you share content with to download your photos and videos on the Google AlbumArchive, or if the target has ever used Picasa linked to their Google account.
More info here.

Those marked with a (M) require the Google Maps reviews of the target to be public (they are by default).
🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 🐰 🐇 🐿️ 🦔 🦇🐻 🐨 

👣👣👣👣Installation👣👣👣👣

👣Docker👣
You can build the Docker image with:

docker build --build-arg UID=$(id -u ${USER}) --build-arg GID=$(id -g ${USER}) -t ghunt .
Any of the scripts can be invoked through:

docker run -v $(pwd)/resources:/usr/src/app/resources -ti ghunt check_and_gen.py
docker run -v $(pwd)/resources:/usr/src/app/resources -ti ghunt hunt.py <email_address>

👣👣Manual installation👣👣
👣Make sure you have Python 3.6.1+ installed. (I developed it with Python 3.8.1)
👣Some Python modules are required which are contained in requirements.txt and will be installed below.

1. Chromedriver & Google Chrome
This project uses Selenium and automatically downloads the correct driver for your Chrome version.
⚠️ So just make sure to have Google Chrome installed.

2. Requirements
In the GHunt folder, run:

python -m pip install -r requirements.txt
Adapt the command to your operating system if needed.

Usage
For the first run and sometimes after, you'll need to check the validity of your cookies.
To do this, run check_and_gen.py.
If you don't have cookies stored (ex: first launch), you will be asked for the 4 required cookies. If they are valid, it will generate the Authentication token and the Google Docs & Hangouts tokens.

Then, you can run the tool like this:

python hunt.py myemail@gmail.com
⚠️ I suggest you make an empty account just for this or use an account where you never login because depending on your browser/location, re-logging in into the Google Account used for the cookies can deauthorize them.

Where I find these 4 cookies ?
Log in to accounts.google.com
After that, open the Dev Tools window and navigate to the Storage tab (Shift + F9 on Firefox) (It's called "Application" on Chrome)
If you don't know how to open it, just right-click anywhere and click "Inspect Element".
Then you'll find every cookie you need, including the 4 ones.

![1](https://user-images.githubusercontent.com/62492737/118133394-6a472c80-b41e-11eb-9b33-462d5f952f44.png)



🛡️ Protecting yourself
Regarding the collection of metadata from your Google Photos account:

Given that Google shows "X require access" on your Google Account Dashboard, you might imagine that you had to explicitly authorize another account in order for it to access your pictures; but this is not the case.
Any account can access your AlbumArchive (by default):

![2](https://user-images.githubusercontent.com/62492737/118133437-77641b80-b41e-11eb-8766-f91be70d98b9.jpg)



account-dashboard

Here's how to check and fix the fact that you're vulnerable (wich you most likely are):
Go to https://get.google.com/albumarchive/ while logged in with your Google account. You will be automatically redirected to your correct albumarchive URL (https://get.google.com/albumarchive/YOUR-GOOGLE-ID-HERE). After that, click the three dots on the top left corner, and click on setting

![3](https://user-images.githubusercontent.com/62492737/118133536-95318080-b41e-11eb-942f-baad9a7bd4b4.jpg)


Then, un-check the only option there:

setting

![4](https://user-images.githubusercontent.com/62492737/118133776-d7f35880-b41e-11eb-93dd-cca938314d2e.jpg)

On another note, the target account will also be vulnerable if they have ever used Picasa linked to their Google account in any way, shape or form. For more details on this, read PinkDev1's comment on issue #10.
For now, the only (known) solution to this is to delete the Picasa albums from your AlbumArchive.

Thanks

This tool is based on Sector's research on Google IDs and completed by my own as well.
If I have the motivation to write a blog post about it, I'll add the link here !
