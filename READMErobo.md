# CSS Art: Let's create a Cute Robot (Beginner)

![robo](https://res.cloudinary.com/practicaldev/image/fetch/s--OKttPc6m--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_800/https://cdn.dribbble.com/users/722835/screenshots/4082720/bot_icon.gif)

This will be a three-part series where we will try and learn how to create 3 Cute Robots with just CSS.

For this first part, we will try and create this simple cute one which is designed by [Irina Mir](https://dribbble.com/irmirx). Send her some love ❤

Now, CSS art can seem quite intimidating in the beginning, but it all comes together when we look at all of these as simple shapes and colors. Through-out this series I will try and explain my thought process while re-creating these beautiful little bots.

**Step 1**:

Let's begin with a simple one. As a first step lets extract all the colors used in this image
```javascript
//cute-robot-v1.scss
$background: #ffffff;
$outline-color: #195272;
$face-color: #e1f4f0;
$tongue-color: #f9bbbb;
$inner-bg: #cedbdd;
```
For extracting colors from an image we have multiple options.
I used the chrome-developer-tools eye-dropper tool to get color codes. Or we could also use online color extractor like [Tiny Eye](https://labs.tineye.com/color/).

**Step 2**:

Now that is done, let us start breaking down it into smaller designable chunks:


1. Background circle
2. Ears
3. Head
4. Face
5. Eyes
6. Mouth
7. Body

Let's put that down in HTML:

```html
<div class="cute-robot-v1">
    <div class="circle-bg">
        <div class="robot-ear left"></div>
        <div class="robot-head">
            <div class="robot-face">
                <div class="eyes left"></div>
                <div class="eyes right"></div>
                <div class="mouth"></div>
            </div>
        </div>
        <div class="robot-ear right"></div>
        <div class="robot-body"></div>
    </div>
</div>
```

**Step 3**:

Now, we will start styling those small individual components and give life to our bot.
```css
//cute-robot-v1.scss
.cute-robot-v1{
    height: 600px;
    display: flex;
    justify-content: center;
    align-items: center;

    * {
        box-sizing: border-box;
    }

    .circle-bg {
        background: $inner-bg;
        width: 250px;
        height: 250px;
        border-radius: 100%;
        border: 8px solid $outline-color;
        position: relative;
    }
}
```

There is nothing fancy happening as of now.

We gave our container height of 600px and set its display property to flex. Also, set the justify-content and align-items to center. This is to make sure everything we put in it will be centered both horizontally and vertically.

And, we also created the style for our background circle, by giving it a height and width and making it a circle by specifying `border-radius: 100%`.

One another important thing to notice here is the position: `relative property`. This makes sure everything else we put inside of the circle will be positioned relative to the circle.

This is our output so far:
![Circle](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fi%2Ft7ckp87aztxvih4afxz5.PNG)

**Step 4**:

Now, to the interesting bit. We will start with the head first so that we can position the ears relative to it.
```css
.robot-head {
    height: 200px;
    width: 200px;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: -20px;
    border: 8px solid $outline-color;
    border-radius: 85px/ 60px;
    background: $background;
    z-index: 4;
}
```
Since the head is absolutely positioned we have to do a small hack to make sure it is centered horizontally. And that is what we do with `left: 50%; transform: translateX(-50%);`.

Here, `left: 50%` makes sure the object starts from the middle but that offsets our robot head to the right. So to rectify the offset we do `transform: translateX(-50%)` which offsets the head back 50% of its width thus making it perfectly centered.

One other interesting thing to notice here is the non-conventional border-radius property.
```css
border-radius: 85px/ 65px;
// can also be interpreted as
border-top-left-radius: 85px 65px;
border-top-right-radius: 85px 65px;
border-bottom-right-radius: 85px 65px;
border-bottom-left-radius: 85px 65px;
```
More on border-radius [here](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius).

Result so far:
![Geometric shape](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fi%2F7i8l9qwajq1ptc1nuea1.PNG)

**Step 5**:

Now we will add the antenna to the head of the bot. I made that choice specifically to not consider antenna as a separate body part but just as an extension to the head itself. But feel free to have it as a different element.

So, since we did not add the antenna as a different element. We will style it using pseudo-selectors `:after` and `:before` and attach it to the robot-head element.
```css
.robot-head {
  ..
  &:after {
    content: "";
    position: absolute;
    top: -30px;
    height: 30px;
    width: 10px;
    left: 50%;
    transform: translateX(-50%);
    background: $outline-color;
  }
  &:before {
    content: "";
    position: absolute;
    top: -60px;
    left: 50%;
    transform: translateX(-50%);
    height: 20px;
    width: 20px;
    background: $inner-bg;
    border: 8px solid $outline-color;
    border-radius: 100%;
  }
}
```
Let us also go ahead and style the eyes and mouth of the robot:
```css
.robot-face {
    height: 120px;
    width: 160px;
    background: $face-color;
    position: absolute;
    top: 45px;
    left: 50%;
    transform: translateX(-50%);
    border: 8px solid $outline-color;
    border-radius: 45px;

    .eyes {
        height: 20px;
        width: 20px;
        background: $outline-color;
        border-radius: 100%;
        position: absolute;
        top: 40px;

        &.left {
            left: 30px;
        }
        &.right {
            right: 30px;
        }
    }

    .mouth {
        height: 45px;
        width: 45px;
        border-radius: 100%;
        border: 8px solid transparent;
        border-bottom-color: $outline-color;
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        top: 50px;
    }
}
```
All the elements are positioned absolutely to its parent element and pushed to its right spot using `top` and `left` property.

The result so far:
![Half robo](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fi%2Fpa7bf6w6bp33jcnsvs4k.PNG)

***Yay!*** ***We are getting there!*** 🕺🎉

**Step 6**:

Now let's give our robot two ears and a body.
```css
.circle-bg{
  ..
  &:after {
    content: "";
    position: absolute;
    z-index: 2;
    height: 100%;
    width: 100%;
    top: -3px;
    left: 0;
    border-radius: 100%;
    border-bottom: 10px solid $outline-color;
  }

  .robot-ear {
    position: absolute;
    height: 100px;
    width: 100px;
    border-radius: 100%;
    background: $background;
    border: 8px solid $outline-color;
    z-index: 3;
    top: 30px;

    &.left {
        left: -20px;
    }
    &.right {
        right: -20px;
    }
  }

  .robot-body {
    height: 50px;
    width: 100px;
    border: 8px solid $outline-color;
    background: $background;
    position: absolute;
    bottom: -5px;
    left: 50%;
    transform: translateX(-50%);
    border-radius: 25px 25px 30px 30px;
  }
  ```
Notice that extra `:after` pseudo selector we added to circle-bg. It is to make sure we add an overlay on the robot body to make it look like it is inside the circle. It is a complete overkill but, well why not! 😎

There, we are done with our first cute robot!
![Whole robo ready](https://media.dev.to/cdn-cgi/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fi%2Fujeoabv34vy5maparzyk.PNG)

Stay tuned for more cute robots! 🤖

I hope you all enjoyed this tutorial. 🫶