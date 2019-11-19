## 2018 Web Features

##### display content

- implementation:
```css
.class {
  display: content;
}
```

##### Reporting Observer

- purpose: `this gives you to understand what is working and what is not working`
- implementation:
```javascript
const observer = new ReportingObserver((reports, observer) => {
  for (const report of reports) {
    // ... send analytics to someone
  }
})
```

##### Scroll Snap
- purpose: on implementing horizontal scroll views gives you the ability to put the image in the center of the parent
- implementation:
```css
.gallery {
  scroll-snap-type: x mandatory;
  overflow-x: scroll;
  display: flex;
}
.gallery img {
  scroll-snap-align: center;
}
```

##### Site Isolation
##### Named Workers
##### Payment Handlers

##### Conic Gradient
##### AV1 Decoding
##### Async Clipboard
- Solving one of the cliche problems

* Before:
 ```javascript
    button.addEventListener('click', () => {
      const input = document.createElement('input');
      document.body.appendChild(input);
      input.value = text;
      input.focus();
      input.select();
      document.execCommand('copy')
    })
 ```

* after
 ```javascript
  button.addEventListener('click', () => {
    await navigator.clipboard.writeText(text);
  });
  button.addEventListener('click', () => {
    const text = await navigator.clipboard.readText();
    console.log(text);
  });
 ```

##### Typed OM
- purpose: it gives you the type of css properties
- implementation:
```javascript
styleMap.get("opacity") // { value: 1, unit: "number" }
styleMap.get("top") // { value: 1, unit: "px" }
styleMap.get("margin-left") // { value: 10, unit: "percent" }
```
- *Note* You can create your values

##### Update Via Cache
- purpose: we can tell to service worker what should go through the cache and what shouldn't
- implementation:
```javascript
navigator.serviceWorker.register('/service-worker.js', {
  updateViaCache: 'none',
})
```

##### Bitmap Renderer
- implementation:
```javascript
const canvas = document.createElement('canvas');
const context = canvas.getContext('bitmaprenderer');
const image = await createImageBitmap(imageBlob);
context.transferFromImageBitmap(image);
```

##### Web Locks
```javascript
await do_something_without_lock()

await navigator.locks.request('my_resource', async lock => {
  await doSomething();
  await doSomethingElse();
})

await do_something_without_lock()
```
##### Feature Policy

- implementation:
```
Feature-Policy: geolocation 'none'
```

- You can use it for iframes too:
```html
<iframe src="" allow="geolocation 'none'" />
```

##### CSS Paint API
- purpose: you can access to the paint pipeline
```html
<!DOCTYPE html>
<style>
  .main {
    border-image: paint(squircle-corners);
  }
</style>
<main></main>
<script>
CSS.painWorklet.addModule('squircle-corners.js')
</script>
```
```javascript
registerPaint('squircle-corners', class {
  paint(ctx, geometry, properties);
})
```
Note: This code runs off the main thread and the good part is this

##### Web Auth Public Key Credential

##### toggleAttribute
- purpose: toggling an attribute
- implementation;
```javascript
someElement.toggleAttribute('hidden');
```

##### Offscreen Canvas
```javascript
const canvas = new OffscreenCanvas(256, 256);
```
##### Focus Management API
- purpose: you can use it for accessibility and other stuff
- implementation:
```javascript
someElement.focus({ preventScroll: true});
```

##### Sensors
```javascript
const accelerometer = new Accelerometer();
const linearAccelerationSensor = new LinearAccelerationSensor()
const gravitySensor = new GravitySensor();
const gyroscope = new Gyroscope()
const absoluteOrientationSensor = new absoluteOrientationSensor();
const relativeOrientationSensor = new relativeOrientationSensor();
```

#### Lifecycle API
```javascript
document.addEventListener('freeze', (event) => {
  // this page is now frozen
})

document.addEventListener('resume', (event) => {
  // this page has been unfrozen
})

if (document.wasDiscarder) {
  // page was previously discarded by the browser while in a hidden tab
}
```

##### Server Timing
- send it in analytics
```json
Server-Timing: missedCache, cpu; dur=2.4; desc="Processing time"
```
```javascript
let entries = performance.getEntriesByType('resource');
for (const entry of entries) {
  entry.serverTiming[0];
  entry.serverTiming[1];
}
```

##### Trim
```javascript
' hello '.trim();
' hello '.trimStart();
' hello '.trimEnd();
' hello '.trimLeft();
' hello '.trimRight();
```

##### Import Meta Url

##### Regex Named Capture Groups
```javascript
const pattern = /(?<year>d{4})-(?<month>d{2})-(?<day>d{2})/
const result = pattern.exec('2018-12-25');
const { year, month, day} = result.groups;
```

#### Relative Time Format
#### Resize Observer
- purpose: triggering a code when an element just resized.
- implementation:
```javascript
const observer = new ResizeObserver((changes) => {
  for (const {target, contentRect } of changes) {
    // ...
  }
})
observer.observe(element);
```
##### Audio Worklets
```javascript
// app.js
const audioCtx = new AudioContext();
await audioCtx.audioWorklets.addModule('a-node.js');
const track = audioCtx.createMediaElementSource(audioElement);
const aNode = new AudioWorkletNode(context, 'a-node');
track.
  .connect(sNode)
  .connect(audioCtx.destination);

```
```javascript
// a-node.js
class ANode extends AudioWorkletProcessor {
  process(inputs, outputs, parameters) {
    // ...
  }
}
registerProcessor('gain-processor', GainProcessor);
```
##### Cache-Mode
```javascript
const response = await fetch(url, {
  cache: 'reload',
  // or 'default'
  // or 'no-store'
  // or 'no-cache'
  // or 'force-cache'
  // or 'only-if-cached'
})
```
##### Class fields
- *Note*: This is just a syntactic sugar
```javascript
class MyClass {
  x = 4;
  static y = 9;
}
```
