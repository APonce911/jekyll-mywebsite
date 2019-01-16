---
title: "Javascript30 challenge 03 - CSS variables & JS"
date: 2019-01-09 17:18:00
---
Objetivo: Fazer o Javascript alterar dinamicamente os inputs de CSS recebidos pelo browser.

 Veja <a href="https://aponce911.github.io/javascript30/03-CSS-variables/index.html" target="_blank">aqui</a>, como ficou minha versão do exercício.


Diferenças entre a solução do Wes Bos e a minha:
1. Definição de objetos \<input> no Javascript.

    - Wes definiu uma constante ‘inputs’ que contém todos os inputs do HTML5 em um nodeList:

    <pre>
      const inputs = document.querySelectorAll('.controls input');
    </pre>

    - Eu defini cada input como uma variável:

    <pre>
      let spacing = document.getElementById('spacing');
      let blur = document.getElementById('blur');
      let base = document.getElementById('base');
    </pre>

1. Wes definiu uma constante com ‘suffix’ e fallback ‘nil’, eu escrevi os sufixos manualmente.

    - Wes:

    <pre>
      const suffix = this.dataset.sizing || '';
    </pre>

1. Numero de Handlers nos event listeners.

    - Wes usou dois event handlers(change e mousemove) e iterou sobre o objeto ‘inputs’:

    <pre>
      inputs.forEach(input => input.addEventListener('change', handleUpdate));
      inputs.forEach(input => input.addEventListener('mousemove', handleUpdate));
    </pre>

    - Eu usei apenas um handler(change) para cada variável:

    <pre>
      spacing.addEventListener("change", updateSpacing);
      blur.addEventListener("change", updateBlur);
      base.addEventListener("change", updateBase);
    </pre>

    (não sei porque ele utilizou o handler mousemove se o change já é o suficiente…)

1. Definição de fallback function(s).


    - Eu defini 3 fallback functions, uma para cara input:

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

    - Wes definiu uma única função de fallback (handleUpdate) para todos os eventos, e usou um médoto de JS que não conhecia, o setProperty, segue função de atuaização do wes:

    <pre>
     function handleUpdate() {
        const suffix = this.dataset.sizing || '';
        document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
      }
    </pre>


Links dos repositórios no github:
<a href="https://github.com/APonce911/javascript30/tree/master/03-CSS-variables" target="_blank"> Meu Código</a>,<a href="https://github.com/wesbos/JavaScript30/blob/master/03%20-%20CSS%20Variables/index-FINISHED.html"  target="_blank"> do Wes</a>.

