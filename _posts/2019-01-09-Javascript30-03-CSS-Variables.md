---
<!-- layout: post -->
title:  "Javascript30 Challenge 03 - CSS Variables & JS"
date:   2019-01-09 17:18:00
---
Javascript30 Challenge 03 - CSS Variables & JS
Objetivo: Fazer inputs no browser alterar CSS dinamicamente.

Diferenças entre solução WesBos & minha:
- CSS variables foram definidas com nome diferentes, e também alterei os nomes no HTML.
- Wes definiu uma constante ‘inputs’ que contém todos os inputs do HTML5 em um nodeList
  const inputs = document.querySelectorAll('.controls input');

e eu defini cada input como uma variável:

let spacing = document.getElementById('spacing');
let blur = document.getElementById('blur');
let base = document.getElementById('base');

- Wes definiu uma constante com ‘suffix’ e fallback ‘nil’.
const suffix = this.dataset.sizing || '';

-Wes usou dois event handlers(change e mousemove) e iterou sobre o objeto ‘inputs’; Eu usei apenas um handler(change) para cada variável:
WES:
inputs.forEach(input => input.addEventListener('change', handleUpdate));
inputs.forEach(input => input.addEventListener('mousemove', handleUpdate));
Eu:
spacing.addEventListener("change", updateSpacing);
blur.addEventListener("change", updateBlur);
base.addEventListener("change", updateBase);

não sei porque ele utilizou o handler mousemove se o change já é o suficiente…

- Wes definiu uma única função de fallback (handleUpdate) para todos os eventos, e eu defini 3:
MINHA:
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
- Wes usou um médoto de JS que não conhecia, o setProperty
document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);

segue função de atuaização do wes:

   function handleUpdate() {
      const suffix = this.dataset.sizing || '';
      document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
    }

Links dos repositórios no github:
Meu:https://github.com/APonce911/javascript30/tree/master/03-CSS-variables
Wes:https://github.com/wesbos/JavaScript30/blob/master/03%20-%20CSS%20Variables/index-FINISHED.html