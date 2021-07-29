# Channel Messaging (MessageChannel)

- [https://developer.mozilla.org/en-US/docs/Web/API/Channel_Messaging_API/Using_channel_messaging](https://developer.mozilla.org/en-US/docs/Web/API/Channel_Messaging_API/Using_channel_messaging)
- [https://developer.mozilla.org/en-US/docs/Web/API/SharedWorker](https://developer.mozilla.org/en-US/docs/Web/API/SharedWorker)

> The Channel Messaging API allows two separate scripts running in different browsing contexts attached to the same document (e.g., two IFrames, or the main document and an IFrame, or two documents via a SharedWorker) to communicate directly, passing messages between one another through two-way channels (or pipes) with a port at each end.
>
> __This feature is available in Web Workers__

"Channel Messaging API는 다른 browing context에서 실행되는 다른 scripts가 서로 직접적으로 통신할수 있도록 통로를 만들어준다.  
(ex: 두개의 IFrames, main document & IFrame, SharedWorker를 통한 두개의 documents)"

> Channel messaging is mainly useful in cases where you've got a social site that embeds capabilities from other sites into its main interface via iframes, such as games, address book, or an audio player with personalized music choices.

"Channel Messaging은 보통 소셜 사이트에서 내포하고 있는 다른 사이트의 기능을 iframe으로 제공할때 많이 사용된다"

## 예제

[https://github.com/mdn/dom-examples/tree/master/channel-messaging-multimessage](https://github.com/mdn/dom-examples/tree/master/channel-messaging-multimessage)

### index.html

```js
var input = document.getElementById('message-input');
var output = document.getElementById('message-output');
var button = document.querySelector('button');
var iframe = document.querySelector('iframe');

var channel = new MessageChannel();
var port1 = channel.port1;

// Wait for the iframe to load
iframe.addEventListener("load", onLoad);

function onLoad() {
  // Listen for button clicks
  button.addEventListener('click', onClick);

  // Listen for messages on port1
  port1.onmessage = onMessage;

  // Transfer port2 to the iframe
  iframe.contentWindow.postMessage('init', '*', [channel.port2]);
}

// Post a message on port1 when the button is clicked
function onClick(e) {
  e.preventDefault();
  port1.postMessage(input.value);
}

// Handle messages received on port1
function onMessage(e) {
  output.innerHTML = e.data;
  input.value = '';
}
```

Iframe의 load에:

1. 버튼 콜백을 달아준다
2. port1에 메세지 콜백을 달아준다 (onMessage)
3. port2를 iframe에 넘겨준다 (iframe.contentWindow.postMessage('init', '*', [channel.port2]))

#### iframe.contentWindow.postMessage('init', '*', [channel.port2])

arguments:

- 'init': 보내는 메세지. port transefer에는 필요없지만 그냥 'init'으로 넣어놓음

- '\*': 이 메세지가 보내지는 origin. '\*' 은 모든 origin을 뜻한다.

- [channel.port2]: 받는 browsing context 입장에서 소유권을 가져가는 오브젝트. 여기서는 channel.port2가 되겠다.

### page2.html

```js
var list = document.querySelector('ul');
var port2;

// Listen for the initial port transfer message
window.addEventListener('message', initPort);

// Setup the transferred port
function initPort(e) {
  port2 = e.ports[0];
  port2.onmessage = onMessage;
}

// Handle messages received on port2
function onMessage(e) {
  var listItem = document.createElement('li');
  listItem.textContent = e.data;
  list.appendChild(listItem);
  port2.postMessage('Message received by IFrame: "' + e.data + '"');
}
```

IFrame의 이벤트의 반응해 main에 영향을 줄수 있다.


### React

```js
  // DOM and Worker environments.
  // We prefer MessageChannel because of the 4ms setTimeout clamping.
  const channel = new MessageChannel();
  const port = channel.port2;
  channel.port1.onmessage = performWorkUntilDeadline;
  schedulePerformWorkUntilDeadline = () => {
    port.postMessage(null);
  };
```

리액트 라이브러리에서는 scheduler가 MessageChannel api를 사용해 동작하는것을 볼수 있다.

[돌아가기](/README.md)
