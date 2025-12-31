---
title: "Cenários de Testes e Resultados"
permalink: /resultados.html
hide_sidebar: true
toc: false
page_comments: false
tags: [metodologia, cenarios, resultados, bft, cgb, bravo]
hide_tags: true
---


Diferentes cenários de simulação foram desenvolvidos para atender às necessidades das Forças Armadas. Os cenários principais são detalhados a seguir, com o objetivo de ilustrar o progresso e o impacto da comunicação na simulação.

## Cenários com Aplicações Desenvolvidas no Projeto: Metodologia de Teste e Cenários BFT

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

Este cenário teve o objetivo de avaliar o impacto de **unidades hostis** na precisão do sistema BFT (Blue Force Tracking) e nos diferentes intervalos de comunicação (`T`). A simulação manteve o mesmo mapa e topologia do cenário de controle, posicionando **15 unidades aliadas** (3 grupos) e **5 unidades inimigas** em locais estratégicos. A movimentação das unidades aliadas se deu por rotas **determinísticas**, que não são alteradas pela presença hostil. O teste incluiu 5 rodadas para os intervalos `T30` a `T180` ticks.

<table class="c2-split-columns two-figures">
    <tr>
        <td>
            <img src="assets/images/BFT.Inimigos.jpg" alt="Cenário de Simulação BFT 02, posição inicial de aliados e inimigos." style="width:70%;">
        </td>
        <td>
            <img src="assets/images/BFT.inimigos.fogoamigo.png" alt="Cenário de Simulação BFT 02, média de fogo amigo para cinco rodadas por intervalo de tick.">
        </td>
    </tr>
    <tr>
        <td>
            <figure style="margin: 0;">
                <figcaption>Cenário de Simulação BFT 02, posição inicial de aliados e inimigos.</figcaption>
            </figure>
        </td>
        <td>
            <figure style="margin: 0;">
                <figcaption>Cenário de Simulação BFT 02, média de fogo amigo para cinco rodadas por intervalo de tick.</figcaption>
            </figure>
        </td>
    </tr>
</table>

A classificação dos resultados dependeu de três (03): Visão Direta; Mensagem BFT Válida; e Classificação por Omissão, em que a unidade é **tratada como inimigo**. As principais conclusões a partir dos resultados apontam para o **aumento substancial no risco de classificação incorreta** (aliados tratado como inimigos), devido a inclusão de inimigos reais, bem como:

* **Impacto da Comunicação:** O cenário demonstrou uma **forte dependência da frequência** de atualização do BFT.
    * **Curto Intervalo (`T30`, `T60`):** Produziu **alta identificação correta** e baixas taxas de Fogo Amigo.
    * **Longo Intervalo (`T150`, `T180`):** Causou **falhas críticas**, resultando nos maiores índices de Fogo Amigo e classificação cruzada (aliados como inimigos).
* **Origem da Falha:** A adoção de um mapa estático e rotas fixas confirmou que as falhas de identificação originaram-se **exclusivamente da latência e da validade dos dados do BFT**.

Resultados que, em conjunto, reforçam a necessidade crítica de **comunicação frequente** para evitar duplamente o risco: Fogo Amigo e falha na detecção de ameaças reais.

## Cenários com Aplicações do Cliente: Simulação com GCB e Bravo

### Cenário de Simulação com GCB
Este cenário demonstra a **interoperabilidade** do simulador com um software real de Comando e Controle, o **GCB (Gerenciador de Campo de Batalha)**.

* **Objetivo:** Permitir a troca de mensagens entre o simulador e o software GCB para apoiar a tomada de decisão do comandante.
* **Integração:** Após a parametrização do cenário, as estações GCB são inicializadas nos nós simulados do Emulador de Redes, rodando em complemento ao cenário de simulação.
* **Funcionalidade Principal:** O sucesso da comunicação via rede é o que permite o reconhecimento mútuo. Se um novo nó é inserido no campo de batalha e não é reconhecido pela rede BFT/GCB, ele é **automaticamente identificado como inimigo**. Após a troca de mensagens bem-sucedida, o novo elemento é reconhecido como parte do mesmo grupo e inserido corretamente na hierarquia de comando. 


