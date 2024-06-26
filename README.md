# Image protection cookbook
Documentation for AI image protection software.

## What is Magan?
Hundreds of thousands of images are stolen by bots such as Dall-E and Midjourney to train them, causing these models to produce images eerily similar to these images stolen. If you have any kind of image on your website, you need to protect it *now* so that you can maintain your ownership of your art.

You can use the [Magan GUI](https://kendasi.com/magan) to protect these images easily, however if you know a thing or two about technology (or have a proper website admin), you can automise this easily with the Magan API.

## How to use
The Magan API is simple to implement.

### Protecting a new image
To protect an image, make a post request to `https://kendasi.com/magan/api/new.php`, providing the fileUpload POST parameter with the image you wish to protect. For example, in Python, this might look like:
```
import requests
url = "https://kendasi.com/magan/api/new.php"
filename_to_protect = "file.png" # The filename of the image that you want to protect
with open(image_to_protect, "rb") as f: # Open it as a binary file to get the contents so it can be sent to our server
  image_data = f.read()
files = {"image": (filename_to_protect, image_data)}
r = requests.post(url, files=files) # Note that no headers are needed yet
json_response = r.content # This is the data that our server responded with. The next section explains what to do with this.
```
### Showing a protected image
From the response that the previous POST request sends back, you'll need to store it's data then you can use it to present the protected image. The server response from the previous request will return two JSON parameters: `dirname` and `ext`. You can just substitute this URL with those parameters, which will form the URL from which you need to get the image, like so:
```
https://kendasi.com/magan/api/show.php?image=[dirname goes here]&extension=[ext goes here]
```
You can put this into a HTML iframe to present it on your website, like this:
```
<iframe src="[The URL formed above goes here]" style="border: none;"></iframe>
```
Easy!

## Disclaimers
Note that this software is still in early stages. If you find a bug, please report it in the [Issues](https://github.com/ArtPolice/imageprotection-cookbook/issues/) tab, and we'll fix it as soon as possible. This documentation is not under any license and can be used, shared, and modified freely, however the actual software is (currently) closed source and can not be modified, distributed, sold, sublicensed, copied or merged.
