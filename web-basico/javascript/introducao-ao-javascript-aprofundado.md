---
description: >-
  Runtime Environment, JS Engine, ECMAScript-ES6. Capítulo destinado a uma explicação mais minuciosa sobre o Javascript. Caso
  esteja iniciando, não é necessário estudá-lo por enquanto. Recomendado para
  leitores que já programam em outras linguagens.
---

# Introdução ao Javascript - Aprofundado

## O que é Javascript
Uma Linguagem feita originalmente para os browsers, que são **Runtine Environments \(Ambiente de execução\)**. Cada browser possui sua própria **JS Engine \(Ou interpretador javascript\)**. Não pode ter sua estrutura original modificada pois isso quebraria sites legados, mas recebe constantemente atualizações **\(ES6/ECMAscript2015\)** por instituições de padronização **\(ECMA\)**.

## Javascript Engine ou Motor Javascript

A JS engine **interpreta o código .js**. Javascript utiliza **"Just in time compilation"**, que transforma em código de máquina apenas a instrução atualmente utilizada, performando otimização durante a execução. O blog voidcanvas possui um [ótimo artigo](https://www.google.com/url?q=https://www.voidcanvas.com/is-javascript-really-interpreted-or-compiled-language/) sobre o assunto

* Exemplos de JS engines: Chackra\(Edge\) SpiderMonkey\(Firefox\) e **V8\(Google Chrome\)**

## Runtime Environment ou Ambiente de Execução

Acrescentam às engines um **ambiente com scripts, bibliotecas e APIS** úteis ao seu contexto.

* O **browser** implementa um runtime environment para **clientes**, e acrescenta por exemplo funções de **manipulação do DOM/HTML** \(`document.getElementById()`\)
* **Node** é um runtime environment para **servidores**, e acrescenta por exemplo funções de acesso aos **arquivos do sistema** \(`fs.readfile()`\)

![Runtime Environment](../../.gitbook/assets/js_intro_img1.png)

Tanto o Google Chrome quanto Node utilizam a mesma JS Engine, o V8.

## ECMA, ES6, ECMAScript2015

Sigla para European Computer Manufacturers Association. **ECMA é uma Instituição de padronização** altamente respeitada que já padronizou outras linguagens como o C\#. Lançam periodicamente novas versões do ECMAScript com **novas funcionalidades** do JS.

Versões demoram para serem implementadas nos browsers. Ferramentas como o **Babel.js transpilam código** de especificação nova para o dito **Vanila.js \(Javascript "Puro"**\).

* A **ECMAScript2015 ou ES6** é a versão que utilizaremos, por ter sido implementada na grande maioria dos browsers sem necessidade de transpilação.

![Imagem de Kostas Diakogiannis](../../.gitbook/assets/js_intro_img2.png)

![Funcionalidades mais &#xFA;teis do ES6 de acordo com 5000 programadores. Pesquisa de Nicol&#xE1;s Bevacqua](../../.gitbook/assets/js_intro_img3.png)