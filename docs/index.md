# 1. Introdução: Visão Geral do Projeto

Este documento detalha o projeto e a implementação de uma nova linguagem de programação imperativa, desenvolvida para a disciplina DIM0548 - Engenharia de Linguagens da Universidade Federal do Rio Grande do Norte. O principal objetivo do projeto é conceber e implementar uma linguagem de programação, com foco particular na área de Ciência de Dados e Aprendizado de Máquina.

A linguagem foi projetada para ter uma sintaxe clara e expressiva, visando a legibilidade do código. Ela oferecerá suporte a tipagem dinâmica ou estática opcional, provendo flexibilidade e segurança. Um aspecto crucial é o suporte a tipos de dados abstratos, como dataframes e tensores, com sobrecarga de operadores para manipulação eficiente, o que é essencial para o domínio de aplicação.

O sistema de implementação ideal para a linguagem proposta é a interpretação, dada a importância da execução interativa para o desenvolvimento e experimentação em Ciência de Dados e Aprendizado de Máquina. Essa abordagem permite a exploração rápida de dados e o desenvolvimento de modelos sem a necessidade de recompilar a cada modificação, acelerando o processo de prototipagem e ajustes.

A linguagem busca ser um híbrido, herdando características de linguagens como C e GoLang, mantendo um propósito semelhante ao LISP, e se posicionando próxima ao Python na árvore genealógica das linguagens de programação. A inspiração do Python se reflete na sintaxe limpa e expressiva, além do suporte à tipagem estática opcional para controle de desempenho e segurança. O projeto visa equilibrar facilidade de uso e expressividade com a eficiência e robustez computacional de linguagens compiladas, tornando-a atrativa tanto para cientistas de dados quanto para desenvolvedores que necessitam de alto desempenho.

O projeto aborda as fases principais de um compilador, incluindo a análise léxica e a análise sintática, com a construção de um analisador sintático bottom-up (LALR). A linguagem também define suas vinculações e sistema de tipos, com foco em tipagem estática e forte.
