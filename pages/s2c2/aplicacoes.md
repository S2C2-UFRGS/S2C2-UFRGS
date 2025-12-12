---
title: "Aplicações e modelagem de dados"
permalink: /aplicacoes.html
hide_sidebar: true
toc: false
page_comments: false
---

Para organizar as informações geradas pela co-simulação e facilitar a análise, os dados trocados entre agentes, simulador (NetLogo) e emulador (Mininet-WiFi) são estruturados em três conjuntos principais:

<table>
    <thead>
        <tr>
            <th>Dado</th>
            <th>Propósito</th>
            <th>Impacto</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>Mensagens</strong></td>
            <td>Registra as tentativas e comunicações bem-sucedidas.</td>
            <td>Avalia a robustez da rede e o sucesso das informações.</td>
        </tr>
        <tr>
            <td><strong>Posições</strong></td>
            <td>Registra o log da trajetória, coordenadas (X, Y) e tempo (<code>tick</code>) de cada unidade.</td>
            <td>Utilizado para deslocamento das unidades e avaliação de comunicações.</td>
        </tr>
        <tr>
            <td><strong>Colinas</strong></td>
            <td>Registra a interferência de elevações do terreno entre pares de unidades.</td>
            <td>Impacta o algoritmo de deslocamento (A*) e o sucesso da comunicação via rádio.</td>
        </tr>
    </tbody>
</table>

## Modelagem de Percepção dos Agentes

Inspirada nos modelos de Kuiper e Wenkstern, a simulação amplia o cone de visão tradicional com um círculo de visão periférica de 180° e um pequeno raio de audição. Essa combinação reduz limitações na detecção de aliados muito próximos, evita interpretações equivocadas e torna o sistema perceptivo mais realista e menos sujeito a falhas que poderiam gerar Fogo Amigo.

## Modelagem de Ocorrências de Fogo Amigo

A simulação é projetada para monitorar e analisar incidentes de Fogo Amigo, que ocorrem quando uma unidade militar ataca outra por engano devido à falha em identificá-la como aliada.

### Sistema Blue Force Tracking (BFT)

A identificação de aliados depende do **reconhecimento visual** (dentro de um limite de distância) e, crucialmente, da **comunicação por rede**. O sistema utiliza um módulo **Blue Force Tracking (BFT)**, que rastreia e exibe as posições de forças aliadas (forças azuis) no campo de batalha, aprimorando a consciência situacional.

* **Implementação:** O BFT é construído como um módulo dentro do **Emulador de Redes (Mininet-WiFi)**. Ele é composto por módulos `Client` e `Server` que se comunicam usando a pilha de rede isolada de cada nó.
* **Comunicação:** O BFT troca dados de localização entre nós. Interrupções na rede, causadas por obstáculos (como colinas), podem gerar dados BFT incompletos ou perdidos, aumentando o risco de fogo amigo. 
* **Dados:** A comunicação entre o orquestrador e a aplicação BFT é realizada via interface **MQTT**.

### Lógica de Ataque e Decisão

O simulador itera sobre o cenário, registrando e analisando alvos dentro do campo de visão e alcance das unidades.

* **Unidades Inimigas:** Seguem um comportamento simplificado: disparam sempre contra unidades aliadas dentro do alcance e **nunca** causam fogo amigo.
* **Unidades Aliadas:** Seguem um processo decisório complexo, baseado em um diagrama de atividades que valida múltiplas condições antes de um disparo, visando modelar o risco de Fogo Amigo. 

As condições que levam a um disparo de fogo amigo incluem:

* A distância está **fora do alcance de reconhecimento visual**.
* O atacante **não recebeu feedback de comunicação BFT** do alvo.
* O alvo está em um estado de combate válido (não `Morto` ou `Assistência Médica Urgente`).
* A unidade respeitou um atraso mínimo de 6 segundos entre a visualização e o disparo (tempo requisitado para tomada de decisão).

Se o atacante for aliado e o alvo for aliado, e todas as condições de ataque forem atendidas, a contagem de **Fogo Amigo** é incrementada.

<div align="center">
    <img src="assets/images/fig7.friendly_fire.png" alt="Fluxo de fogo amigo da aplicação" style="width:80%;">
<div>
