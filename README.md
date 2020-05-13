<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Questions</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__left">
    <div class="stackedit__toc">
      
<ul>
<li><a href="#questions">Questions</a>
<ul>
<li><a href="#ques1.-how-video-streaming-from-url-works.-what-is-hls-">Ques1. How video streaming from URL works. What is HLS ?</a></li>
<li><a href="#ques2.-how-is-video-played-in-android-app-">Ques2. How is video played in Android app ?</a></li>
<li><a href="#ques3.-how-youtube-changes-video-quality-based-upon-internet-connection">Ques3. How Youtube changes video quality based upon internet connection</a></li>
<li><a href="#ques4.-how-does-firebase-database-works">Ques4. How does Firebase database works</a></li>
<li><a href="#ques5.-how-sensex-api-works">Ques5. How sensex API works</a></li>
<li><a href="#ques6.--explain-whatsapp-system-design">Ques6.  Explain whatsapp system design</a></li>
<li><a href="#ques7.-how-whatsapp-compresses-images">Ques7. How whatsapp compresses images</a></li>
<li><a href="#ques8.-what-is-deeplink-">Ques8. What is deeplink ?</a></li>
<li><a href="#ques9.-difference-between-web-sockets-long-polling-and-server-side-events-sse.">Ques9. Difference between web sockets, long polling and Server Side Events (SSE).</a></li>
<li><a href="#ques-10.-difference-between-mainui-thread-and-background-thread.">Ques 10. Difference between Main/UI Thread and background Thread.</a></li>
<li><a href="#ques-11.-how-does-pip-picture-in-picture-works-in-android-applications-">Ques 11. How does PIP (picture in picture) works in android applications ?</a></li>
<li><a href="#ques-12.-briefly-explain-the-following-terms-in-android">Ques 12. Briefly explain the following terms in android</a></li>
</ul>
</li>
</ul>

    </div>
  </div>
  <div class="stackedit__right">
    <div class="stackedit__html">
      <h1 id="questions">Questions</h1>
<p><em>repository URL: <a href="https://github.com/ishanknijhawan/Questions.git">https://github.com/ishanknijhawan/Questions.git</a></em><br>
<em>gist ID: 4771e2b719d987ecc7f512a904fa8445</em></p>
<h2 id="ques1.-how-video-streaming-from-url-works.-what-is-hls-">Ques1. How video streaming from URL works. What is HLS ?</h2>
<p>Answer: When someone streams a video online, he/she connects to the server where that video is stored. The client connects to a URL where that video is stored, and the server starts sending packets, i.e. server sends picture frames to the client’s video player. And as soon as the server has sent enough frames to the client to form a scene, the video starts playing on the client side. In fact, the server always sends extra frames to keep the remaining frames in buffer so that when the client has an unstable internet connection, there are always few extra frames to be played in that time limit when the client’s internet is slow. When the extra frames are also utilized and the client is not being able to receive more packets due to low bandwidth, client sees a buffering screen.</p>
<p>Now, people might upload the video on the server with different formats and there are so many video formats available. And its difficult for the video player to keep track of videos of different formats. Therefore there are some fixed formats for web streaming like smooth streaming (by Microsoft) and HDS (by Adobe). But the most commonly used are <strong>HLS (HTTP Live Steaming)</strong> and <strong>DASH (Dynamic Adaptive Streaming over HTTP)</strong>. After the video is uploaded, there is served side processing of the video into these formats.</p>
<p>HLS is a format which is developed by Apple. Rather than delivering the video in one go, HLS splits it into smaller segments which are contained within the MPEG-2 transport streams. Each segment has about 10 seconds duration with the extension <em>.ts</em>.H264 has to be used as the video codec.</p>
<h2 id="ques2.-how-is-video-played-in-android-app-">Ques2. How is video played in Android app ?</h2>
<p>Answer: Android has it’s own native Mediaplayer class which helps in playing videos. It supports almost all audio and video formats, but the main drawback is that it’s not very customizable. For that, android has what it’s called <em>Exoplayer</em>. Youtube and google’s many other apps which supports video streaming use Exoplayer.<br>
Exoplayer is extremely customizable unlike media player, which is just a black box. It also supports dynamic streaming over HTTP, and smooth streaming of the video played.</p>
<h2 id="ques3.-how-youtube-changes-video-quality-based-upon-internet-connection">Ques3. How Youtube changes video quality based upon internet connection</h2>
<p>Answer: Youtube compresses the data while storing so that it is able to differentiate between different data sizes of the same data, and store it in different sizes in different places across their servers. With the help of data compression, we can save a single piece of data in various sizes. Now when some user streams that video, youtube is able to determine the internet speed of that user by calculating the rate at which their data packets are being transferred. It then uses some basic conditional base code as shown below to determine which quality packets the server has to send the user.</p>
<ul>
<li>0 to 10kbps : Auto 144p</li>
<li>10 to 50kbps : Auto 240p</li>
<li>50 to 100kbps : Auto 360p</li>
<li>100 to 500kbps : Auto 720p</li>
<li>500kbps+ : Auto 1080p</li>
</ul>
<p>So, unless the video quality explicitly specified by the user, youtube follows these algorithms to dynamically adjust the video quality.</p>
<h2 id="ques4.-how-does-firebase-database-works">Ques4. How does Firebase database works</h2>
<p>Answer: Firebase database (or Firebase cloud Firestore) are based upon NoSQL databases. NoSQL is different from SQL (or MySQL or SQLite) database. In SQL we have to define database which store one or more records (which are in the form of tables). Each record has some specific fields and every record must adhere to the same fields.</p>
<p>For example, we have a products table which has the following attributes</p>

