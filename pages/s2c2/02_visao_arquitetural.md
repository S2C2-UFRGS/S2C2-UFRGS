---
title: "2. Visão Arquitetural"
permalink: /visao_arquitetural.html
hide_sidebar: true
toc: false
summary: "Arquitetura geral do sistema S2C2 EmuSim"
---
Para representar um ambiente operacional próximo ao real, adotou-se uma abordagem co-simulada, que integra um Simulador de Sistema Multiagente (MAS) com um Emulador de Rede. Essa combinação permite modelar tanto o comportamento das tropas quanto os desafios de comunicação característicos de cenários militares.

O sistema é composto por módulos que se complementam. A interface gráfica (GUI) e o componente lógico S2C2 permitem ao operador criar, carregar e gerenciar cenários de simulação. O conhecimento doutrinário militar é fornecido por uma ontologia externa em OWL, utilizada pelo OWL Manager para manter a consistência lógica dos cenários e apoiar a criação e edição de instâncias de simulação.

Parâmetros operacionais adicionais — como seleção do mapa, modo de execução e opções de visualização — são controlados pelo Parameters Manager, que repassa a configuração final ao orquestrador EmuSim. Este é o núcleo do sistema, responsável por coordenar a execução conjunta do Simulador MAS e do Emulador de Rede, garantindo a sincronização entre o comportamento dos agentes e o fluxo de comunicação.

A arquitetura também inclui um módulo de gerenciamento de dados, responsável por registrar resultados das simulações, manter o modelo de dados e interagir com a ontologia. Para análise e visualização, métricas e indicadores são disponibilizados por meio de dashboards integrados ao Grafana, permitindo observar o desempenho dos cenários simulados.
