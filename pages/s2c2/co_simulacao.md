---
title: "Co-simulação: Unindo Comportamento e Comunicação Realista"
permalink: /co_simulacao.html
hide_sidebar: true
toc: false
page_comments: false
tags: [co-simulação, simulador, emulador, netlogo, mininet-wifi, interoperabilidade, simulacao, emulacao]
hide_tags: true
---

Para abordar esses desafios de forma abrangente, empregamos um ambiente de **co-simulação** que combina dois simuladores poderosos: **NetLogo** e **Mininet-WiFi**.

Essa combinação permite uma análise mais completa, examinando tanto a **coordenação comportamental** quanto a **robustez da comunicação** sob condições de rede verossímeis, uma vez que a comunicação é um ponto crítico para aplicações C2 em rede \cite{gomes2024survey}.

## NetLogo: O Coração da Simulação Multiagente

<table class="c2-split-columns large-figure">
    <tr>
        <td>
            <img src="assets/images/fig12.mapa_simulação.jpeg" alt="Interface Gráfica do NetLogo, um Simulador Multiagente;">
        </td>
        <td>
            O <strong>NetLogo</strong> é um Simulador de Sistemas Multiagentes, de código aberto, amplamente reconhecido, utilizado para projetar, implementar e analisar modelos baseados em agentes. Sua Interface de Desenvolvimento (IDE) amigável e uma comunidade ativa o tornaram um dos simuladores MAS mais populares. É frequentemente considerado a plataforma de Modelagem Baseada em Agentes (ABM) mais conhecida devido à sua vasta aplicação em diversas disciplinas e níveis educacionais.

            <p>O NetLogo é implementado em Java e <strong>Scala</strong>, uma linguagem de programação funcional conhecida por sua sintaxe legível. É uma ferramenta excelente para prototipagem rápida de modelos de pequeno a médio porte ou para a implementação de cenários complexos.</p>
        </td>
    </tr>
</table>

### Agentes e Extensibilidade do NetLogo

O NetLogo suporta quatro tipos principais de agentes \cite{nogare2020netlogo}:</p>

* **Turtles (Tartarugas):** Agentes móveis que se movem no ambiente.
* **Patches (Patches):** Agentes estacionários que representam pontos fixos ou o ambiente de fundo.
* **Links (Ligações):** Agentes que conectam Turtles, utilizados para modelar redes e grafos.
* **Observer (Observador):** O agente que cria e emite comandos para os outros agentes.

Embora o ambiente principal do NetLogo seja uma matriz de Turtles se movendo sobre Patches, suas capacidades são altamente **extensíveis** ao ser conectado a outras aplicações e linguagens. Por exemplo, existem *plug-ins* que permitem a comunicação com a linguagem R para análise estatística \cite{chiacchio2014agent}, e bibliotecas como PyNetLogo, que possibilitam o controle do NetLogo via programas Python.

## Mininet-WiFi: Emulando Interoperabilidade de Rede

O **Mininet-WiFi** é um emulador leve e de código aberto, desenvolvido em Python, essencial para criar **redes virtuais realistas**. Ele permite simular uma rede completa (com switches, kernel e código de aplicação do computador host) e introduzir a complexidade de **conexões sem fio** (pontos de acesso, comunicação ad hoc e redes mesh).

### Isolamento e Vantagens na Simulação

O Mininet-WiFi é crucial para simular cenários militares realistas, pois utiliza **namespaces do kernel do Linux** para criar ambientes de execução altamente isolados e leves em cada nó (estações e Access Points). 

* **Isolamento Completo:** Cada nó possui sua própria pilha de rede, tabela de rotas e endereços IP, completamente isolados do sistema operacional do host e dos demais nós. Isso garante que as aplicações de C2 (Comando e Controle) rodem em um ambiente virtualmente separado, como se estivessem em máquinas físicas distintas.
* **Vantagem de Leveza:** Ao concentrar-se primariamente no isolamento do espaço de rede e dos processos, o uso de *namespaces* torna o Mininet-WiFi mais leve e eficiente do que soluções baseadas em contêineres Docker, resultando em simulações de rede mais rápidas e com menor sobrecarga computacional.

