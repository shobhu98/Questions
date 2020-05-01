# Questions

*repository URL: https://github.com/ishanknijhawan/Questions.git*
*gist ID: 4771e2b719d987ecc7f512a904fa8445*
## Ques1. How video streaming from URL works. What is HLS ?
Answer: When someone streams a video online, he/she connects to the server where that video is stored. The client connects to a URL where that video is stored, and the server starts sending packets, i.e. server sends picture frames to the client's video player. And as soon as the server has sent enough frames to the client to form a scene, the video starts playing on the client side. In fact, the server always sends extra frames to keep the remaining frames in buffer so that when the client has an unstable internet connection, there are always few extra frames to be played in that time limit when the client's internet is slow. When the extra frames are also utilized and the client is not being able to receive more packets due to low bandwidth, client sees a buffering screen.

Now, people might upload the video on the server with different formats and there are so many video formats available. And its difficult for the video player to keep track of videos of different formats. Therefore there are some fixed formats for web streaming like smooth streaming (by Microsoft) and HDS (by Adobe). But the most commonly used are **HLS (HTTP Live Steaming)** and **DASH (Dynamic Adaptive Streaming over HTTP)**. After the video is uploaded, there is served side processing of the video into these formats.

HLS is a format which is developed by Apple. Rather than delivering the video in one go, HLS splits it into smaller segments which are contained within the MPEG-2 transport streams. Each segment has about 10 seconds duration with the extension *.ts*.H264 has to be used as the video codec.

## Ques2. How is video played in Android app ?
Answer: Android has it's own native Mediaplayer class which helps in playing videos. It supports almost all audio and video formats, but the main drawback is that it's not very customizable. For that, android has what it's called *Exoplayer*. Youtube and google's many other apps which supports video streaming use Exoplayer.
Exoplayer is extremely customizable unlike media player, which is just a black box. It also supports dynamic streaming over HTTP, and smooth streaming of the video played.
## Ques3. How Youtube changes video quality based upon internet connection
Answer: Youtube compresses the data while storing so that it is able to differentiate between different data sizes of the same data, and store it in different sizes in different places across their servers. With the help of data compression, we can save a single piece of data in various sizes. Now when some user streams that video, youtube is able to determine the internet speed of that user by calculating the rate at which their data packets are being transferred. It then uses some basic conditional base code as shown below to determine which quality packets the server has to send the user.

 - 0 to 10kbps : Auto 144p
 - 10 to 50kbps : Auto 240p
 - 50 to 100kbps : Auto 360p
 - 100 to 500kbps : Auto 720p
 - 500kbps+ : Auto 1080p

So, unless the video quality explicitly specified by the user, youtube follows these algorithms to dynamically adjust the video quality.
## Ques4. How does Firebase database works
Answer: Firebase database (or Firebase cloud Firestore) are based upon NoSQL databases. NoSQL is different from SQL (or MySQL or SQLite) database. In SQL we have to define database which store one or more records (which are in the form of tables). Each record has some specific fields and every record must adhere to the same fields.

For example, we have a products table which has the following attributes
| product_id |description  |	price| tax|
|--|--|--|--|
|1|milk|20|2.5
|2|chips|10|1.75
Now, suppose we want to have a product which also includes a field named quantity, then we can't simply insert that record without adding that field to the entire table. We can assign that field as *null* to rest of the elements, but then that would very acquire a lot of useless space.
**NoSQL**, on the other hand has a completely different schema, and Firebase firestore database has a schema very similar to the NoSQL database. Here, the records are stored as *documents* which are maintained inside a collection. Unlike SQL, a collection can contain documents with different fields. For example we have a chatApp, then there would be one collection named **Users** which stores all the user data, and the other collection can be **Chats** which stores every message as document with the fields are senderID, receiverID, message, time, etc. Suppose a user wants to add a an image to his message, then we don't need to add message field in all the documents which do not have image attached. We could simply update that particular document with the an image URL. A NoSQL database stores everything as a **JSON** tree.  

