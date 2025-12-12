---
title: "Cenários de testes e resultados"
permalink: /resultados.html
hide_sidebar: true
toc: false
page_comments: false
tags: [metodologia, cenarios, resultados, bft, cgb, bravo]
hide_tags: true
---


Diferentes cenários de simulação foram desenvolvidos para atender às necessidades das Forças Armadas. Dois cenários principais são detalhados a seguir, com o objetivo de ilustrar o progresso e o impacto da comunicação na simulação.

## Metodologia de Teste e Cenários BFT

Os cenários de teste utilizam o mesmo mapa , características de tropas, parâmetros de comunicação e condições climáticas, diferindo apenas pela presença ou ausência de forças inimigas.

* **Objetivo:** Analisar como a variação na frequência de comunicação afeta a ocorrência de Fogo Amigo (Friendly Fire).
* **Metodologia:** Foram realizadas 43 execuções de simulação para diferentes intervalos de tempo de comunicação (Ex: T30, T60, T90, etc.). O período de validade de cada mensagem BFT recebida foi definido como o dobro do intervalo de comunicação.
* **Identificação de Aliados:** As unidades classificam como aliados aquelas que:
    1.  São identificadas visualmente (dentro do campo de visão).
    2.  Têm suas informações de posição recebidas via rede BFT dentro do período de validade.
    Qualquer unidade que não atenda a esses critérios é classificada como **inimiga**, mesmo que o cenário não contenha adversários reais.

### Cenário BFT 01: Ausência de Inimigos

Para isolar a eficácia do sistema BFT (Blue Force Tracking), as primeiras análises foram executadas na **ausência de unidades inimigas** e em condições climáticas claras.

* **Resultado Principal:** Os dados do BFT contribuem significativamente para a **redução do fogo amigo** em comparação com cenários sem seu uso.
* **Impacto da Comunicação:** Comunicações em intervalos **mais curtos** (maior frequência) melhoram a prevenção de fogo amigo.
* **Tendência Não Linear:** O aumento do intervalo de comunicação não produziu uma tendência linear de aumento de fogo amigo. Observou-se que em intervalos muito longos (ex: T150), se o número de unidades no alcance de comunicação aumentasse, a troca de mensagens bem-sucedidas também aumentava, resultando em uma **redução inesperada** nos incidentes de fogo amigo. 

### Cenário BFT 02: Presença de Inimigos

<p style="color: darkred; font-style: italic; background-color: #ffe8e8; padding: 10px; border-left: 5px solid darkred;">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>

## Cenário de Simulação com GCB (Grupo de Combate)

Este cenário demonstra a **interoperabilidade** do simulador com um software real de Comando e Controle, o **GCB (Grupo de Combate)**.

* **Objetivo:** Permitir a troca de mensagens entre o simulador e o software GCB para apoiar a tomada de decisão do comandante.
* **Integração:** Após a parametrização do cenário, as estações GCB são inicializadas nos nós simulados do Emulador de Redes, rodando em complemento ao cenário de simulação.
* **Funcionalidade Principal:** O sucesso da comunicação via rede é o que permite o reconhecimento mútuo. Se um novo nó é inserido no campo de batalha e não é reconhecido pela rede BFT/GCB, ele é **automaticamente identificado como inimigo**. Após a troca de mensagens bem-sucedida, o novo elemento é reconhecido como parte do mesmo grupo e inserido corretamente na hierarquia de comando. 

<table class="c2-split-columns two-figures">
    <tr>
        <td>
            <img src="assets/images/simulacoes-no-lab.png" alt="Cenário rodando sobre mapa de simulação" style="width:70%;">
        </td>
        <td>
            <img src="assets/images/simulacao.gcb.png" alt="Cenário rodando sobre mapa de visualização">
        </td>
    </tr>
</table>

## Cenário de Simulação com BRAVO

<p style="color: darkred; font-style: italic; background-color: #ffe8e8; padding: 10px; border-left: 5px solid darkred;">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>