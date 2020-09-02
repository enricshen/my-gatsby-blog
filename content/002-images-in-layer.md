---
date: 2020-08-20
title: "Best place to store images with your layer"
cover: "https://miro.medium.com/max/640/1*rGs1UQRTA__tDusA_13p4Q.jpeg"
categories:
    - FME
    - ArcGIS
tags:
    - arcgis online
    - hack

---


![Image for post](https://source.unsplash.com/800x400/?library,storage)

## The Issue

In ArcGIS Online, the most common way to display image thumbnails in the pop-ups is done by adding the image URL in the pop-up configuration.

![Image for post](https://miro.medium.com/max/30/1*96dKS2z6fONln3ZbOROecQ.png?q=20)

![Image for post](https://miro.medium.com/max/991/1*96dKS2z6fONln3ZbOROecQ.png)



The disadvantages of doing it:

- The images are stored on a different web server.
- Your feature layer and the image thumbnails are stored in two different places.
- If the image is removed from that server, you thumbnail link is broken.

So where is the best place to store those images? The answer is:

> In the feature layer itself!

Today I will show you how to use FME to convert images to byte arrays and store them with your feature layer.

## The Solution

The modern web browsers are capable of rendering images from byte arrays.

Instead of using an actual jpeg image url:

```
<img src="http://myimagesite.com/myPhoto.jpg" >
```

The web browsers are able to translate something like this:

```
<img src="data:image/jpeg;base64, /9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAgGBgcGBQgHBwcJCQgKDBQNDAsLDBkSEw8UHRofHh0aHBwgJC4nICIsIxwcKDcpLDAxNDQ0Hyc5PTgyPC4zNDL/2wBDAQkJCQwLDBgNDRgyIRwhMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjL/wAARCALuA+gDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE10KxwRVS0fAkM2JyggkK"
```

to an actual photo:

![Image for post](https://miro.medium.com/max/30/1*LK9NyqOSNoask8acS7gu0w.jpeg?q=20)
