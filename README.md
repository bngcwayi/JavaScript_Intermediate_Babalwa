# JavaScript_Intermediate_Babalwa
 Bb JAVASCRIPT INTERMEDIATE:JAVASCRIPT FOUNDATIONS
WEEK1:WINDOW EVENTS IN JAVASCRIPT
Day1:26-29September 2023
FRAMES AND WINDOWS:
	POPUPS AND WINDOWS METHOD:is the oldest method of showing additional documents to the user
	basically run this:
	 
	The above example will open a new window
	Most browsers open URLs in a new tabs instead of separate windows
	The initial idea for PopUps was to show additional content without closing  the main window
	But nowadays we have different ways of doing that by using  FETCH to get the content and show it in a dynamically generated <div>, basically we don’t use popups that often
	Its tricky to use PopUps with mobiles devices, wont be able to show simultaneous windows
	PopUps are still useful in certain tasks such as:Authorization.Where they provide a separate window with its own JavaScript environment  and also popup are easy to open. A popup can navigate(change URL)
	Most browsers are blocking popups especially if they are called outside user triggered events such asOnClick
	 
WINDOW.OPEN
	The syntax for opening a PopUp: window.open(url, name, params)
	URL= to load  into a new window
	Name= the name of the new indow
	Params=configuration strings of the new window, contains settings, no spaces in params
	 














ACCESSING POPUP FROM WINDOW
	The open call returns a reference to the new window. 
	It can be used to manipulate its properties, change location and even more.
	 
Accessing window from popup
	The popup may access the opener window as well
	 
Closing a popup
	Use win.close= to close a pop up window
	Win.closed= to double check if the window closed
	Technically, the close() method is available for any window, but window.close() is ignored by most browsers if window is not created with window.open(). So it’ll only work on a popup.
	The closed property is true if the window is closed. That’s useful to check if the popup (or the main window) is still open or not. A user can close it anytime, and our code should take that possibility into account.
	 
Scrolling and resizing
	There are methods to move/resize a window
	 






Scrolling a window
	Scrolling on a window can be done by pixel whether right or down, using coordinates
	 
Focus/Blur on a window
	Theoretically, there are window.focus() and window.blur() methods to focus/unfocus on a window. And there are also focus/blur events that allow to catch the moment when the visitor focuses on a window and switches elsewhere.
	When a user attempts to switch out of the window (window.onblur), it brings the window back into focus. The intention is to “lock” the user within the window.
	 a mobile browser usually ignores window.focus() completely. Also focusing doesn’t work when a popup opens in a separate tab rather than a new window.
	Still, there are some use cases when such calls do work and can be useful.
	For instance:
	When we open a popup, it might be a good idea to run newWindow.focus() on it. Just in case, for some OS/browser combinations it ensures that the user is in the new window now.
	If we want to track when a visitor actually uses our web-app, we can track window.onfocus/onblur. That allows us to suspend/resume in-page activities, animations etc. But please note that the blur event means that the visitor switched out from the window, but they still may observe it. The window is in the background, but still may be visible.





