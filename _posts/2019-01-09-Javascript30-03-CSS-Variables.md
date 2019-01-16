---
title: "Javascript30 challenge 03 - CSS variables & JS"
date: 2019-01-09 17:18:00
---
Objetivo: Fazer o Javascript alterar dinamicamente os inputs de CSS recebidos pelo browser.

Diferenças entre solução WesBos & minha:
- CSS variables foram definidas com nome diferentes, e também alterei os nomes no HTML.
- Wes definiu uma constante ‘inputs’ que contém todos os inputs do HTML5 em um nodeList:
<pre>
  const inputs = document.querySelectorAll('.controls input');
</pre>

e eu defini cada input como uma variável:
<pre>
  let spacing = document.getElementById('spacing');
  let blur = document.getElementById('blur');
  let base = document.getElementById('base');
</pre>

- Wes definiu uma constante com ‘suffix’ e fallback ‘nil’.
<pre>
  const suffix = this.dataset.sizing || '';
</pre>

-Wes usou dois event handlers(change e mousemove) e iterou sobre o objeto ‘inputs’; Eu usei apenas um handler(change) para cada variável:

WES:

<pre>
  inputs.forEach(input => input.addEventListener('change', handleUpdate));
  inputs.forEach(input => input.addEventListener('mousemove', handleUpdate));
</pre>

Eu:

<pre>
  spacing.addEventListener("change", updateSpacing);
  blur.addEventListener("change", updateBlur);
  base.addEventListener("change", updateBase);
</pre>

não sei porque ele utilizou o handler mousemove se o change já é o suficiente…

- Wes definiu uma única função de fallback (handleUpdate) para todos os eventos, e eu defini 3:
MINHA:

<pre>
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
</pre>

- Wes usou um médoto de JS que não conhecia, o setProperty:

<pre>
  document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
</pre>

segue função de atuaização do wes:

<pre>
 function handleUpdate() {
    const suffix = this.dataset.sizing || '';
    document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
  }
</pre>

Links dos repositórios no github:
<a href="https://github.com/APonce911/javascript30/tree/master/03-CSS-variables" target="_blank">Meu Código</a>,<a href="https://github.com/wesbos/JavaScript30/blob/master/03%20-%20CSS%20Variables/index-FINISHED.html"  target="_blank"> do Wes</a>.

