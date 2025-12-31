---
title: "Visão Arquitetural"
permalink: /visao_arquitetural.html
hide_sidebar: true
toc: false
#summary: "Arquitetura geral do sistema S2C2 EmuSim"
page_comments: false
tags: [arquitetura, co-simulação, simulador, emulador, simulacao, emulacao, componentes, orquestrador, orquestracao]
hide_tags: true
---

Para criar um ambiente de campo de batalha realista, a solução adota uma abordagem integrada que combina um **Simulador de Sistema Multiagente (MAS)** e um **Emulador de Rede**. Essa integração é fundamental para representar tanto os comportamentos realistas das tropas quanto os problemas de interoperabilidade de comunicação no cenário militar.

A estrutura geral da solução é denominada **S2C2 – Configuração e Orquestração de Simulação de Comando e Controle**.

## Co-simulação Orquestrada

O aspecto central da arquitetura é a execução coordenada e sincronizada das duas principais ferramentas em formato de **co-simulação**.

O sistema é composto por um núcleo central de orquestração e dois pilares essenciais:

<table>
    <thead>
        <tr>
            <th>Componente</th>
            <th>Função Essencial</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>EmuSim</strong> (Orquestrador)</td>
            <td>É o <strong>núcleo do sistema</strong>. Responsável por gerenciar e coordenar a execução do cenário de simulação, garantindo a sincronia entre as ferramentas.</td>
        </tr>
        <tr>
            <td><strong>Simulador MAS</strong></td>
            <td>Utilizado para simular o <strong>ambiente de campo de batalha</strong> e o <strong>comportamento das tropas</strong> (agentes), incluindo a tomada de decisão, busca de caminhos e ações.</td>
        </tr>
        <tr>
            <td><strong>Emulador de Rede</strong></td>
            <td>Utilizado para simular a <strong>comunicação real</strong> entre os agentes, emulando a troca de dados entre as aplicações de Comando e Controle (C2) e as tropas simuladas pelo MAS.</td>
        </tr>
    </tbody>
</table>

## Componentes de Suporte

O restante dos componentes fornecem o suporte necessário para configuração, gerenciamento e visualização, incluem:

* **Configuração:** Componentes como `S2C2`, `OWL Manager` e `Parameters Manager` são responsáveis por **criar, carregar e gerenciar** os cenários de simulação, incluindo regras da doutrina militar e parâmetros não doutrinários (mapa, interface gráfica, etc.).
* **Dados e Observabilidade:** Componentes como o `Data Manager` (para modelagem e persistência de dados em um `Database`) e o **Grafana** (API) são usados para **coletar, armazenar e visualizar** as métricas e indicadores de desempenho das simulações executadas.