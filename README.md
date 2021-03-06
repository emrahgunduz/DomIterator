# DomIterator
PHP terminal script to convert given HTML dom tree to Javascript code.

* Just run and paste your HTML dom tree, the command line accepts multiline inputs.
* On a new line, enter "!q" (without quotes) to end the input.
* You'll see your dom tree and also the javascript code will be output.
* Script will also save your code to a "dom.js" file for easy access.

* Creates a javascript variable name from the code.
 * You can use "data-jsid" in your html to tell the script what to use as variable name.
 * This is the current priority for creating a variable name:
    data-jsid > 
    class (first class from all assigned ones) > 
    dom name (like div, img, h4, etc.)
 * If variable name is already used, a number will be added and incremented if needed (like img1, img2, etc.)

For example, this html:
```html
<div class="categoryparent" data-jsid="categoryParent">
  <div class="categoryname" data-jsid="categoryName">
    <h4>Generate JS Code!</h4>
  </div>

  <div class="mainvideoholder" data-jsid="topHolder">
    <div class="left" data-jsid="buttonLeft">
      <img class="arrow" src="/images/video/arrow-left.svg">
    </div>

    <div class="videos" data-jsid="videoHolder">
    Holding videos since 1977
    </div>

    <div class="right" data-jsid="buttonRight">
      <img class="arrow" src="images/video/arrow-right.svg">
    </div>
  </div>
</div>
```

Becomes this javascript code
```javascript
const categoryParent = document.createElement('div');
categoryParent.setAttribute('class','categoryparent');

const categoryName = document.createElement('div');
categoryName.setAttribute('class','categoryname');
categoryParent.appendChild(categoryName);

const h4 = document.createElement('h4');
categoryName.appendChild(h4);
h4.innerHTML = "Generate JS Code!";

const topHolder = document.createElement('div');
topHolder.setAttribute('class','mainvideoholder');
categoryParent.appendChild(topHolder);

const buttonLeft = document.createElement('div');
buttonLeft.setAttribute('class','left');
topHolder.appendChild(buttonLeft);

const arrow = document.createElement('img');
arrow.setAttribute('class','arrow');
arrow.setAttribute('src','/images/video/arrow-left.svg');
buttonLeft.appendChild(arrow);

const videoHolder = document.createElement('div');
videoHolder.setAttribute('class','videos');
topHolder.appendChild(videoHolder);
videoHolder.innerHTML = "Holding videos since 1977";

const buttonRight = document.createElement('div');
buttonRight.setAttribute('class','right');
topHolder.appendChild(buttonRight);

const arrow1 = document.createElement('img');
arrow1.setAttribute('class','arrow');
arrow1.setAttribute('src','images/video/arrow-right.svg');
buttonRight.appendChild(arrow1);
```