<table class="c2-split-columns two-figures">
    <tr>
        <td>
            <img src="assets/images/simulacoes-no-lab.png" alt="Diferentes cenários de simulação em execução no laboratório S2C." style="width:70%;">
        </td>
        <td>
            <img src="assets/images/simulacao.gcb.png" alt="Troca de mensagens bem-sucedida entre os nós.">
        </td>
    </tr>
    <tr>
        <td>
            <figure style="margin: 0;">
                <figcaption>Diferentes cenários de simulação em execução no laboratório S2C2.</figcaption>
            </figure>
        </td>
        <td>
            <figure style="margin: 0;">
                <figcaption>Troca de mensagens bem-sucedida entre os nós.</figcaption>
            </figure>
        </td>
    </tr>
</table>


### Cenário de Simulação BRAVO (Extensão  S2C2)

Este cenário foi projetado para validar os protocolos e as tecnologias da aplicação **Bravo** (FAC2FTer). Ao contrário de cenários anteriores, o Bravo foi executado de forma isolada para garantir que as funcionalidades de comunicação operassem sem interferências externas.

#### Configuração e Forças

* **Organização:** Três Grupos de Combate (GCs), totalizando 15 agentes de infantaria.
* **Escalabilidade:** Para simular um cenário realista, utilizou-se uma instância do Bravo por grupo. No 3º GC, duas instâncias foram executadas simultaneamente para testar a escalabilidade da aplicação.
* **Conectividade por Proximidade:** O acesso ao Barramento Centralizado depende da localização geográfica. No mapa, pontos de acesso possuem alcances distintos:
    * **Retângulos Amarelos:** Alcance de sinal de **2 km**.
    * **Retângulos Rosas:** Alcance de sinal de **4 km**.



#### Funcionalidades Validadas

* **Mensageria (Chat):** Sucesso no fluxo completo de mensagens (envio, entrega e confirmação de leitura).
* **BFT Nativo:** Monitoramento em tempo real da posição das tropas aliadas. 

<table class="c2-split-columns two-figures">
    <tr>
        <td>
            <img src="assets/images/bravo1.png" alt="Inicialização da aplicação" style="width:60%;">
        </td>
        <td>
            <img src="assets/images/bravo6.png" alt="Comunicação via chat">
        </td>
    </tr>
    <tr>
        <td>
            <figure style="margin: 0;">
                <figcaption>Inicialização da aplicação e apresentaçao dos dados de configuração.</figcaption>
            </figure>
        </td>
        <td>
            <figure style="margin: 0;">
                <figcaption>Comunicação via chat: Envio de resposta com confirmação de leitura.</figcaption>
            </figure>
        </td>
    </tr>
</table>

<div style="width: 100%; text-align: center; margin: 20px 0;">
    <figure style="margin: 0 auto; display: inline-block; width: 100%;">
        <img src="assets/images/bravo.friendly.view.png" 
             alt="Inicialização da aplicação" 
             style="width: 70%; max-width: 800px; border-radius: 4px;">
        <figcaption style="font-size: 0.9em; color: #666; margin-top: 10px; font-style: italic;">
            Distribuição geográfica dos aliados no cenário de simulação.
        </figcaption>
    </figure>
</div>

<div style="width: 100%; margin: 20px 0;">
    <video autoplay loop muted playsinline 
           style="display: block; margin: 0 auto; width: 100%; max-width: 800px; border-radius: 8px; border: 1px solid #ddd;">
        <source src="assets/videos/BravoDemo.mp4" type="video/mp4">
        Seu navegador não suporta a exibição de vídeos.
    </video>
    <p style="text-align: center; font-size: 0.9em; color: #666; margin-top: 10px; font-style: italic;">
        Uso do BFT nativo do Bravo: Atualização de marcação de tropa aliada no mapa.
    </p>
</div>

#### Dinâmica e Conclusão

Durante o deslocamento em direção à Vila Planalto, os Grupos de Combate dependeram da cobertura de rádio para sincronizar dados. A simulação confirmou que a lógica de **Barramento Centralizado por Proximidade** é estável e funcional.