![Capture](https://user-images.githubusercontent.com/45118110/80212647-80d4e700-8655-11ea-979c-4543cb1bfa24.PNG)

An example of Firebase NoSQL database with a Chat and users collection and a document with some fields.
## Ques5. How sensex API works
APIs like displaying stocks, sensex, real time news coverage all use Server Side Events or SSE to keep track of changes in real time, see answer to Ques9.
## Ques6.  Explain whatsapp system design
*This answer is summary of [this](https://www.youtube.com/watch?v=vvhC64hQZMk) video.*
A chat application should have the following features that i'll be going to discuss as well as to how these features are implemented.

 1. One to one messaging
 2. Group messaging
 3. sent/delivered/read receipts status
 4. online/last seen feature
 5. Image/video sharing
 6. Permanent and temporary chats

The user connects through the app by something we call as a **Gateway**. Whenever any activity happens, the gateway is notified about that. We shall discuss all the above mentioned features in detail.

 ### One to one messaging
 Suppose there are two users, user A and user B. when user A sends a message, it is then updated in gateway A. Now, there can be two ways in which the message from gateway can be sent from gateway A to gateway B (and then to user B). First is, we could store the information of *which user is connected to which box* in the gateway itself. So, when A sends message to B through gateway A, this gateway has stored that information as to which box this sender and receiver belongs to. But, this is a very expensive task as occupies a lot of memory in the gateway box which could've been used in storing more TCP connections coming from the sender. Not just that, this information is duplicated in all the gateways and hence consuming even more memory.

So, the second way is that we want to have that TCP connection as a dumb connection, i.e. when gateway A receives a message, it doesn't know to whom it belongs, and it always redirects that message to a so called **microservice**. This microservice stores the information which every gateway was storing in the last case, i.e. who is connected to which box. Now when A sends a message using *sendMessage(B)* (where B is the userID of user B), gateway A forwards it to the microservice. And when this step is done, user A receives a **sent** status or a single tick inside his/her app.  The microservice then sends this message to gatewayB using the information stored inside it.

Now, the gatewayB can't send this message directly to user B because the server are supposed to be *'client to server'* only, and not vice versa. So, there are many ways in which user B can receive the message. One way is **long polling** over HTTP, in which user B asks the gateway every minute or so whether there is any new message or not. And if there is, it receives from the gateway server. But as this is a chat application, we want the message to be sent in realtime. For that, we can **web sockets** over TCP itself. Web sockets help users with peer to peer communication without the need of any Client server in between. For more information regarding sockets, refer Ques 9. So, using web sockets user A can send message directly to user B.  

### Group messaging

 ### sent/delivered/read receipts status
 As we discussed earlier how user A sends message to B. We read that as soon as the message is sent to the microservice by the gateway A, user A is updated with a **sent** status. Now, when the micro service sends the message to gatewayB, it waits for B to ask whether there is a message or not (using long polling method), and soon as user B has received a message, user A is updated with a **delivered** status. And as you might have guessed, as soon as B open the chat window of the sender in his/her app, user A is updated with a **seen** status.
 ### online/last seen feature
 This feature is quite straight forward. Let's say we want to display the last seen of user A in user B's application. Then we make a microservice which tracks user's activity. So, whenever user A closes the app, this microservice will be updated with the user A's timestamp, which will be displayed in user B's app. Now, if user A has opened the app but hasn't closed it, we should show user A as **online** instead of last seen. Also, we should set a threshold after user A closes the app. Let's say it's been only 3 seconds that user has closed the app, now user B should not be shown that user A has last seen 3 seconds ago, instead it should show online only. So, ideally we can set a last seen threshold of about 20 seconds. Another point, there are times when the app is working in the background and is continuously in touch with the gateway. So we should differentiate this interaction with the user's interaction with a flag variable. When user is interacting, set flag to say *user request*. Else set flag to *app request*, and update last seen only when it is a user request flag.
 ### Image/video sharing
 ### Permanent and temporary chats
 Apps like instagram have a permanent chat feature, i.e. if a user has deleted the app and reinstalls it, all the chats will be restored because all the messages were stored in the cloud, Whereas, apps like snapchat have a temporary chat feature where the messages are destroyed as soon as user closes the app. Apps like whatsapp also have some sort of temporary messages, because if user A and his user B both have deleted the app then those messages are permanently deleted. All the messages are locally stored inside the app and there is no cloud storage unless the user manually prepares for a chat backup.
## Ques7. How whatsapp compresses images
Answer: There are basically two types of compression techniques:
- lossless
- lossy

Whatsapp uses lossy image compression technique to reduce the size of images to a great extent. Consider an 12MP file with a resolution of around 3000x4000 pixels and a file size of around 5.9MB. Whatsapp reduces it to a file size of mere 220KB, with a resolution of 960x1280 with a 50% compressioin rate. If the image already has this resolution, whatsapp doesen't scale it because it is already in its minimum resolution which is set by whatsapp. I tried sending a file of size 960x1280 and it kept the same. Let's see a higher level algorithm of how whatsapp compresses images:

    function compressImage(image){
	    var originalHeight <- *image height*
	    var orignalWidth <- *image width*
	    var maxHeight <- 960
	    var maxWidth <- 1280
	    var imgRatio <- actualWidth/actualHeight
	    var maxRatio <- maxWidth/maxHeight

	    if(actualHeight > maxHeight or actualWidth > maxWidth){
		    if(imgRatio < maxRatio){
				 imgRatio <- maxHeight/originalHeight
	            originalWidth <- imgRatio * originalWidth
	            originalHeight <- maxHeight   
		    }
	    }
	    else if(imgRatio > maxRatio){
		    imgRatio <- maxWidth/originalWidth
            originalHeight <- imgRatio * originalHeight
            originalWidth <- maxWidth
	    }
	    else{
		    originalHeight = maxHeight
		    originalWidth = maxWidth
	    }
	    //image with updated resolution
	    var updatedImage = originalWidth x originalHeight
    }


## Ques8. What is deeplink ?
## Ques9. Difference between web sockets, long polling and Server Side Events (SSE).
- Long polling means sending repeated requests to the server, as each new incoming connection is established, the HTTP headers are parsed, a query for new data is performed, and a response is generated and delivered. But rather than having to repeat this process multiple times for every client until new data for a given client becomes available, long polling is a technique where the server chooses to hold a client’s connection to be open for as long as possible, thus delivering a response only after data becomes available or a timeout threshold is reached.

- On the other hand, web sockets provide a persistent connection between the client and the server, they are built around **TCP/IP** connection. In this, unlike long polling, the client doesn't have to repeatedly send request to the server. The WebSocket protocol enables interaction between a web browser and a web server with lower overhead than half-duplex alternatives such as HTTP polling, providing real-time data transfer from and to the server. Web sockets have advantages in scenarios in chat application like whatsapp where realtime updation of data is greatly preferred.

> *Web sockets require user to handle lots of exceptions which were taken of in HTTP long polling on it's own*
- Server side events or SSE provides the mechanism that allows the server to push data to the client asynchronously as soon as the client-server connection is established.  Since SSE is based on HTTP, it has a natural fit with HTTP/2 and can be combined to get the best of both: HTTP/2 handling an efficient transport layer based on multiplexed streams and SSE providing the API up to the applications to enable push. Therefore it is greatly preferred over long polling and web sockets for building real time apps like sensex display, stock update, Covid19 updates, etc.

## Ques 10. Difference between Main/UI Thread and background Thread.
## Ques 11. How does PIP (picture in picture) works in android applications ?
## Ques 10. How do type-ahead and autosuggestion work ?  