SUMMARY OF DAY1 
	Popup windows are used rarely, as there are alternatives: loading and displaying information in-page, or in iframe.
	If we’re going to open a popup, a good practice is to inform the user about it. An “opening window” icon near a link or button would allow the visitor to survive the focus shift and keep both windows in mind.
	A popup can be opened by the open(url, name, params) call. It returns the reference to the newly opened window.
	Browsers block open calls from the code outside of user actions. Usually a notification appears, so that a user may allow them.
	Browsers open a new tab by default, but if sizes are provided, then it’ll be a popup window.
	The popup may access the opener window using the window.opener property.
	The main window and the popup can freely read and modify each other if they havee the same origin. Otherwise, they can change location of each other and [exchange messages.
	To close the popup: use close() call. Also the user may close them (just like any other windows). The window.closed is true after that.
	Methods focus() and blur() allow to focus/unfocus a window. But they don’t work all the time.
	Events focus and blur allow to track switching in and out of the window. But please note that a window may still be visible even in the background state, after blur.














DAY2:CROSS-WINDOW COMMUNICATION
o	The “Same Origin” (same site) policy limits access of windows and frames to each other.
o	The idea is that if a user has two pages open: one from john-smith.com, and another one is gmail.com, then they wouldn’t want a script from john-smith.com to read our mail from gmail.com. 
o	So, the purpose of the “Same Origin” policy is to protect users from information theft.
o	
SAME ORIGIN
o	Two URLs are said to have the “same origin” if they have the same protocol, domain and port.
o	 
o	JavaScript cross-communication refers to the process of different JavaScript programs or components on a web page exchanging information or messages with each other, even if they are running in separate contexts or iframes. 
o	This is often necessary when you have multiple parts of a web application that need to work together but are isolated from one another for security or organization reasons.



IN ACTION:IFRAME
o	An <iframe> tag  hosts a separate embedded window with its own separate document and window objects
o	We can access them using properties:
o	 
o	When accessing something inside the embedded window, browser checks if the iframe is the same origin, if not, then access is denied
Windows on subdomains: document.domain
o	By definition,  two URLs with different domains have different origins.
o	But if windows share the same second-level domain, for instance john.site.com, peter.site.com and site.com (so that their common second-level domain is site.com), we can make the browser ignore that difference, so that they can be treated as coming from the “same origin” for the purposes of cross-window communication.
o	 
o	URLs and Origins: Every website you visit on the internet has a unique web address called a URL. For example, "site.com" and "john.site.com" are two different web addresses.
o	Same Origin: Normally, web browsers treat web pages from different web addresses as if they come from different places. This is a security measure to prevent one web page from messing with or stealing data from another web page that you have open in your browser.
o	Sharing Data: Sometimes, we want web pages from different web addresses to be able to share information or work together. To do this, we need to tell the browser that even though these pages have different addresses, they should be treated as if they're from the same place (same origin).
o	How to Make It Work: To make this work, if the web pages share the same second-level domain (like "john.site.com" and "peter.site.com" both have "site.com" as their second-level domain), we can make the browser ignore the differences and treat them as the same origin.
o	Setting Document Domain: To make this happen, each web page (window) should include a small piece of code that says: document.domain = 'site.com';. This code tells the browser to consider both "john.site.com" and "peter.site.com" as if they are from "site.com."
o	Benefits: Once this code is added, the web pages can communicate and share information with each other without any restrictions. They are treated as if they come from the same place.
o	Important Note: This trick only works if the web pages actually share the same second-level domain, like "john.site.com" and "peter.site.com." It won't work for web pages from completely different domains.
o	In summary, this code helps web pages from related web addresses work together by making the browser treat them as if they are from the same place, allowing them to share information without restrictions.
Iframe: wrong document pitfall
o	IFrame and Origin: An iframe is like a mini web page inside a main web page. When this mini web page (iframe) is from the same place as the main web page (same origin), we can work with its content.
o	Pitfall: However, there's a tricky thing to be aware of. When we create an iframe, it already has a document (like its own blank page). But, this document is not the same as the one that will eventually load into the iframe.
o	Timing Issue: So, if we try to do something with the iframe's document right away (as soon as it's created), that action will most likely get lost or not work as expected.
o	In simpler terms, imagine the iframe as a TV that's turned on but hasn't tuned into any channel yet. If you try to change the channel immediately, it won't work because the TV is still figuring itself out. You have to wait for it to load the actual channel (content) before you can interact with it effectively.
o	Not-Yet-Loaded Iframe: Imagine you have a special mini-webpage inside a webpage called an iframe. When this iframe is not yet loaded with its content, it's like trying to read a book that hasn't been opened yet. You shouldn't try to do anything with it because it's not ready.
o	Event to Wait For: To know when the iframe is ready to be used, you need to wait for a specific event called iframe.onload. It's like waiting for the book to be fully opened before you start reading it.
o	Challenge: However, this event only happens when everything inside the iframe, including all the pictures, videos, and text, has finished loading. This might take a while, especially for complex web pages.
o	Early Detection: If you want to start doing something with the iframe's content before it's fully loaded (like opening the book before you finish reading it), you can keep checking it at regular intervals using something called setInterval. It's like peeking inside the book every few seconds to see if you can start reading, even if you haven't reached the last page.
o	In simple terms, the message here is: Don't try to work with the content of an iframe until it's fully loaded, which is signaled by the iframe.onload event. If you're impatient and want to do something with it before that, you can keep checking it using setInterval, but be careful not to do anything too early, or it might not work as expected.
Collection: window.frames
o	Getting Window Objects for Iframes: When you have an <iframe> on a webpage, you can get access to its window (like its own little world) in a couple of ways:
o	By Number: You can use window.frames[0] to get the window object for the first <iframe> in the webpage. It's like saying, "Give me the first little world inside this webpage."
o	By Name: If your <iframe> has a specific name, like iframeName, you can use window.frames.iframeName to get the window object for that particular <iframe>. It's like saying, "Give me the little world with the name 'iframeName' inside this webpage."
o	Hierarchy of Iframes: Sometimes, an <iframe> can contain other <iframes> inside it, creating a hierarchy of little worlds. Here are some ways to navigate within this hierarchy:
o	window.frames: This is like a collection of all the "children" windows inside the current <iframe>. It gives you access to the little worlds within.
o	window.parent: This refers to the "parent" window, which is the outer window that contains the current <iframe>. It's like going one level up in the hierarchy to the bigger world.
o	window.top: This points to the very topmost parent window, the main window of the whole webpage. It's like reaching the highest level in the hierarchy, the biggest world that contains everything.
o	So, in simple terms, you can use these methods to navigate and interact with different levels of iframes and their parent windows within a webpage. It's like opening a series of nested dolls, each containing its own little world, and you can jump in and out of them as needed.
The “sandbox” iframe attribute
o	Sandbox Attribute for Iframes - Keeping Things Safe:
o	What is it?: The "sandbox" attribute is like a protective shield for an <iframe> (which is like a mini web page within a web page). It's used to prevent this mini web page from doing certain things that might be risky or untrustworthy.
o	Default Restrictions: When you use the "sandbox" attribute without any specific values, it puts the strictest limitations possible on the <iframe>. It's like saying, "Be very careful, and don't let this mini web page do anything risky."
o	Custom Restrictions: However, you can relax these restrictions by specifying a list of things the <iframe> is allowed to do. You do this by adding values to the "sandbox" attribute, like "allow-forms" or "allow-popups."
o	List of Restrictions: Here are some restrictions you can set:
o	allow-same-origin: By default, the "sandbox" makes sure that the mini web page inside the <iframe> is treated as if it's from a different place, even if it's on the same website. This option removes that restriction
o	allow-top-navigation: It lets the <iframe> change the web address of the main web page that contains it.
o	allow-forms: This allows the <iframe> to submit forms, like when you fill out an online survey or enter your username and password.
o	allow-scripts: It allows the <iframe> to run computer programs (scripts), which can make things happen on the web page
o	allow-popups: This lets the <iframe> open small new windows (pop-ups) on the web page.
o	In simple terms, the "sandbox" attribute is like setting rules for a little playground (the <iframe>). By default, it's a very safe playground, but you can choose to loosen some rules if you trust the content inside the playground. This helps keep your main web page safe while letting the mini web page inside do some specific tasks.
Cross Window Messaging
o	Using postMessage to Talk Between Windows on Different Websites:
o	What is it?: The postMessage tool is like a way for different windows (like web pages) from different websites to talk to each other, even though they come from different places on the internet. This is a way to get around the "Same Origin" rule, which usually stops web pages from different websites from chatting.
o	Safety First: It's important to note that this communication only happens if both windows agree to talk and use special JavaScript functions. This keeps it safe for users because it's not automatic - both sides have to give their consent.
o	Two Parts: This tool has two main parts:
o	postMessage: This is like the method a window uses to send a message to another window. It's like saying, "Hey, I want to send you some information!" To do this, you call win.postMessage(data, targetOrigin).
o	data: This is the actual information you want to send. It can be anything, like text or numbers. If you want to send complex stuff, you need to turn it into text using a special method.
o	targetOrigin: This is like the address of the window you want to send the message to. It's a safety measure to make sure your message only goes to the right place. You can't peek at what's inside the other window, so you need to trust that it's still where you expect it to be.
o	onmessage: To receive a message, the window on the other side needs to be ready to listen for it. It's like having a mailbox where messages arrive. This mailbox has a special handler called onmessage, and it triggers when someone sends a message using postMessage. When this handler triggers, it gets information about the message:
o	data: This is the content of the message, what the other window wanted to tell you.
o	origin: This tells you where the message came from (which website).
o	source: This gives you a way to send a message back to the sender if you need to reply.
o	Using it: To make this work, you set up the onmessage handler using a function called addEventListener. You can't just use window.onmessage, it doesn't work that way.
o	In simple terms, postMessage is like a secret code that lets web pages from different places chat with each other, but they have to agree to talk, and they can only send messages to the right address. This keeps things safe for users while allowing different web pages to cooperate.
DAY 2 SUMMARY
o	To call methods and access the content of another window, we should first have a reference to it.
o	For popups we have these references:
o	From the opener window: window.open – opens a new window and returns a reference to it,
o	From the popup: window.opener – is a reference to the opener window from a popup.
o	For iframes, we can access parent/children windows using:
o	window.frames – a collection of nested window objects,
o	 window.parent, window.top are the references to parent and top windows,
o	 iframe.contentWindow is the window inside an <iframe> tag.
o	If windows share the same origin (host, port, protocol), then windows can do whatever they want with each other.
o	Otherwise, only possible actions are:
o	Change the location of another window (write-only access).
o	Post a message to it.
o	Exceptions are:
o	Windows that share the same second-level domain: a.site.com and b.site.com. Then setting document.domain='site.com' in both of them puts them into the “same origin” state.
o	If an iframe has a sandbox attribute, it is forcefully put into the “different origin” state, unless the allow-same-origin is specified in the attribute value. That can be used to run untrusted code in iframes from the same site.
o	The postMessage interface allows two windows with any origins to talk:
o	The sender calls targetWin.postMessage(data, targetOrigin).
o	If targetOrigin is not '*', then the browser checks if window targetWin has the origin targetOrigin.
o	If it is so, then targetWin triggers the messageevent with special properties:
o	origin – the origin of the sender window (like http://my.site.com)
o	source – the reference to the sender window.
o	data – the data, any object in everywhere except IE that supports only strings.
o	We should use addEventListener to set the handler for this event inside the target window

DAY3:27September23
Introduction to Clickjacking
	Clickjacking in JavaScript, in simple terms, is a deceptive technique where a malicious website or web page tricks a user into clicking on something different from what they perceive. This is typically achieved by overlaying an invisible or partially visible element on top of a legitimate website or button, making the user unknowingly interact with the hidden element.
	For example, a clickjacking attack might involve placing a transparent button over a "Download" button on a trusted website. When the user clicks what they believe to be the legitimate "Download" button, they are actually clicking the hidden button, which can trigger malicious actions without their knowledge or consent, such as downloading malware or making unintended changes to their settings.
	In essence, clickjacking exploits the user's trust in a legitimate website's appearance and functionality to carry out harmful actions without their awareness. It is considered a security vulnerability and is typically addressed through measures like frame-busting scripts or using the X-Frame-Options HTTP header to prevent a webpage from being displayed within an iframe on another site.
	Clickjacking is for clicks, not for keyboard
	The attack only affects mouse actions (or similar, like taps on mobile).
OLD SCHOOL DEFENSES [WEAK]
	The oldest defence is a bit of JavaScript which forbids opening the page in a frame (so-called “framebusting”).
	 
	Framebusting in JavaScript, in simple terms, is a technique used to prevent a webpage from being displayed within a frame or iframe on another website. It's a security measure to protect a website from being loaded in an unauthorized context, such as in a frame on a malicious website.
	Here's how framebusting works:
	A website includes a small piece of JavaScript code in its pages.
	 When a user tries to load the website within a frame on another website, the JavaScript code detects this and takes action.
	The code typically redirects the browser to the website's own URL, effectively breaking out of the frame and displaying the site in its own window or tab.
	This prevents the website's content from being "framed" within another site without the website owner's permission, which can help protect against clickjacking attacks and other unauthorized uses of the website's content. Framebusting ensures that the website is viewed in its intended context, preserving its security and functionality.
	This way is not reliable, will look  some other ways of preventing malicious attacks below
	Blocking top-navigation= Blocking top navigation in the context of clickjacking means preventing a malicious website from tricking a user into navigating to a different webpage without their knowledge or consent. In simple terms, it stops a website from changing the web address (URL) of the user's browser without their permission.
	Here's how it works:
	Clickjacking involves overlaying a deceptive element on a webpage to make the user click on something hidden, like a button, while believing they are interacting with something else, like a legitimate button on a trusted site.
	After the user clicks, the malicious website can attempt to change the URL of the user's browser to a different web page, often a malicious one.
	Blocking top navigation is a security measure that prevents this URL change. It ensures that even if a user clicks on something deceptive, the browser won't navigate to a different webpage without the user explicitly confirming the navigation.
	In essence, it safeguards users from being redirected to potentially harmful websites without their awareness or consent, providing an additional layer of security against clickjacking attacks.
	SANDBOX ATTRIBUTE= In simple terms, when you use the "sandbox" attribute with an iframe in web development, it's like putting the iframe in a protective bubble to restrict what it can do. One of the things this bubble restricts is the ability to change the top-level web page's location, which means you can't make the whole web page navigate to a different website.
	However, you have the option to customize this protection. If you add "sandbox='allow-scripts allow-forms'" to the iframe, you're telling the browser that it's allowed to run scripts and use forms inside the iframe. This relaxes some of the restrictions, making the iframe more interactive.
	But, even with these permissions, you're still preventing the iframe from changing the main web page's location. In other words, the iframe can't make the entire web page navigate to a different website because you've omitted "allow-top-navigation." This is a security measure to ensure that the main web page's location can only be changed by the code outside of the iframe, maintaining control and security over the whole web page.
X-Frame-Options
	The X-Frame-Options header is a server-side header that controls whether a web page can be displayed inside a frame or iframe. It is used as a security measure to prevent clickjacking attacks, where an attacker tricks a user into clicking on something on a malicious website by overlaying it with a legitimate-looking frame.
	The X-Frame-Options header must be sent as an HTTP header and cannot be set using an HTML <meta> tag. If it is found in an HTML <meta> tag, the browser will ignore it.
	The X-Frame-Options header can have three possible values:
	DENY: This value instructs the browser to never show the page inside a frame. This means that the page cannot be embedded in any other website.
	SAMEORIGIN: This value allows the page to be displayed inside a frame only if the parent document comes from the same origin. The "origin" refers to the combination of the protocol, domain, and port of a website. For example, if the parent document is from https://example.com, the page can be displayed inside a frame on https://example.com but not on any other domain.
	ALLOW-FROM domain: This value allows the page to be displayed inside a frame if the parent document is from the specified domain. For example, if the header is set to ALLOW-FROM https://example.com, the page can be displayed inside a frame on https://example.com but not on any other domain.
	It's important to note that the ALLOW-FROM value is not widely supported by all browsers, so it's recommended to use the SAMEORIGIN value for broader compatibility.
	For example, Twitter uses the X-Frame-Options header with the value SAMEORIGIN, which means that its pages can only be displayed inside a frame if the parent document comes from the same origin as Twitter.
SAMESITE COOKIE ATTRIBUTE
	The samesite cookie attribute is used to prevent clickjacking attacks. When a cookie has the samesite attribute, it will only be sent to a website if it is opened directly, not through a frame or iframe from another site. 
	This means that if a site like Facebook has the samesite attribute on its authentication cookie, the cookie will not be sent when Facebook is opened in an iframe from another site. This prevents clickjacking attacks from being successful.
	However, it's important to note that the samesite attribute only has an effect when cookies are used. If a website does not use cookies for authentication, it may still be vulnerable to clickjacking attacks. For example, an anonymous polling website that prevents duplicate voting by checking IP addresses would still be vulnerable to clickjacking because it does not authenticate users using cookies.
	In summary , the samesite cookie attribute helps prevent clickjacking attacks by ensuring that cookies are only sent to the website when it is opened directly, not through a frame or iframe from another site. However, it does not provide protection if the website does not use cookies for authentication.

CLICKJACKING SUMMARY
	Clickjacking is a way to “trick” users into clicking on a victim site without even knowing what’s happening. That’s dangerous if there are important click-activated actions.
	A hacker can post a link to their evil page in a message, or lure visitors to their page by some other means. There are many variations.
	From one perspective – the attack is “not deep”: all a hacker is doing is intercepting a single click. But from another perspective, if the hacker knows that after the click another control will appear, then they may use cunning messages to coerce the user into clicking on them as well.
	The attack is quite dangerous, because when we engineer the UI we usually don’t anticipate that a hacker may click on behalf of the visitor. So vulnerabilities can be found in totally unexpected places.
	It is recommended to use X-Frame-Options: SAMEORIGIN on pages (or whole websites) which are not intended to be viewed inside frames.
	Use a covering <div> if we want to allow our pages to be shown in iframes, but still stay safe.To insert a few words of code, use the <code>tag, for several lines – use <pre>, for more than 10 lines – use a sandbox








DAY 4:ARRAY BUFFER AND BINARY ARRAYS
ArrayBuffer
	In simple terms, an ArrayBuffer in JavaScript is like an empty container that can hold a fixed amount of binary data (zeros and ones). It doesn't store any actual data but provides a space to put binary information. Think of it as an empty box with a specific size where you can later fill in data.
	In web development, binary data is often encountered when working with files (creating, uploading, downloading) or performing tasks like image processing. JavaScript allows us to handle binary data efficiently, although it might seem a bit confusing due to the various classes involved.
	The fundamental binary data object in JavaScript is called an "ArrayBuffer." Think of it as a reference to a fixed-size block of memory. 
	Here's how you create one:
	 
	This line of code allocates a continuous block of memory with 16 bytes and initializes them to zeros.
	It's important to note that an ArrayBuffer is not an array like you might be familiar with in JavaScript. It has some key differences:
	Fixed Length: An ArrayBuffer has a fixed length, and you can't change its size once created.
	Memory Space: It occupies exactly the amount of memory specified during creation, not more or less.
	To access the individual bytes within an ArrayBuffer, you need to use a "view" object. Think of these view objects as "eyeglasses" that provide an interpretation of the bytes stored in the ArrayBuffer.
	Here are a few common view objects:
	Uint8Array: This treats each byte in the ArrayBuffer as a separate number, ranging from 0 to 255. Each of these numbers is an "8-bit unsigned integer."
	Uint16Array: It treats every 2 bytes as an integer, with values ranging from 0 to 65535, known as a "16-bit unsigned integer."
	Uint32Array: It interprets every 4 bytes as an integer, with values from 0 to 4294967295, called a "32-bit unsigned integer."
	Float64Array: This view treats every 8 bytes as a floating-point number with a wide range of possible values.
	So, if you have an ArrayBuffer of 16 bytes, you can choose how to interpret it. You can treat it as 16 separate "tiny numbers," 8 larger numbers (2 bytes each), 4 even larger numbers (4 bytes each), or 2 high-precision floating-point values (8 bytes each).
	In summary, ArrayBuffer is the core binary data object in JavaScript. It represents raw binary data, and to work with it effectively, you use view objects to interpret and manipulate the data as needed.
TypedArray
	In simple terms, a TypedArray in JavaScript is like a set of special tools you can use to work with binary data stored in an ArrayBuffer. 
	These tools help you interpret and manipulate the data in specific ways, treating it as numbers or other data types, making it easier to work with binary information.
	They are much more like regular arrays: have indexes and iterable.
	TypedArray in JavaScript is like a collection of tools for handling binary data efficiently. These TypedArrays are similar to regular arrays, meaning they have indexes and can be iterated over.
	There are different ways to create TypedArrays, and they behave differently based on how you create them:
	If you provide an ArrayBuffer as an argument, the TypedArray is created to work with that specific memory space. You can also specify a starting position (byteOffset) and a length to work with only a portion of the ArrayBuffer.
	If you provide an array or array-like object, a TypedArray of the same length is created, and the data is copied into it. This is handy for initializing the TypedArray with existing data.
	If you provide another TypedArray, a new TypedArray of the same length is created, and values are copied from the source TypedArray. The values may be converted to match the new data type if necessary.
	If you provide a numeric argument (length), it creates a TypedArray with the specified number of elements. The size in bytes of each element is determined by the data type, and the total byte length is calculated accordingly
	If you create a TypedArray without any arguments, it creates an empty TypedArray with zero elements.
	To access the underlying ArrayBuffer, you can use properties like arr.buffer, which references the ArrayBuffer, and arr.byteLength, which tells you the length of the ArrayBuffer.
	Here are some common TypedArray types:
	Uint8Array, Uint16Array, Uint32Array: For unsigned integer numbers of 8, 16, and 32 bits, respectively.
	Uint8ClampedArray: For 8-bit integers that are "clamped" to a specific range upon assignment.
	Int8Array, Int16Array, Int32Array: For signed integer numbers, which can be negative.
	Float32Array, Float64Array: For signed floating-point numbers of 32 and 64 bits, respectively.
	It's important to note that JavaScript doesn't have single-valued types like "int" or "int8" as seen in other programming languages. TypedArrays are not arrays of individual values but views on an underlying ArrayBuffer, which makes them efficient for working with binary data.
Out-of-bounds behaviour
	out-of-bounds behavior in JavaScript refers to what happens when you try to access an element in an array or collection using an index that doesn't exist within that array or collection.
	Imagine you have an array with five elements, and you try to access the sixth element by using an index of 5. This is considered an out-of-bounds access because there is no element at that index. 
	In JavaScript, when you perform such an out-of-bounds access, you typically get an "undefined" result, meaning there is no value at that location in the array.
TypedArray methods
	TypedArrays in JavaScript behave a lot like regular arrays in many ways. You can use familiar methods like iterate (loop through), map (transform elements), slice (get a portion), find (locate an element), and reduce (aggregate values).
	However, there are some differences:
	No splice: You can't remove or "delete" elements from a TypedArray because they are views on a fixed, continuous block of memory. The only thing you can do is assign a value of zero to replace an element.
	No concat method: TypedArrays don't have a built-in way to combine or concatenate them directly.
	In addition to the regular array methods, there are two special methods for TypedArrays:
	arr.set(fromArr, [offset]): This method copies all elements from fromArr into arr, starting at a specified position (offset). By default, it starts from the beginning (offset 0).
	arr.subarray([begin, end]): This method creates a new view of the same data type, but only for a specific portion of the TypedArray, defined by the begin and end positions. Unlike slice, it doesn't copy the data; it just provides a different view for working with a specific part of the data.
	These additional methods enable you to copy data between TypedArrays, create new views on existing data, and manipulate TypedArrays effectively while taking into account their underlying memory structure.

DATAVIEW
	 DataView in JavaScript is like a versatile tool for reading and interpreting binary data stored in an ArrayBuffer. It's "untyped," meaning you can use it to access data at any position and in any data format within the ArrayBuffer.
	Here's how it works:
	Underlying ArrayBuffer: DataView needs an existing ArrayBuffer with the binary data. Unlike typed arrays, it doesn't create its own buffer; you must provide one.
	Byte Offset: You can specify a starting position (byteOffset) within the ArrayBuffer where the DataView should begin reading data. By default, it starts at the beginning (byteOffset 0).
	Byte Length: You can also specify how many bytes the DataView should cover (byteLength). By default, it extends until the end of the buffer.
	Now, here's where DataView differs from typed arrays:
	Typed arrays have a fixed data format determined when you create them (e.g., Uint8Array, Uint16Array). All elements in the array must follow that format.
	DataView, on the other hand, allows you to choose the data format (like 8-bit or 16-bit) at the time you read the data, using methods like .getUint8(i) or .getUint16(i). This means you can read different parts of the data in various formats within the same ArrayBuffer.
	So, in summary, DataView is like a flexible reader that can access binary data in any format at any position within an ArrayBuffer, making it highly adaptable for working with diverse data structures.
SUMMARY
	ArrayBuffer is the core object, a reference to the fixed-length contiguous memory area.
	To do almost any operation on ArrayBuffer, we need a view.
	It can be a TypedArray:
	Uint8Array, Uint16Array, Uint32Array – for unsigned integers of 8, 16, and 32 bits.
	Uint8ClampedArray – for 8-bit integers, “clamps” them on assignment.
	Int8Array, Int16Array, Int32Array – for signed integer numbers (can be negative).
	Float32Array, Float64Array – for signed floating-point numbers of 32 and 64 bits.
	Or a DataView – the view that uses methods to specify a format, e.g. getUint8(offset).
	In most cases we create and operate directly on typed arrays, leaving ArrayBuffer undercover, as a “common discriminator”. We can access it as .bufferand make another view if needed.
	There are also two additional terms, that are used in descriptions of methods that operate on binary data:
	ArrayBufferView is an umbrella term for all these kinds of views.
	BufferSource is an umbrella term for ArrayBuffer or ArrayBufferView.
