# Website Performance


# Middle-end

- Fewer HTTP requests: combine images and use background positioning, concatenate scripts and css, request less during page load
- Use a CDN: static resources that do not require a server to figure out the content
- Expires/Cache-Control Header
- Gzip: compression
- Stylesheets at top: browser will block rendering of content without
- Scripts at bottom
- Avoid CSS expressions
- External JS/CSS
- Fewer DNS lookups
- Minify JS/CSS
- Avoid redirects
- Avoid duplicate scripts
- Etags
- Cacheable AJAX

- smush.it for image optimization
- sprite.me for image sprites

### Architecture
- Middle-end: buffer, a layer that exists between whats happening purely in the front-end and back-end
- SPAs only load HTML once, serve up initial request, hybrid view of some client side and some server side, use javascript templating engine: heres new data give me the new markup, we dont want to make roundtrip to server to ask for new data
- Do least amount of work necessary to get something visible on the screen, and only do more work when forced to by an exception case
- Hybrid approach is better because it allows server to make decision where stuff/markup gets rendered based upon performance conditions like bandwidth and device size, ex: smaller device offload templating work to server, and more capable device like pc have the device take care of work

### Data Validation
- In non javascript back-end, you write stateless data validation rules and also rewrite it in javascript for performance reasons, to respond to the user asap, and we end up writing stateless data validation rules twice
- Write data validation rules once in one language that can run in both places: insert a javascript based middle-end layer on the server like node.js
- Stateful data validation rules like unique email address cannot be done in client because db lives in server side

### AJAX vs Web Sockets
- AJAX is the way to communicate between client and server without a page refresh, it is a full request response cycle at the HTTP layer which opens a new connection on the server and takes up extra HTTP packets and resources. 1684 bytes
- Web Sockets create one initial HTTP request response cycle, then there is a persistent socket between the client and server, 2 way communication. 8 bytes


# Front-end

### Resource loading
- Preloading: load beforehand <link rel="prefetch" href="">
- Lazy Loading: respond to loading requests only when necessary
function scriptLoaded9() {
  // do stuff
}
var src = document.createElement('script');
src.src = 'foobar.js';
document.head.appendChild(scr);
src.onload = scriptLoaded; // on done
src.onreadystatechange = function() {
  if (src.readyState === 'loaded' || src.readyState === 'complete') {
    scriptLoaded();
  }
}
- Parallel Loading: many scripts need to load, preserve execution order, dynamic loading without document.write gives same loading time but vastly quicker document ready event, src.async = false;

### Abstractions
- OO is slower
- ORM layers are good for individual database access and bad for batch operations

### JavaScript Animations
- Performance of animation is better if it's offloaded in CSS than running it in javascript
- CSS has 2 ways to handle movement: transition (automatic calculated animation, starting and ending value for property) and animation

### UI Thread
- JavaScript is single threaded and has asynchronous code through the event loop but does not have parallelism
- Web workers allow a javascript file to explicitly run in its own thread separate from my thread, good for heavy work, downside is communication channel becomes the bottleneck and at the moment the communication channel between the browsesr thread and worker is stream based and is copy only so if sending large amounts of data end up with 2 copies of that data in memory for a brief moment one is in the worker one is in the browser until garbage collector cleans up one, API is just listen for messages and get messages back and information comes back and forth as quickly as the threaded system can handle cause theres no blocking inside the worker
var longThread = new Worker('long.js');
longThread.onmessage = function(e) {
  var answer = e.data;
  // do something with the answer
}
longThread.postMessage({
  question: '...'
});
- Garbage collector comes along and says here are objects that used to have references but no longer do and we need to reclaim that memory, the more often the browser thinks the garbage collector needs to run the more likely your code will be negatively affected performance wise, so write code that creates less garbge collection by