<table>
<thead>
<tr>
<th>product_id</th>
<th>description</th>
<th>price</th>
<th>tax</th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>milk</td>
<td>20</td>
<td>2.5</td>
</tr>
<tr>
<td>2</td>
<td>chips</td>
<td>10</td>
<td>1.75</td>
</tr>
</tbody>
</table><p>Now, suppose we want to have a product which also includes a field named quantity, then we can’t simply insert that record without adding that field to the entire table. We can assign that field as <em>null</em> to rest of the elements, but then that would very acquire a lot of useless space.<br>
<strong>NoSQL</strong>, on the other hand has a completely different schema, and Firebase firestore database has a schema very similar to the NoSQL database. Here, the records are stored as <em>documents</em> which are maintained inside a collection. Unlike SQL, a collection can contain documents with different fields. For example we have a chatApp, then there would be one collection named <strong>Users</strong> which stores all the user data, and the other collection can be <strong>Chats</strong> which stores every message as a document with the fields are senderID, receiverID, message, time, etc. Suppose a user wants to add  an image to his message, then we don’t need to add message field in all the documents which do not have an  image attached. We could simply update that particular document with  an image URL. A NoSQL database stores everything as a <strong>JSON</strong> tree.</p>
<p><img src="https://user-images.githubusercontent.com/45118110/80212647-80d4e700-8655-11ea-979c-4543cb1bfa24.PNG" alt="Capture"></p>
<p>An example of Firebase NoSQL database with a 
	and users collection and a document with some fields.</p>
