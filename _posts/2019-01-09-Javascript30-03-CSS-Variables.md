---
title: "Javascript30 challenge 03 - CSS variables & JS"
date: 2019-01-09 17:18:00
lang: en
ref: javascript30-challenge-03

---
Goal: To make the javascript change dynamically the page CSS with the inputs passed through the browser.

 See <a href="https://aponce911.github.io/javascript30/03-CSS-variables/index.html" target="_blank" class="external-link">here</a> how is my version of the exercice.


Difference between Wes Bos solution and mine:

1. Defining the \<input> object on Javascript.

    Wes defined a constant 'inputs' which contains all HTML inputs in a nodeList:

    <pre>
      <code>
      const inputs = document.querySelectorAll('.controls input');
      </code></pre>

    I defined each input as a variable:

    <pre>
      <code>
      let spacing = document.getElementById('spacing');
      let blur = document.getElementById('blur');
      let base = document.getElementById('base');
      </code></pre>

1. Wes defined a 'suffix' constant and a 'nil' default value, I wrote manually each suffix.

    <pre>
      <code>
      const suffix = this.dataset.sizing || '';
    </code></pre>

1. Number of handlers on event listeners.

    Wes used two event handlers(change e mousemove) and iterated over the object ‘inputs’:

    <pre>
      <code>
      inputs.forEach(input => input.addEventListener('change', handleUpdate));
      inputs.forEach(input => input.addEventListener('mousemove', handleUpdate));
    </code></pre>

    I used one handler(change) for each variable:

    <pre>
      <code>
      spacing.addEventListener("change", updateSpacing);
      blur.addEventListener("change", updateBlur);
      base.addEventListener("change", updateBase);
    </code></pre>

    (I don't know why he used the 'mousemove' handler if the 'change' is enough ...)

1. Fallback function(s) definition.


    I defined 3 fallback functions, one for each input:

    <pre>
      <code>
      function updateSpacing() {
        image.style.marginTop = `${spacing.value}px`;
        image.style.marginLeft = `${spacing.value}px`;
        console.log(spacing.value);
      }
      function updateBlur() {
        image.style.filter = `blur(${blur.value}px)`;
        console.log(blur.value);
      }
      function updateBase() {
        document.body.style.background = base.value;
        console.log(base.value);
      }
      </code></pre>

    Wes defined a single fallback function (handleUpdate) for all events, and used a JS method that I didn't knew, the setProperty. Here is the his update function:

    <pre>
      <code>
      function handleUpdate() {
        const suffix = this.dataset.sizing || '';
        document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
      }
      </code></pre>


Github repositories links:
<a href="https://github.com/APonce911/javascript30/tree/master/03-CSS-variables" target="_blank" class="external-link"> My code</a>,<a href="https://github.com/wesbos/JavaScript30/blob/master/03%20-%20CSS%20Variables/index-FINISHED.html"  target="_blank" class="external-link"> Wes</a>.

