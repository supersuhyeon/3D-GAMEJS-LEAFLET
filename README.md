![ezgif com-gif-maker (13)](https://user-images.githubusercontent.com/94214512/212603931-f1515cbc-1deb-4d8a-a760-ad205ed7bf24.gif)<br>
This is a 3D interactive leaflet that I made for a section named JS game on my portfolio website.<br>
I was inspired by Squid Game, so the overall design is dark, with the famous circle, triangle, and square business card as a leaflet.<br>
[Suhyeon Kim portfolio website](https://suhyeonkim-portfolio.netlify.app/)<br>
[3D-LEAFLET](https://magenta-brioche-9db893.netlify.app/)

### Languages

HTML CSS Javascript

### Features

1. Hand FOLLOWS the cursor so that it moves smoothly<br>
   ![handreadme](https://user-images.githubusercontent.com/94214512/212618736-bbd5016c-db65-4df2-b3f1-a5c778190be9.png)

```css
.hand {
  position: absolute;
  width: 400px;
  z-index: 10;
  /* when the browser loads, this will be the default position of the hand element */
  left: 70%;
  top: 70%;
}

.hand img {
  transition: 1s;
  /* when the page is zoomed in, the hand should not be scaled from the center so its origin value should be changed to avoid blocking the cursor. */
  transform-origin: left top;
}

.zoom-in .hand img {
  transform: scale(2);
}
```

```js
const hand = document.querySelector(".hand");

//distance
let distX;
let distY;

// hand position (which is the object relative to the mouse cursor's position)
const handPos = { x: 0, y: 0 };
// mouse's cursor position
const targetPos = { x: 0, y: 0 };

function render() {
  distX = targetPos.x - handPos.x;
  distY = targetPos.y - handPos.y;
  handPos.x = handPos.x + distX * 0.1;
  handPos.y = handPos.y + distY * 0.1;
  hand.style.transform = `translate(${handPos.x - 60}px,${handPos.y + 30}px)`;
  requestAnimationFrame(render); //keeps making the distance short
}
render();

window.addEventListener("mousemove", (e) => {
  targetPos.x = e.clientX - window.innerWidth * 0.7; // due to the hand's default position
  targetPos.y = e.clientY - window.innerHeight * 0.7;
});
```

2. Send email from a static HTML by using google Apps <br>[guideline github](https://github.com/dwyl/learn-to-send-email-via-google-script-html-no-server#how)<br>
   ![ezgif com-gif-maker (62)](https://user-images.githubusercontent.com/94214512/212614402-f3b97e8b-f283-4ef0-be2b-3f6c0f5a41aa.gif)<br>
   I followed these guidelines and added more functions to check for a vaild email address and disabling the button. It was really good to see that I can retrieve the email addresss from my personal email and have a Google sheet update in realtime.

```js
  function handleFormSubmit(event) {
      event.preventDefault();

      const email = document.querySelector('#email')
      if (email.value.length >= 1) {
        let exptext = /^[A-Za-z0-9_\.\-]+@[A-Za-z0-9\-]+\.[A-Za-z0-9\-]+/;
        if (exptext.test(email.value) == false) {
            alert("Please enter a vaild email");
            email.focus();
            document.querySelector(".gform").action = " ";
        }else if(email.value.length === 0){
            return
        }else{
            document.querySelector(".gform").action = "MY URL";
            document.querySelector('.send-btn').classList.add('disabled')
            var url = form.action;
            var xhr = new XMLHttpRequest();
            xhr.open('POST', url);
            // xhr.withCredentials = true;
            xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
            xhr.onreadystatechange = function() {
                if (xhr.readyState === 4 && xhr.status === 200) {
                  form.reset();
                  const formElements = form.querySelector(".form-elements")
                  if (formElements) {
                    formElements.style.display = "none"; // hide form
                  }
                  const thankYouMessage = form.querySelector(".thankyou_message");
                  if (thankYouMessage) {
                    thankYouMessage.style.display = "block";
                  }
                }
          }
        }
    }
```

### self-reflection

From this project, I learned the importance of having sufficient knowledge for each device before developing an interactive UI. Unfortunately, it is currently not possible to see if the user is browsing through a mobile device or a small tablet, but it is possible to check if they have a device with a screen size of 1024p or more. In the future, I plan to develop it as a leaflet that opens vertically so that it can respond to smaller devices. (It is really difficult to develop interactive designs for all screen sizes🥺)

these are two major issues that I am trying to solve.

- how to keep the leaflet's size the same when clicked or zoomed in on when the user's screen size is larger than 2400p. As a placeholder until I solve this issue, the UI will redirect to a different version of the JS game UI when larger than 1920p.
- when the user changes the tablet's orientation, how quickly can the user be redirected to the different UI of JS game