<h2 id="ques5.-how-sensex-api-works">Ques5. How sensex API works</h2>
<p>APIs like displaying stocks, sensex, real time news coverage all use Server Side Events or SSE to keep track of changes in real time, see answer to Ques9.</p>
<h2 id="ques6.--explain-whatsapp-system-design">Ques6.  Explain whatsapp system design</h2>
<p><em>This answer is summary of <a href="https://www.youtube.com/watch?v=vvhC64hQZMk">this</a> video.</em><br>
A chat application should have the following features that I’ll be going to discuss as well as to how these features are implemented.</p>
<ol>
<li>One to one messaging</li>
<li>Group messaging</li>
<li>sent/delivered/read receipts status</li>
<li>online/last seen feature</li>
<li>Image/video sharing</li>
<li>Permanent and temporary chats</li>
</ol>
<p>The user connects through the app by something we call as a <strong>Gateway</strong>. Whenever any activity happens, the gateway is notified about that. We shall discuss all the above mentioned features in detail.</p>
<h3 id="one-to-one-messaging">One to one messaging</h3>
<p>Suppose there are two users, user A and user B. when user A sends a message, it is then updated in gateway A. Now, there can be two ways in which the message from gateway can be sent from gateway A to gateway B (and then to user B). First is, we could store the information of <em>which user is connected to which box</em> in the gateway itself. So, when A sends message to B through gateway A, this gateway has stored that information as to which box this sender and receiver belongs to. But, this is a very expensive task as occupies a lot of memory in the gateway box which could’ve been used in storing more TCP connections coming from the sender. Not just that, this information is duplicated in all the gateways and hence consuming even more memory.</p>
<p>So, the second way is that we want to have that TCP connection as a dumb connection, i.e. when gateway A receives a message, it doesn’t know to whom it belongs, and it always redirects that message to a so called <strong>microservice</strong>. This microservice stores the information which every gateway was storing in the last case, i.e. who is connected to which box. Now when A sends a message using <em>sendMessage(B)</em> (where B is the userID of user B), gateway A forwards it to the microservice. And when this step is done, user A receives a <strong>sent</strong> status or a single tick inside his/her app.  The microservice then sends this message to gatewayB using the information stored inside it.</p>
<p>Now, the gatewayB can’t send this message directly to user B because the server are supposed to be <em>‘client to server’</em> only, and not vice versa. So, there are many ways in which user B can receive the message. One way is <strong>long polling</strong> over HTTP, in which user B asks the gateway every minute or so whether there is any new message or not. And if there is, it receives from the gateway server. But as this is a chat application, we want the message to be sent in realtime. For that, we can <strong>web sockets</strong> over TCP itself. Web sockets help users with peer to peer communication without the need of any Client server in between. For more information regarding sockets, refer Ques 9. So, using web sockets user A can send message directly to user B.</p>
<h3 id="group-messaging">Group messaging</h3>
<h3 id="sentdeliveredread-receipts-status">sent/delivered/read receipts status</h3>
<p>As we discussed earlier how user A sends message to B. We read that as soon as the message is sent to the microservice by the gateway A, user A is updated with a <strong>sent</strong> status. Now, when the micro service sends the message to gatewayB, it waits for B to ask whether there is a message or not (using long polling method), and soon as user B has received a message, user A is updated with a <strong>delivered</strong> status. And as you might have guessed, as soon as B open the chat window of the sender in his/her app, user A is updated with a <strong>seen</strong> status.</p>
<h3 id="onlinelast-seen-feature">online/last seen feature</h3>
<p>This feature is quite straight forward. Let’s say we want to display the last seen of user A in user B’s application. Then we make a microservice which tracks user’s activity. So, whenever user A closes the app, this microservice will be updated with the user A’s timestamp, which will be displayed in user B’s app. Now, if user A has opened the app but hasn’t closed it, we should show user A as <strong>online</strong> instead of last seen. Also, we should set a threshold after user A closes the app. Let’s say it’s been only 3 seconds that user has closed the app, now user B should not be shown that user A has last seen 3 seconds ago, instead it should show online only. So, ideally we can set a last seen threshold of about 20 seconds. Another point, there are times when the app is working in the background and is continuously in touch with the gateway. So we should differentiate this interaction with the user’s interaction with a flag variable. When user is interacting, set flag to say <em>user request</em>. Else set flag to <em>app request</em>, and update last seen only when it is a user request flag.</p>
<h3 id="imagevideo-sharing">Image/video sharing</h3>
<h3 id="permanent-and-temporary-chats">Permanent and temporary chats</h3>
<p>Apps like instagram have a permanent chat feature, i.e. if a user has deleted the app and reinstalls it, all the chats will be restored because all the messages were stored in the cloud, Whereas, apps like Snapchat have a temporary chat feature where the messages are destroyed as soon as user closes the app. Apps like whatsapp also have some sort of temporary messages, because if user A and his user B both have deleted the app then those messages are permanently deleted. All the messages are locally stored inside the app and there is no cloud storage unless the user manually prepares for a chat backup.</p>
<h2 id="ques7.-how-whatsapp-compresses-images">Ques7. How whatsapp compresses images</h2>
<p>Answer: There are basically two types of compression techniques:</p>
<ul>
<li>lossless</li>
<li>lossy</li>
</ul>
<p>Whatsapp uses lossy image compression technique to reduce the size of images to a great extent. Consider an 12MP file with a resolution of around 3000x4000 pixels and a file size of around 5.9MB. Whatsapp reduces it to a file size of mere 220KB, with a resolution of 960x1280 with a 50% compressioin rate. If the image already has this resolution, whatsapp doesen’t scale it because it is already in its minimum resolution which is set by whatsapp. I tried sending a file of size 960x1280 and it kept the same. Let’s see a higher level algorithm of how whatsapp compresses images:</p>
<pre><code>function compressImage(image){
    var originalHeight &lt;- *image height*
    var orignalWidth &lt;- *image width*
    var maxHeight &lt;- 960
    var maxWidth &lt;- 1280
    var imgRatio &lt;- actualWidth/actualHeight
    var maxRatio &lt;- maxWidth/maxHeight
    
    if(actualHeight &gt; maxHeight or actualWidth &gt; maxWidth){
	    if(imgRatio &lt; maxRatio){
			 imgRatio &lt;- maxHeight/originalHeight
            originalWidth &lt;- imgRatio * originalWidth
            originalHeight &lt;- maxHeight   
	    }
    }
    else if(imgRatio &gt; maxRatio){
	    imgRatio &lt;- maxWidth/originalWidth
        originalHeight &lt;- imgRatio * originalHeight
        originalWidth &lt;- maxWidth
    }
    else{
	    originalHeight = maxHeight
	    originalWidth = maxWidth
    }
    //image with updated resolution
    var updatedImage = originalWidth x originalHeight
}
</code></pre>
<h2 id="ques8.-what-is-deeplink-">Ques8. What is deeplink ?</h2>
<h2 id="ques9.-difference-between-web-sockets-long-polling-and-server-side-events-sse.">Ques9. Difference between web sockets, long polling and Server Side Events (SSE).</h2>
<ul>
<li>
<p>Long polling means sending repeated requests to the server, as each new incoming connection is established, the HTTP headers are parsed, a query for new data is performed, and a response is generated and delivered. But rather than having to repeat this process multiple times for every client until new data for a given client becomes available, long polling is a technique where the server chooses to hold a client’s connection to be open for as long as possible, thus delivering a response only after data becomes available or a timeout threshold is reached.</p>
</li>
<li>
<p>On the other hand, web sockets provide a persistent connection between the client and the server, they are built around <strong>TCP/IP</strong> connection. In this, unlike long polling, the client doesn’t have to repeatedly send request to the server. The WebSocket protocol enables interaction between a web browser and a web server with lower overhead than half-duplex alternatives such as HTTP polling, providing real-time data transfer from and to the server. Web sockets have advantages in scenarios in chat application like whatsapp where realtime updation of data is greatly preferred.</p>
</li>
</ul>
<blockquote>
<p><em>Web sockets require user to handle lots of exceptions which were taken of in HTTP long polling on it’s own</em></p>
</blockquote>
<ol>
<li>Server side events or SSE provides the mechanism that allows the server to push data to the client asynchronously as soon as the client-server connection is established.  Since SSE is based on HTTP, it has a natural fit with HTTP/2 and can be combined to get the best of both: HTTP/2 handling an efficient transport layer based on multiplexed streams and SSE providing the API up to the applications to enable push. Therefore it is greatly preferred over long polling and web sockets for building real time apps like sensex display, stock update, Covid19 updates, etc.</li>
</ol>
<h2 id="ques-10.-difference-between-mainui-thread-and-background-thread.">Ques 10. Difference between Main/UI Thread and background Thread.</h2>
<p>In android, the main thread corresponds to all the task the are running on the UI of the application. The main thread is also known as UI thread because all the UI components like button clicks, textviews, populating a recycler view, Activity lifecycle and other UI components happens on the Main Thread/UI Thread.<br>
Now, any other task which can take more than 5 seconds to complete should happen on the background thread. Otherwise it is blocking all the task on the main thread. For example, let’s say we have an app in which we fetch data from an API and display that in a Textview inside our app. Now, if we run both the tasks on the main thread, our app will crash. This happens because the data from the web is extracted separately from the main thread and once it is fetched, then it should load inside the text view or a list. Till then, a progress bar can be shown inside that UI component.</p>
<h2 id="ques-11.-how-does-pip-picture-in-picture-works-in-android-applications-">Ques 11. How does PIP (picture in picture) works in android applications ?</h2>
<h2 id="ques-12.-briefly-explain-the-following-terms-in-android">Ques 12. Briefly explain the following terms in android</h2>
<h3 id="activity">1. Activity</h3>
<p>An activity is a single, focused thing that a user can do. It’s like frames in java. It generally occupies the whole screen of an Android Device. Unlike the <code>main()</code> method in other programming language, an Android app always starts with an Activity. An activity provides the window in which the app draws its UI. This window typically fills the screen, but may be smaller than the screen and float on top of other windows. Generally, one activity implements one screen in an app</p>
<h3 id="fragment">2. Fragment</h3>
<p>A fragment is similar to an activity but it doesn’t necessarily occupy the whole screen of an app, unlike an activity. For example, in <em>Whatsapp</em>, there are three table below the action bar viz <em>chats, status and calls.</em> These tab corresponds to <em>fragments</em> of an app because there is no new screen opening when we are moving from chats screen to calls screen. The tabs and search bar remain at their places and and bottom portion of the screen just slides smoothly to a new section.<br>
This is not the case when you open someone’s chat, however. It then opens a fresh new screen and all the tabs and that search bar is now gone. This is the main key difference between an activity and a fragment.</p>
<h3 id="activity-lifecycle">3. Activity lifecycle</h3>
<p>When the user navigates through the app, in and out of different activities, the <code>Activity</code> instances in your app transition through different states in their lifecycle. Through the different lifecycle callback methods, the user can configure different tasks in different stages of an app. For example, we have a chat app and we want to show when the user is online. We can tell our app that as soon as the user open the main activity, make online variable true, and when the activity pauses, make online false. Or suppose we have a music app, in which we want to convert that song into a sticky notification as soon as user minimised the app, we can do this from the following lifecycle callback methods.</p>
<p><code>onCreate()</code><br>
<em>In the onCreate() method, you perform basic application startup logic that should happen only once for the entire life of the activity.</em></p>
<p><code>onStart()</code><br>
<em>The onStart() call makes the activity visible to the user, as the app prepares for the activity to enter the foreground and become interactive</em></p>
<p><code>onResume()</code><br>
<em>When the activity enters the Resumed state, it comes to the foreground, and then the system invokes the onResume() callback. This is the state in which the app interacts with the user. The app stays in this state until something happens to take focus away from the app.</em></p>
<p><code>onPause()</code><br>
<em>The system calls this method as the first indication that the user is leaving your activity (though it does not always mean the activity is being destroyed); it indicates that the activity is no longer in the foreground (though it may still be visible if the user is in multi-window mode).</em></p>
<p><code>onStop()</code><br>
<em>When your activity is no longer visible to the user, it has entered the <em>Stopped</em> state, and the system invokes the onStop() callback. This may occur, for example, when a newly launched activity covers the entire screen. The system may also call onStop() when the activity has finished running, and is about to be terminated.</em></p>
<p><code>onDestroy()</code><br>
<em>The system invokes this method when either of the following 2 things happen</em></p>
<ul>
<li><em>the activity is finishing (due to the user completely dismissing the activity or due to finish().</em></li>
<li><em>the system is temporarily destroying the activity due to a configuration change (such as device rotation or multi-window mode)</em></li>
</ul>
<img src=" https://static.javatpoint.com/images/androidimages/Android-Activity-Lifecycle.png">
<h3 id="retrofit">4. Retrofit</h3>
<p>Retrofit is a type safe HTTP client developed by Square, the company who also developed libraries like Dagger, OkHTTP and Picasso. Retrofit models REST endpoints and converts them into Java interfaces. Using retrofit, in addition wirh OkHttp, we can asynchronously fetch the data from an API in JSON format and convert it using GSON, and then we can assign that data into a textview or a listview.</p>
<h3 id="dagger2">5. Dagger2</h3>
<p>Suppose we have a class, and it takes parameters as objects which are also objects of some other class. For example, there is a class <code>Car()</code>, which takes 2 parameters, namely <code>Engine()</code> and <code>Wheels()</code>. Then the <code>Engine()</code> and <code>Wheels()</code> are so called dependencies of <code>Car()</code>. Now suppose <code>Engine()</code> class further depends upon say. <code>Piston()</code> and <code>Cylinder()</code> class. Then, if we have to initialize the <code>Car()</code> class, we have to initialize every other class in order to fill in the parameters of the <code>Car()</code> class. This can be very tedious and memory consuming. Therefore Square developed this library called Dagger, a dependency injection library, which injects dependencies at runtime and the user doesn’t have to take care of all the values and parameters in order to satisfy the dependencies of <code>Car()</code> class.</p>
<h3 id="rxjava-doubt">6. RxJava (doubt)</h3>
<p>RxJava is a library which simplifies development focused around threading. A developer need not worry too much about the details of how to perform operations that should occur on different threads. For example, if we want to make a network call using <code>AsyncTask()</code> , we have to</p>
<ol>
<li>Create an inner <code>AsyncTask()</code> subclass in our Activity/Fragment</li>
<li>perform the network operation in the background</li>
<li>take the result of that operation and update the UI in the background.</li>
</ol>
<p>This code, might look simple, but can cause certain bugs namely memory leak. Also, if we want to chain another long operation after network call, it wouldn’t be possible. On the contrary, RxJava uses a different approach. In the RxJava world, everything can be modeled as streams. A stream emits item(s) over time, and each emission can be consumed/observed.</p>
<blockquote>
<p><em>The three O’s of RxJava: Observable, Observer and Operator</em></p>
</blockquote>
<ul>
<li>An Observable is the stream abstraction in RxJava. It is similar to an <strong>Iterator</strong> in that, given a sequence, it iterates through and produces those items in an orderly fashion.</li>
<li>The next component to the Observable stream is the Observer (or Observers) subscribed to it.</li>
<li>Items emitted by an Observable can be transformed, modified, and filtered through Operators before notifying the subscribed Observer objects.</li>
</ul>
<h3 id="kotlin-coroutines">7. Kotlin Coroutines</h3>
<p>In short, Kotlin Coroutines helps to simplify the code which runs asynchronously. In Android, Coroutines help to solve 2 primary issues:</p>
<ul>
<li>Manage long running tasks that might freeze the app if run on main/UI thread.</li>
<li>provide safe calling network or disk operations from main thread.</li>
</ul>
<p>If your app is assigning too much work to the main thread, the app can seemingly freeze or slow down. Network requests, JSON parsing, reading or writing from a database, or even just iterating over large lists can cause your app to run slowly enough to cause slow or frozen UI that responds slowly to touch events. These long-running operations should run outside of the main thread.</p>
<p>Kotlin Coroutines use <strong>Dispatchers</strong> to determine which threads are used for Coroutine execution. To run code outside of the main thread, you can tell Kotlin coroutines to perform work on either the <em>Default</em> or <em>IO</em> dispatcher. In Kotlin, all coroutines must run in a dispatcher, even when they’re running on the main thread.</p>
<p>Kotlin provides 3 Dispatchers in use:</p>
<ol>
<li><code>Dispatchers.Main</code>- use this Dispatcher to run the code on the main Android thread</li>
<li><code>Dispatchers.IO</code>- This dispatcher is optimized to perform disk or network I/O outside of the main thread</li>
<li><code>Dispatchers.Default</code>- This dispatcher is optimized to perform CPU-intensive work outside of the main thread.</li>
</ol>
<h3 id="sqlite-databaseroom-persistence">8. SQLite Database/Room Persistence</h3>
<p>SQLite Database is a mobile version of the MySQL database. SQLite helps to store data locally inside the application, so that when app is destroyed, the data is still persisted. It has all the functions which a normal SQL has like <em>SELECT, INSERT, UPDATE, DELETE, ORDER_BY, FILTER, etc.</em><br>
Room is also a database library, which is part of Android architecture components. According to <a href="http://developers.android.com">developers.android.com</a>, <em>The Room persistence library provides an abstraction layer over SQLite to allow for more robust database access while harnessing the full power of SQLite.</em><br>
Room helps to create a Cache of your app, and store the key frame of the app’s data (just like Firebase snapshot). Room has all the functionality of SQLite and some of the common operation like INSERT, DELETE and UPDATE are per defined inside the library. It reduces a lot of code which has to written in the SQLite database.<br>
Room, when combined with tools like Viewmodel, Repository, Livedata and Kotlin Coroutines can be a very efficient method to implement inside and app and to improve app’s performance.</p>
<h3 id="design-patterns">9. Design Patterns</h3>
<p>Design patterns are reusable solutions to common software problems. They can be broadly classified into three types:</p>
<ol>
<li><strong>Creational Patterns</strong></li>
</ol>
<ul>
<li>
<p><em>Builder</em><br>
Builder pattern separates the construction of a complex object. in this way, the same construction process can create different representations. In Android, the Builder pattern appears when using objects like  <code>AlertDialog.Builder</code></p>
</li>
<li>
<p><em>Dependency Injection</em><br>
Please refer to part 5 of the same Question for the answer.</p>
</li>
<li>
<p><em>Singleton</em><br>
The Singleton Pattern specifies that only a single instance of a class should exist with a global point of access. This works well when modeling real-world objects only having one instance. The Kotlin <code>object</code> keyword is used to declare a singleton, without the need to specify a static instance as in other languages.</p>
</li>
</ul>
<ol start="2">
<li><strong>Structural Patterns</strong></li>
</ol>
<ul>
<li>
<p><em>Adapter</em><br>
An adapter lets two incompatible classes work together by converting the interface of a class into another interface the client expects. For example, RecyclerView extends the Adapter class to bind the view inside it.</p>
</li>
<li>
<p><em>Facade</em><br>
Please refer to part 4 of the same Question for the answer.</p>
</li>
</ul>
<ol start="3">
<li><strong>Behavioral Patterns</strong></li>
</ol>
<ul>
<li>
<p><em>Command</em><br>
The Command pattern lets you issue requests without knowing the receiver. You encapsulate a request as an object and send it off; deciding how to complete the request is an entirely separate mechanism.</p>
</li>
<li>
<p><em>Observer</em><br>
The Observer pattern defines a one-to-many dependency between objects. When one object changes state, all of its dependents are notified and updated automatically. This is a versatile pattern; you can use it for operations of indeterminate time, such as API calls. You can also use it to respond to user input. The <em>RxAndroid</em> framework (aka Reactive Android) will let you implement this pattern throughout your app.</p>
</li>
<li>
<p><em>Model View Controller</em><br>
Also knows as MVC, it refers to the current reigning presentation architectural pattern across several platforms; it’s particularly easy to set your project up in this way on Android. It refers to the three divisions of classes used in this pattern:</p>
</li>
</ul>
<ol>
<li><strong>Model</strong>:  your data classes. If you have  <code>User</code>  or  <code>Product</code>  objects, these “model” the real world.</li>
<li><strong>View</strong>:  your visual classes. Everything the user sees falls under this category.</li>
<li><strong>Controller:</strong>  the glue between the two. It updates the view, takes user input, and makes changes to the model.</li>
</ol>
<p>Dividing your code between these three categories will go a long way toward making your code decoupled and reusable. Additionally, moving as much layout and resource logic as possible into Android XML keeps your View layer clean and tidy.</p>
<ul>
<li>
<p><em>Model View ViewModel</em><br>
This architectural pattern is similar to the MVC pattern; the Model and View components are the same. The ViewModel object is the <em>glue</em> between the model and view layers, but operates differently than the Controller component. Instead, it exposes commands for the view and binds the view to the model. When the model updates, the corresponding views update as well via the data binding. Similarly, as the user interacts with the view, the bindings work in the opposite direction to automatically update the model.</p>
</li>
<li>
<p><em>Clean Architecture</em><br>
Clean Architecture exists at a higher abstraction level than the MVC and MVVM presentation architecture patterns. It describes the overall application architecture: how the various layers of an app (business objects, use cases, presenters, data storage, and UI) communicate with one another.</p>
</li>
</ul>
<h3 id="memory-leak">10. Memory leak</h3>
<p>A memory leak happens when a code allocated memory for an object, but never deallocates it. When a memory leak occurs the Garbage Collector thinks an object is still needed because it’s still referenced by other objects. But those references should have cleared. It can be caused by many reasons like memory leak from Thead, Handler, Asynctask, Singleton, etc.</p>
<h3 id="gradle-build-systems">11. Gradle build systems</h3>
<p>In Android Studio, Gradle is used to build our application projects. Before Android Studio, in Eclipse we used to compile and build the applications using command line tool which was soon taken over by GUI based steps to build and run Android Applications in eclipse using ANT. Every android application development tool has to compile resources, java source code, external libraries and combine them into a final Android Package Kit (APK).</p>
<blockquote>
<p><em><strong>Gradle</strong> is a build system, which is responsible for code compilation, testing, deployment and conversion of the code into <code>.dex</code> files and hence running the app on the device.</em></p>
</blockquote>
<p>There are 2 gradle files inside every android project, one is project level and other is application level. In the build process, the compiler takes the source code, resource, external libraries, JAR files and the <code>AndroidManifest.xml</code>(this contains all the meta data of the) file, and converts them into a <code>.dex</code> file, which includes bytecode. Then <em>APK Manager</em> combines the <code>.dex</code> files and all other resources into single <strong>apk</strong> file.</p>
<h3 id="threads">12. Threads</h3>
<h3 id="threadpool">13. Threadpool</h3>
<h3 id="queries">14. Queries</h3>
<p>Query is a part of <code>androidx.room.Query</code>, is is given by <code>@Query</code> annotation.<br>
As an extension over SQLite bind arguments, Room supports binding a list of parameters to the query. At runtime, Room will build the correct query to have matching number of bind arguments depending on the number of items in the method parameter. For example:</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token annotation punctuation">@Query</span><span class="token punctuation">(</span><span class="token string">"SELECT * FROM song WHERE id IN(:songIds)"</span><span class="token punctuation">)</span>
 <span class="token keyword">public</span> <span class="token keyword">abstract</span> List<span class="token operator">&lt;</span>Song<span class="token operator">&gt;</span> <span class="token function">findByIds</span><span class="token punctuation">(</span><span class="token keyword">long</span><span class="token punctuation">[</span><span class="token punctuation">]</span> songIds<span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>For more information about room, refer Ques. 8</p>
<h3 id="performance-optimization">15. Performance optimization</h3>
<p>Making an android app is not a very challenging task, the thing that makes it challenging is how fast and responsive the app behaves at user’s end. Below are some of the Performance optimization tips that should be kept in mind while designing an Android application:</p>
<ol>
<li>
<p><strong>Avoid Creating Unnecessary Objects</strong><br>
As you allocate more objects in your app, you will force a periodic garbage collection, creating little <em>janks</em> in the user experience. The concurrent garbage collector introduced in Android 2.3 helps, but unnecessary work should always be avoided.</p>
</li>
<li>
<p><strong>Prefer Static over Virtual</strong><br>
If you don’t need to access an object’s fields, make your method static. Invocations will be about 15%-20% faster. It’s also good practice, because you can tell from the method signature that calling the method can’t alter the object’s state.</p>
</li>
<li>
<p><strong>Use static <code>const val</code> for constants</strong><br>
Using the <code>const val</code> directly, we can send that variable directly into forming a <code>.dex</code> file rather than forming an instance of it while compiling.</p>
</li>
<li>
<p><strong>Use enhanced for loop syntax</strong><br>
The enhanced <code>for</code> loop (also sometimes known as “for-each” loop) can be used for collections that implement the <code>Iterable</code> interface and for arrays. With collections, an iterator is allocated to make interface calls to <code>hasNext()</code> and <code>next()</code>. With an <code>ArrayList</code>, a hand written counted loop is about considerably faster, but for other collections the enhanced for loop syntax will be exactly equivalent to explicit iterator usage.</p>
</li>
<li>
<p><strong>Avoid using Floating point</strong><br>
Floating point is about 2 times slower than integer on Android devices. In speed terms, there’s no difference between <code>float</code> and <code>double</code> on the more modern hardware. Space-wise, <code>double</code> is 2 times larger.</p>
</li>
</ol>
<h3 id="profiling">16. Profiling</h3>
<p>Android Profiler is a tool which measures performance of an application in real time. The Android Profiler tools provide data to help us understand how our app uses CPU, memory, network, and battery resources. To open the <strong>Profiler</strong> window, choose <strong>View &gt; Tool Windows &gt; Profiler</strong> or click <strong>Profile</strong>  in the toolbar. 	It continues to fetch the data in the form of a shared timeline until the user disconnects manually. The whole screen looks something like this.</p>
<img src="https://i.pinimg.com/originals/06/c6/97/06c697758639b88d6376cebc9938d061.png">
<h3 id="debugging">17. Debugging</h3>
<p>Android Studio provides a debugger that allows you to do the following and more:</p>
<ul>
<li>Select a device to debug your app on.</li>
<li>Set breakpoints in your Java or Kotlin code.</li>
<li>Examine variables and evaluate expressions at runtime.</li>
</ul>
<h4 id="start-debugging">Start Debugging</h4>
<ol>
<li>Select some breakpoints in your code</li>
<li>Select a device to debug from the dropdown list of devices available (connect via USB or enable an AVD)</li>
<li>In the toolbar, click <strong>Debug</strong>. The output should look something like this,<br>
<img src="https://developer.android.com/studio/images/debug/debugger_2x.png"></li>
</ol>
<h3 id="api">18. API</h3>
<p><strong>A</strong>pplication <strong>P</strong>rogramming <strong>I</strong>nterface, or API in short, is a software intermediary that allows two applications to talk to each other. When you use an application on your mobile phone, the application connects to the Internet and sends data to a server. The server then retrieves that data, interprets it, performs the necessary actions and sends it back to your phone. The application then interprets that data and presents you with the information you wanted in a readable way. This is what an API is - all of this happens via API.</p>
<p>The API also provides a level of security, your smartphone’s data is never fully exposed to the server, and likewise the server is never fully exposed to your phone. Instead, each communicates with small packets of data, sharing only that which is necessary. An API usually contains data in the form of a JSON and it is converted by tools such as GSON to make is usable for the software. An example API can be <a href="https://api.covid19india.org/data.json">Covid 19 India API</a></p>

    </div>
  </div>
</body>

</html>
