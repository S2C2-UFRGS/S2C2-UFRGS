---
title: "Modelagem do Sistema"
permalink: /modelagem.html
hide_sidebar: true
toc: false
#summary: "Organização e execução das simulações no S2C2"
page_comments: false
tags: [modelagem, co-simulacao, orquestrador, orquestracao, simulador, emulador, simulacao, emulacao, mapas, granularidade, agentes, modelo]
hide_tags: true
---

O sistema dispõe de uma **Interface Gráfica (GUI)** que se comunica com o núcleo da **Lógica Central da Aplicação (S2C2)** para gerenciar as funcionalidades.

## Funções Chave de Configuraçãoe Gerenciamento:

* **Base de Doutrina Militar:** Componente externo responsável por definir as **regras da doutrina militar** do Exército Brasileiro. Isso determina as configurações e ações permitidas nos cenários (ex: hierarquia de comunicação, alcance de dispositivos, tipologia de agentes).
* **Gerenciamento Semântico (OWL):** Agrega as operações de uma linguagem semântica (OWL) para representar o conhecimento e as regras da doutrina militar. Converte dados doutrinários em parâmetros de simulação e gerencia modificações nos cenários. 
* **Gerenciamento de Parâmetros:** Permite a listagem e personalização dos parâmetros da simulação (dentro das restrições do OWL), essenciais para definir o cenário. Inclui:
    * **Geografia:** Mapa, Clima.
    * **Tropa:** Organização Militar, Tipo de Plataforma, Posição Inicial.
    * **Comunicação:** Alcance dos Dispositivos de Comunicação.
    * **Execução:** Algoritmo de Busca de Caminhos, Tamanho do Lote.

## Orquestrador de Co-simulação

A aplicação possui um **orquestrador (EmuSim)** que gerencia o funcionamento geral do sistema, atuando como ponte entre os eventos da aplicação e os motores de simulação externos, em formato de co-simulação.

<table>
    <thead>
        <tr>
            <th>Motor de Simulação</th>
            <th>Ferramenta</th>
            <th>Papel na Co-simulação</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>Simulador MAS</strong></td>
            <td>NetLogo (Java/Scala)</td>
            <td>Gerencia aspectos operacionais: número de agentes, objetivos, comportamentos e o ambiente.</td>
        </tr>
        <tr>
            <td><strong>Emulador de Redes</strong></td>
            <td>Mininet-WiFi (Python)</td>
            <td>Provê os componentes de rede, executando aplicações de C2 reais e suportando a troca de dados entre os agentes.</td>
        </tr>
    </tbody>
</table>

### Sincronização e Isolamento

* **Sincronização:** O orquestrador foi construído com interfaces para comunicação com o **NetLogo** e **Mininet-WiFi**, garantindo o *loop* sincronizado da co-simulação.
* **Isolamento de Rede:** Cada nó de tropa é executado como uma estação no Mininet-WiFi, utilizando **namespaces do kernel Linux**. Isso garante isolamento completo da pilha de rede e dos processos. Esta abordagem permite que o software C2 real seja executado em um ambiente virtualmente idêntico a um hardware dedicado, mas com maior leveza e controle do que contêineres Docker.

## Mapas e Granularidade

A validade da simulação depende da representação fidedigna do ambiente operacional.

* **Criação de Mapas:** A modelagem utiliza **arquivos topográficos reais**, pré-processados para interpretação pelo NetLogo com rótulos padrão (Ex: terreno intransponível, campo aberto).
* **Modos de Visualização:** O sistema suporta dois modos:
    * **Mapa de Simulação (Padrão):** Agentes interagem diretamente com o *grid* de *patches* e suas propriedades topográficas (afetando movimento, visão e comunicação).
    * **Visualização sobre Imagem (PNG):** A simulação ocorre sobre uma imagem estática (ex: satélite), abstraindo a interação detalhada com a topografia. 
* **Granularidade:** Para otimizar o desempenho em mapas grandes, o sistema permite ajustar a **granularidade do *grid*** do cenário de simulação (tamanho do *patch*). Isso é essencial para evitar que *patches* muito pequenos elevem excessivamente o custo computacional do algoritmo de busca de caminhos (A*).

<table class="c2-split-columns two-figures">
    <tr>
        <td>
            <img src="assets/images/fig12.mapa_simulação.jpeg" alt="Cenário rodando sobre mapa de simulação" style="width:80%;">
        </td>
        <td>
            <img src="assets/images/fig13.mapa_PNG.jpeg" alt="Cenário rodando sobre mapa de visualização">
        </td>
    </tr>
</table>

## Modelagem dos Agentes

A cor de cada agente reflete seu estado durante o *loop* de simulação, sendo definido por uma **Máquina de Estados Finitos (FSM)**. 

<table>
    <thead>
        <tr>
            <th>Estado (Aliado/Inimigo)</th>
            <th>Propósito</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>Saudável</strong> (Azul/Vermelho)</td>
            <td>Estado Inicial.</td>
        </tr>
        <tr>
            <td><strong>Ferido</strong> (Roxo/Rosa)</td>
            <td>Mobilidade reduzida após um acerto.</td>
        </tr>
        <tr>
            <td><strong>Assistência Médica Urgente</strong> (Amarelo/Laranja)</td>
            <td>Estado final que exige evacuação (protegido pela Convenção de Genebra).</td>
        </tr>
        <tr>
            <td><strong>Morto</strong> (Cinza/Preto)</td>
            <td>Estado final.</td>
        </tr>
    </tbody>
</table>

Agentes mudam de estado com base na **probabilidade de acerto** (influenciada pelo alcance da arma e distância do alvo). Acertos em áreas de menor letalidade têm maior probabilidade, enquanto acertos em áreas mais letais têm menor probabilidade, mas causam transições mais graves. A **comunicação e o reconhecimento visual** são essenciais, pois falhas nesses fatores podem levar a incidentes de fogo amigo.

<div align="center">
    <img src="assets/images/fig5.fsm.png" alt="Agentes e suas transições de estados" style="width:45%;">
<div>
