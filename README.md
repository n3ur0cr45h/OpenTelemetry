
<div align="Center"> 
<br>

<h4>

░█████╗░██████╗░███████╗███╗░░██╗████████╗███████╗██╗░░░░░
██╔══██╗██╔══██╗██╔════╝████╗░██║╚══██╔══╝██╔════╝██║░░░░░
██║░░██║██████╔╝█████╗░░██╔██╗██║░░░██║░░░█████╗░░██║░░░░░
██║░░██║██╔═══╝░██╔══╝░░██║╚████║░░░██║░░░██╔══╝░░██║░░░░░
╚█████╔╝██║░░░░░███████╗██║░╚███║░░░██║░░░███████╗███████╗
░╚════╝░╚═╝░░░░░╚══════╝╚═╝░░╚══╝░░░╚═╝░░░╚══════╝╚══════╝
</h4>
</div>

----

<details>
  <summary><b> 1. Fundamentos</b></summary>
<div align="Left">  
<br>  

O1.1 - OpenTelemetry
 > - Projeto Open Source, mantido pela Cloud Native Computing Foundation;
 > - Fornece conjunto unificado de ferramentas, APIs e SDKs, para coletar, gerar, processar e exportar dados de observabilidade;
 > - Plataforma padronizada para instrumentação de aplicações.

O1.2 - OpenTelemetry SDK | Software Development Kit 
 > - Implementação concreta das APIs do OTel, para uma linguagem específica;
 > - Roda dentro da aplicação, coletando e processando dados de observabilidade antes de enviá-los.
 > - Funções:
 >   - Cria Spans, Traces e Métricas;
 >   - Controla Amostragem (Sampling);
 >   - Gerencia Exportação dos Dados (via Exporters);
 >   - Aplica Configurações de Contexto e Propagação de Trace entre Serviços.
 > - O SDK envia os dados diretamente para um backend, ou, para o OTel Collection via OTLP - OpenTelemetry Protocol.

O1.3 - Collector 
 > - Serviço independente que atua como um pipeline de processamento e exportação de dados;
 > - Agnóstico de linguagem - pode receber dados de múltiplas fontes, processá-los e enviá-los para diferentes destinos.
 > - Funções:
 >   - Recebe Dados;
 >   - Processa (Filtra, agrega, enriquece ou transforma);
 >   - Exporta para backends de monitoramento (Grafana, Jaeger, Datadog, Prometheus, etc).
 > - Pode ser executado de três formas:
 >   - Agent: Roda junto com cada aplicação;
 >   - Gateway: Centralizado para todo o tráfego de telemetria;
 >   - Híbrido: Combinação dos dois.        

O1.4 - Instrumentações
 > - Responsáveis por coletar automaticamente | manualmente os dados da aplicação.
 >   - Instrumentação Automática:
 >     - Detecta automaticamente bibliotecas e frameworks conhecidos;
 >     - Injeta spans e métricas sem alterar o código da aplicação;
 >     - Ideal para começar rápido ou monitorar sistemas legados.
 >
 >   - Instrumentação Manual:
 >     - Adição de chamadas explícitas às APIs do OTel;
 >     - Fornece mais controle sobre o que é medido e quando;
 >     - Usado quanto a instrumentação automática não cobre certos cenários.

O1.5 - Receivers | Exporters 
 > - Receivers: 
 >   - Pontos de Entrada no Collector;
 >   - Recebem dados de diferentes formatos e protocolos (OTLP, Jaeger, Zipkin, Prometheus, etc.);
 >
 > - Exporters:
 >   - Pontos de saída do Collector ou SDK;
 >   - Enviam os dados processados para ferramentas de observabilidade ou backends.

O1.6 - Processors | Pipelines 
 > - Processors: 
 >   - Etapas intermediárias dentro do Collector;
 >   - Modificam, filtram ou agregam dados - antes da exportação.
 >   
 > - Pipelines:
 >   - Fluxos lógicos de conexão dos Receivers -> Processors -> Exporters;
 >   - Cada tipo de dados (traces, metrics, logs), tem sua própria pipeline.

