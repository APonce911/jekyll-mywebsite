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
