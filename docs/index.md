# 1. Introdução: Visão Geral do Projeto

## Cabeçalho e documentação online

[https://gsdvl.github.io/DocumentacaoLinguagem/](https://gsdvl.github.io/DocumentacaoLinguagem/)

**Disciplina:** Engenharia de Linguagens - DIM0548

**Integrantes do Grupo:**

- Gabriel Victor de Lima Pimentel  
- Zeus Justino de Lima  
- Lucas Nogueira Cortez  
- Gabriel Soares de Vasconcelos Lira  
- Débora Noemy de Alcântara Valentim

## Visão geral

Este documento detalha o projeto e a implementação da G2DL, uma nova linguagem de programação imperativa desenvolvida para a disciplina DIM0548 - Engenharia de Linguagens da Universidade Federal do Rio Grande do Norte. Com foco particular na área de Ciência de Dados e Aprendizado de Máquina, a linguagem foi cuidadosamente planejada para equilibrar legibilidade, facilidade de escrita, confiabilidade e custo, visando um sistema robusto e eficiente para seu domínio de aplicação.

A G2DL apresenta uma sintaxe clara e expressiva, suporta tipagem estática (com tipos determinados em tempo de compilação para maior segurança), e oferece suporte a tipos de dados abstratos, como dataframes e tensores, com sobrecarga de operadores para manipulação eficiente. Sua concepção híbrida é inspirada na sintaxe limpa e expressividade do Python, na eficiência e robustez de C e GoLang, e nas estruturas de dados primitivas do R. O sistema de implementação idealizado é a interpretação, crucial para a exploração rápida de dados e prototipagem no domínio de Ciência de Dados.

Atualmente, o design da linguagem impõe certas limitações deliberadas para otimização de recursos e clareza. Não há intenção de implementar mecanismos para alocação explícita de variáveis de escopo local na heap, e o tratamento de aliasing é delegado à responsabilidade do programador para poupar recursos. O tratamento completo de exceções é uma funcionalidade que ainda está em desenvolvimento. O projeto abrange as fases principais de um compilador, incluindo a análise léxica e a análise sintática, esta última com a construção de um analisador LALR bottom-up.

Para o futuro, a G2DL planeja aprimorar a robustez da verificação de tipos, expandir seus tipos primitivos para incluir booleanos e implementar funções predefinidas próprias de forma nativa. Adicionalmente, a linguagem busca evoluir para um interpretador completo, aprimorando ainda mais a experiência de desenvolvimento e a interatividade com os dados.