O1.7 - Spans | Traces | Contextos 
 > - Tríade da base do Rastreamento Distribuído.
 >   - Span:
 >     - Unidade individual de trabalho dentro de uma operação maior;
 >     - Cada Span contém informações como:
 >       - Nome;
 >       - Início e Fim (Timestamp);
 >       - Atributos;
 >       - Eventos;
 >       - Contexto (SpanContext).
 >
 >    - Trace:
 >      - Conjunto de Spans conectados entre si;
 >      - Representa a jornada completa de uma requisição;
 >      - Cada Trace tem um Trace ID único, que identifica toda a cadeia.
 >
 >    - Contexto:
 >      - "Fio Condutor", que conecta os spans entre si;
 >      - Contém o Trace ID e o Span ID do Span Atual (Ativo);
 >      - Propagado entre serviços, para manter o trace contínuo em sistemas distribuídos.

O1.8 - Hierarquia entre Spans (Parent | Child) 
 > - Spans podem se encadear hierarquicamente, formando uma árvore de execução:
 >   - O primeiro span é o "Root Span" (Sem pai);
 >   - Spans criados dentro dele, são "Child Spans";
 >   - Cada Child Span herda o Trace ID do Root, mas tem seu próprio Span ID.   

O1.9 - Estrutura de Métrica
 > - As métricas no OTel são compostas por três elementos principais:
 >   - Instrumento:
 >     - Ponto de medição no código - tipo de métrica sendo coletada;
 >     - Tipos de Instrumento:
 >       - Counter: Contagem de eventos cumulativos (Só aumenta);
 >       - UpDownCounter: Aumenta ou Diminui;
 >       - Histogram: Distribuição de Valores;
 >       - Gauge: Valor atual de algo.
 >   - Unidade:
 >     - Define o que está sendo medido - unidade semântica, para padronização e integração com ferramentas de visualização.
 >       - seconds: Tempo; 
 >       - bytes: Tamanho;  
 >       - requests: Contagem de eventos.
 >    - Agregação:
 >      - Define como os valores observados são combinados ao longo do tempo.
 >        - Sum;
 >        - LastValue;
 >        - Histogram;
 >        - ExponentialHistogram.

O1.10 - W3C Trace Context Specification 
 > - Define como o contexto de rastreamento é propagado entre serviços;
 > - Como os serviços compartilham o identificador de trace e span, ao longo de uma requisição distribuída;
 > - O objetivo é garantir que diferentes sistemas e frameworks possam reconhecer e continuar um mesmo trace de ponta a ponta.
 > - Cabeçalhos Principais:
 >   - traceparent: Contém os identificadores do trace e do span;
 >   - tracestate: Metadados adicionais, usados por provedores específicos.        

</div> 
</details>

----

<details>
  <summary><b> 2. Intermediário</b></summary>
<div align="Left">  
<br>  

O2.1 - Fluxo de Dados
 > - Aplicação -> OTel SDK -> OTel Collector -> Backend (Grafana, Prometheus, Tempo, etc.)
 > - Etapa 1: O código é instrumentaod com o OTel SDK - que coleta os dados de telemetria (Traces, Métricas e Logs);
 > - Etapa 2: O SDK pode exportar os dados diretamente (via exporters), ou enviar para um Collector - usando o OTLP;
 > - Etapa 3: O Collector é o agente de processamento e roteamento, recebendo, transformando e exportando os dados aos Backends;
 > - Etapa 4: Backend - sistemas de observabilidade -, recebem os dados.

O2.2 - Agent Mode | Gateway Mode
 > - Agent Mode:
 >   - Collector roda localmente junto da aplicação - no mesmo host ou contêiner;
 >   - Coleta os dados diretamente do SDK.
 > - Gateway Mode:
 >   - Collector roda centralizado - como um serviço ou deployment;
 >   - Recebe dados de vários agentes ou SDKs.   

</div> 
</details>

----

<details>
  <summary><b> 3. Avançado</b></summary>
<div align="Left">  
<br>  



</div> 
</details>

----
