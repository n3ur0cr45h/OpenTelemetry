
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
   

</div> 
</details>

----

<details>
  <summary><b> 2. Intermediário</b></summary>
<div align="Left">  
<br>  



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
