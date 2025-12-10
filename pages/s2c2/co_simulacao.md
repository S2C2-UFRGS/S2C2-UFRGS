---
title: "Co-simulação: Unindo Comportamento e Comunicação Realista"
permalink: /co_simulacao.html
hide_sidebar: true
toc: false
#summary: "Arquitetura geral do sistema S2C2 EmuSim"
---

Para abordar esses desafios de forma abrangente, empregamos um ambiente de **co-simulação** que combina dois simuladores poderosos: **NetLogo** e **Mininet-WiFi**.

Essa combinação permite uma análise mais completa, examinando tanto a **coordenação comportamental** quanto a **robustez da comunicação** sob condições de rede verossímeis, uma vez que a comunicação é um ponto crítico para aplicações C2 em rede \cite{gomes2024survey}.

## NetLogo: O Coração da Simulação Multiagente (MAS)

<table class="c2-split-columns large-figure">
    <tr>
        <td>
            <img src="assets/images/fig12.mapa_simulação.jpeg" alt="Interface Gráfica do NetLogo, um Simulador Multiagente;">
        </td>
        <td>
            O <strong>NetLogo</strong> \cite{netlogo} é um simulador de código aberto amplamente reconhecido, utilizado para projetar, implementar e analisar modelos baseados em agentes. Sua Interface de Desenvolvimento (IDE) amigável e uma comunidade ativa o tornaram um dos simuladores MAS mais populares \cite{vendome2020modelers}. É frequentemente considerado a plataforma de Modelagem Baseada em Agentes (ABM) mais conhecida devido à sua vasta aplicação em diversas disciplinas e níveis educacionais \cite{chiacchio2014agent}.

            <p>O NetLogo é implementado em Java e <strong>Scala</strong>, uma linguagem de programação funcional conhecida por sua sintaxe legível. É uma ferramenta excelente para prototipagem rápida de modelos de pequeno a médio porte ou para a implementação de cenários complexos \cite{chiacchio2014agent}.</p>
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