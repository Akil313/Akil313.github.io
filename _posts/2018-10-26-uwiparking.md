---
layout: posts
title: "Computer Vision Parking Tracker"
date: 2018-10-27
---

Hello everyone. Seeing that this is my first blog post, I hope to be very free with my writing and just create something enjoyable for you to read. Enjoy.

# About the Project
This project is mainly being done for my 'Software Engineering 2' course at my university, The University of the West Indies (UWI). There were not many restrictions in what we could work on but the biggest focus of the project was for us to adhere to the SCRUM methodology of software development.

The project my group decided on was to create a software that could recognize cars in a car park, specifically a carpark from my university and recognize how many parking spots were taken up. Then to take the information gathered and present this in a public medium like a web app, to students of UWI.

# Post 1
## 28/10/2018
Quite a bit has happened since the beginning of this project but I sadly didn't have it all well documented under dates so under this post, I'll cover everything notable that's happened for me.

### Software Development Process
So the main requirement of this project is to follow the SCRUM agile development model. Without going into specific terminology, it seems to be one or the more informal models, or rather, more interactive models.

Of all the models I've studied for this course, I think SCRUM is definitely my favourite because it doesn't feel as strict. It may be because I'm just doing this with a couple of friends, but I also like the idea of the regular quick meetings, being able to get together and discuss progress and even share ideas.

To get the requirements, one person had to act as the 'Product Manager' and list requirements but honestly, everyone in the group listed requirements just so we could get the best out of the system. To be fair though, the product manager started it off.

This is the result of developing our product and sprint backlog:
![Prod Backlog](/assets/images/pblog.PNG)

#Post 2
## 13/11/2018
Its been too long since I've updated this blog but better late than never?

So since the last post, there's been notable progress although there should have been more.

Firstly ill tart with the members of my group, our progress, challenges and other factors affecting the completion of the project.
From the SCRUM methodology, this is called the 'Project Retrospect'

##Project Retrospect



Next I'll talk about what I've been doing for the Raspberry Pi

##Raspberry Pi code

Sadly we haven't gotten into the mean of the Pi code which is the computer vision to recognize the number of cars but one step at a time.

Firstly I needed to learn to send data from the Pi to Firebase Cloud Firestore. Firsestore is a NoSQL document database which I personally feel to be an improvement on the existing Firebase Realtime Database in terms of usability. My goal was just to be able to send data from this program to Firestore so that it would update the [WebApp](https://uwi-park-tracker.firebaseapp.com/) we had created for it.

The first step was, obviously, to install all the dependencies and libraries so that we could perform these functions. After the setup phase, I went on to write basic code to see if I can pull values I put into Firestore.

After some reading and tinkering I was able to create code to change the values of some data in Firestore periodically. For testing I had the values change every 10 seconds but this probably wont be the value used for the product.

```python
def activate():

    tgr_ref = uwi.document(u'TGR')

    while True:

        time.sleep(10)
        print("Sending new info")
        parkingLots[0].setTSpaces(parkingLots[0].tSpaces + 5)
        tgr_ref.update({u'taken_spaces' : parkingLots[0].tSpaces})
        tgr_ref.update({u'parking_spaces': 55})

        tgr = tgr_ref.get()
        print("Available spaces:", tgr.to_dict())

        time.sleep(10)
        print("Sending new info")
        parkingLots[0].setTSpaces(parkingLots[0].tSpaces - 5)
        tgr_ref.update({u'taken_spaces' : parkingLots[0].tSpaces})
        tgr_ref.update({u'parking_spaces': 50})

        tgr = tgr_ref.get()
        print("Available spaces:", tgr.to_dict())
```

Which basically gave me this. The data isn't properly formatted but you can see that there is a value that changes between 50 and 55 every 10 seconds which is reflected in Firestore.

![Basic Output](/assets/images/basic_out.PNG)
