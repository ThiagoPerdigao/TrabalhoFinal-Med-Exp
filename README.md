# **Plano de Experimento – Identificação Básica, Contexto e Problema**  
### *Análise Experimental da Compactação de Payloads em Aplicações Mobile*

---

## **1. Identificação Básica**

### **1.1 Título do Experimento**
**Análise Experimental da Compactação de Payloads em Aplicações Mobile: impacto em consumo de dados, latência e desempenho**

### **1.2 ID / Código**
**EXP-COMP-MOBILE-001**

### **1.3 Versão do Documento e Histórico de Revisão**
| Versão | Data | Descrição |
|-------|------|-----------|
| **v1.0** | 22/11/2025 | Versão inicial da Identificação, Contexto e Problema |

### **1.4 Datas**
- **Criação:** 22/11/2025  
- **Última atualização:** 22/11/2025

### **1.5 Autores**
- **Nome:** *Thiago Vitor Pereira Perdigão*  
  **Área:** Engenharia de Software  
  **Contato:** *thiagovperdigao@gmail.com*

### **1.6 Responsável Principal (PI)**
- **Thiago Vitor Pereira Perdigão**

### **1.7 Projeto / Produto / Iniciativa Relacionada**
Este estudo integra um projeto aplicado de avaliação de desempenho em aplicações mobile, com ênfase na eficiência da transmissão de dados e no uso racional de recursos de rede. O experimento fornece fundamentos técnicos que podem orientar decisões de arquitetura e otimização em produtos mobile modernos.

---

## **2. Contexto e Problema**

### **2.1 Descrição do Problema / Oportunidade**
Aplicações mobile trocam dados com servidores frequentemente por meio de payloads JSON. O volume de dados transmitidos afeta:

- **consumo de dados do usuário**,  
- **latência percebida**,  
- **uso de CPU para descompressão**,  
- **comportamento sob redes móveis instáveis (3G/4G/5G)**.

Apesar da disponibilidade de vários algoritmos (gzip, brotli, zstd), sua adoção em mobile ainda carece de evidências empíricas consistentes. Os impactos variam com:

- tamanho do payload,  
- condição da rede,  
- capacidade do dispositivo,  
- custo computacional da operação.

Assim, permanece a questão: **qual algoritmo de compactação oferece o melhor equilíbrio entre redução de latência, economia de dados e baixo overhead de CPU para payloads JSON em aplicações mobile, considerando diferentes tamanhos de payload e condições de rede?**  
Este experimento busca fornecer dados controlados e reproduzíveis para responder a essa pergunta.

---

### **2.2 Contexto Organizacional e Técnico**
O estudo será conduzido em ambiente acadêmico, com:

- **Aplicação Android (>= 10)** criada exclusivamente para testes;  
- **Servidor** configurado com none/gzip/brotli/zstd;  
- **Simulação de rede** (tc, Network Link Conditioner);  
- **Medição de CPU** via Android Profiler e ADB;  
- **Coleta automatizada** em CSV.

O ambiente permite controle rigoroso de variáveis e repetibilidade experimental.

---

## **2.3 Trabalhos e Evidências Prévias (Internos e Externos)**

Literatura técnica e científica relata que:

- **gzip** oferece bom equilíbrio, mas taxa de compressão limitada para JSON (Jones et al., 2019).  
- **brotli** alcança maior taxa de compressão, porém com custo computacional mais elevado (Alakuijala & Szabadka, 2016).  
- **zstd** obtém alta taxa de compressão com excelente velocidade (Collet, 2021).  
- Redução de bytes impacta fortemente a latência em redes móveis (Ying et al., 2020; Zhang & Ren, 2022).  
- CPU tem grande impacto no tempo de resposta em dispositivos mobile (Kim et al., 2021; Liu et al., 2020).

Poucos trabalhos, entretanto, avaliam esses algoritmos em cenários mobile reais, combinando rede, CPU e variação de payload — lacuna que este estudo busca suprir.

---

## **2.4 Referencial Teórico e Empírico Essencial**

### **a) Teoria da Compactação**
- **LZ77/LZ78** — algoritmos fundamentais para gzip e derivados (Ziv & Lempel, 1977).  
- **Huffman Coding** — usado em praticamente todos os algoritmos de compressão (Huffman, 1952).  
- **Brotli** — compressão baseada em dicionário estático otimizado (Alakuijala & Szabadka, 2016).  
- **Zstandard** — combinação de dicionários dinâmicos + FSE/Huffman (Collet, 2021).

### **b) Desempenho em Redes Móveis**
- Modelos de latência e throughput em redes móveis (Wang et al., 2018; Feamster & Livingood, 2019).  
- Variação temporal e instabilidade de redes celulares (Kakhki et al., 2020).

### **c) Engenharia de Desempenho Mobile**
- Overhead de CPU em dispositivos Android (Liu et al., 2020; Kim et al., 2021).  
- Parsing e descompressão em payloads estruturados (Xu et al., 2019; Zhang & Ren, 2022).

### **d) Metodologia Experimental**
- GQM (Basili et al., 1994).  
- ANOVA e métodos estatísticos aplicados à engenharia de software (Juristo & Moreno, 2010).  
- Diretrizes para experimentação controlada (Wohlin et al., 2012).

---

# **3. Objetivos e Questões (GQM)**

## **3.1 Objetivo Geral (Template GQM)**
**Analisar** o impacto de diferentes algoritmos de compactação (gzip, brotli e zstd)  
**com o propósito de** avaliar sua efetividade em reduzir latência, consumo de dados e overhead de CPU  
**sob a perspectiva de** desenvolvedores e engenheiros de desempenho  
**no contexto de** aplicações mobile Android realizando requisições JSON em redes móveis variáveis.

---

## **3.2 Objetivos Específicos**

- **O1.** Avaliar o impacto dos algoritmos de compactação na *latência total* das requisições.
- **O2.** Comparar a *taxa de redução do tamanho do payload* entre os algoritmos.
- **O3.** Medir o *overhead de CPU* causado pelas etapas de compressão e descompressão.
- **O4.** Avaliar o impacto da compactação no desempenho sob *diferentes condições de rede* (boa, média, degradada).

---

## **3.3 Questões de Pesquisa**

### **Objetivo O1 — Latência**
- **Q1.1:** A compactação reduz a latência total das requisições?  
- **Q1.2:** Qual algoritmo apresenta menor latência sob payloads pequenos, médios e grandes?  
- **Q1.3:** Como a latência varia entre redes 3G, 4G e Wi-Fi?

### **Objetivo O2 — Redução de Tamanho**
- **Q2.1:** Qual algoritmo gera maior taxa de compressão?  
- **Q2.2:** A taxa de compressão varia com o tamanho do payload JSON?  
- **Q2.3:** Existe relação entre taxa de compressão e latência obtida?

### **Objetivo O3 — Overhead de CPU**
- **Q3.1:** Qual algoritmo possui menor custo de CPU no device?  
- **Q3.2:** O custo de CPU varia com o tamanho do payload?  
- **Q3.3:** A descompressão representa maior custo que a compressão?

### **Objetivo O4 — Robustez sob diferentes redes**
- **Q4.1:** Quais algoritmos mantêm desempenho estável em redes instáveis?  
- **Q4.2:** A compactação melhora a performance em redes degradadas?  
- **Q4.3:** Existe diferença significativa entre algoritmos quando há perda de pacotes?

---

## **3.4 Tabela GQM**

| **Objetivo** | **Pergunta** | **Métricas Associadas** |
|--------------|--------------|--------------------------|
| O1 | Q1.1 | M1 Latência total; M2 Tempo de resposta (RTT) |
| O1 | Q1.2 | M1 Latência total; M3 Desvio padrão da latência |
| O1 | Q1.3 | M1 Latência total; M4 Tempo de conexão |
| O2 | Q2.1 | M5 Tamanho comprimido; M6 Taxa de compressão (%) |
| O2 | Q2.2 | M5 Tamanho comprimido; M7 Tamanho original |
| O2 | Q2.3 | M6 Taxa de compressão; M1 Latência total |
| O3 | Q3.1 | M8 CPU utilização (%); M9 Tempo de descompressão |
| O3 | Q3.2 | M8 CPU utilização; M10 Tempo de compressão |
| O3 | Q3.3 | M9 Tempo de descompressão; M10 Tempo de compressão |
| O4 | Q4.1 | M1 Latência; M11 Variação de latência |
| O4 | Q4.2 | M1 Latência; M12 Throughput efetivo |
| O4 | Q4.3 | M11 Variação de latência; M5 Tamanho comprimido |

---

## **3.5 Tabela de Métricas (Descrição e Unidade)**

| **Código** | **Descrição da Métrica** | **Unidade** |
|-----------|---------------------------|-------------|
| **M1** | Latência total medida do app ao servidor (request → response) | ms |
| **M2** | RTT (Round Trip Time) médio por requisição | ms |
| **M3** | Desvio padrão da latência entre execuções | ms |
| **M4** | Tempo até o estabelecimento da conexão | ms |
| **M5** | Tamanho do payload comprimido | bytes |
| **M6** | Taxa de compressão = (1 - M5/M7) | % |
| **M7** | Tamanho do payload original (sem compressão) | bytes |
| **M8** | Utilização de CPU durante compressão/descompressão | % |
| **M9** | Tempo de descompressão do payload | ms |
| **M10** | Tempo de compressão do payload | ms |
| **M11** | Variação de latência entre tentativas consecutivas | ms |
| **M12** | Throughput efetivo sob condição de rede medida | kbps |

---

# 4. Escopo e Contexto do Experimento

## 4.1 Escopo Funcional / de Processo (Incluído e Excluído)

**Incluído:**
- Comunicação entre aplicação Android e servidor via HTTP(S).
- Envio e recebimento de payloads JSON de tamanhos variados (pequeno, médio e grande).
- Execução dos algoritmos de compactação: **none (controle), gzip, brotli, zstd**.
- Medições de desempenho: latência, tamanho do payload, uso de CPU na descompressão.
- Simulação de redes móveis (3G, 4G, 5G e Wi-Fi).
- Execução automatizada e coleta de logs/CSV.

**Excluído:**
- Consumo de bateria (explicitamente fora do escopo).
- Dispositivos iOS.
- Protocolos distintos de JSON/HTTP (por exemplo, gRPC, Protobuf).
- Compactação aplicada apenas no servidor sem descompressão no cliente.
- Avaliação de segurança ou cifragem de payloads.

---

## 4.2 Contexto do Estudo
- Experimento conduzido em ambiente acadêmico, no contexto de um TCC.
- Aplicação Android desenvolvida exclusivamente para testes controlados.
- Estudo não envolve usuários finais, apenas execução automatizada.
- Infraestrutura composta por um servidor Linux com suporte a múltiplos algoritmos de compressão.

---

## 4.3 Premissas
- Os ambientes Android e servidor estarão estáveis durante todo o experimento.
- As ferramentas de medição de CPU e latência (ADB, Android Profiler) funcionarão corretamente.
- A simulação de rede (tc/Network Link Conditioner) reproduzirá condições realistas.
- O volume de payloads será suficiente para gerar diferenças estatisticamente relevantes.
- Todos os scripts e instrumentos serão testados previamente no piloto.

---

## 4.4 Restrições
- Tempo limitado para execução e repetição de múltiplos cenários de rede.
- Capacidade de hardware limitada ao dispositivo Android disponível.
- Apenas algoritmos gzip, brotli e zstd serão avaliados — exclusões por tempo e recursos.
- Execução de testes sob uma única versão do Android (>=10).
- Apenas payloads JSON estruturados — não serão testados binários, imagens ou outros formatos.

---

## 4.5 Limitações Previstas
- Resultados podem não generalizar para:
  - Aplicativos iOS.
  - Aplicações que usam Protobuf, Avro ou outros formatos binários.
  - Redes reais com maior variabilidade do que a simulada.
- A CPU específica do dispositivo pode influenciar significativamente os tempos.
- A análise considera apenas um modelo de smartphone — limita a validade externa.

---

# 5. Stakeholders e Impacto Esperado

## 5.1 Stakeholders Principais
- **Autor/Pesquisador (PI)** – execução, análise e documentação.
- **Orientador Acadêmico** – validação científica.
- **Desenvolvedores Mobile** – potenciais usuários dos resultados.
- **Arquitetos de Software** – decisões sobre pipelines e arquitetura de rede.
- **Equipes de Produto** – impacto em UX (latência percebida).
- **Comunidade Acadêmica** – replicação e benchmarking.

---

## 5.2 Interesses e Expectativas dos Stakeholders

| Stakeholder | Interesse / Expectativa |
|------------|--------------------------|
| Pesquisador (PI) | Resultados estatisticamente válidos; execução reprodutível. |
| Orientador | Rigor metodológico; validade interna e externa. |
| Devs Mobile | Diretrizes práticas sobre quando usar compactação. |
| Arquitetos | Evidências para escolha de algoritmos e padrões de API. |
| Produto | Redução de latência e consumo de dados, melhor experiência do usuário. |
| Comunidade Acadêmica | Experimento claro, replicável e bem documentado. |

---

## 5.3 Impactos Potenciais no Processo / Produto
- Possível identificação de algoritmos inadequados para determinados tamanhos de payload.
- Orientações para melhorar desempenho em redes móveis.
- Potencial redução de latência percebida em aplicativos reais.
- Fornecimento de dados para otimização de APIs e padrões de backend.
- Impacto futuro em decisões arquiteturais e políticas de compressão.

---

# 6. Riscos de Alto Nível, Premissas e Critérios de Sucesso

## 6.1 Riscos de Alto Nível
| Tipo | Risco | Mitigação |
|------|--------|-----------|
| Técnico | Falha nas ferramentas de simulação de rede (tc/NLC). | Validar tudo no piloto; usar alternativas caso necessário. |
| Técnico | Inconsistência nas medições de CPU. | Coletar múltiplas repetições; descartar outliers. |
| Operacional | Tempo insuficiente para executar todos os cenários. | Priorizar cenários críticos; automatizar 100% das execuções. |
| Científico | Diferenças pequenas demais para detectar. | Aumentar repetições; avaliar tamanho de efeito. |
| Contexto | Dependência de apenas um dispositivo Android. | Documentar limitações e realizar múltiplas execuções para estabilidade. |

---

## 6.2 Critérios de Sucesso Globais (Go / No-Go)
O experimento será considerado bem-sucedido se:

- Todas as métricas forem coletadas de forma consistente e sem perdas.
- Cada cenário de rede × tamanho de payload × algoritmo for executado pelo menos N vezes (definido no desenho estatístico).
- For possível responder a todas as questões GQM com evidências quantitativas.
- Houver condições claras para comparar os algoritmos e gerar conclusões válidas.

---

## 6.3 Critérios de Parada Antecipada
O experimento deve ser interrompido **antes da execução** se ocorrer:

- Falha na instrumentação que impeça medições de CPU ou latência.
- Inconsistência grave na simulação de rede.
- Problemas éticos, legais ou de infraestrutura.
- Tempo total estimado ultrapassar o cronograma máximo permitido.
- Dados inconsistentes no piloto indicando inviabilidade de execução real.

---





## **Referências**

ALAKUIJALA, J.; SZABADKA, Z. **Brotli: A general-purpose data compressor**. Google Research, 2016.

BASILI, V. R.; CALDIERA, G.; ROMBACH, H. D. **The Goal Question Metric Approach**. Encyclopedia of Software Engineering, John Wiley & Sons, 1994.

COLLET, Y. **Zstandard compression and the “.zst” file format**. Facebook Engineering, 2021.

FEAMSTER, N.; LIVINGOOD, J. **Measuring Internet Performance in the Age of Mobile Computing**. ACM SIGCOMM, 2019.

HUFFMAN, D. **A Method for the Construction of Minimum-Redundancy Codes**. Proceedings of the IRE, v. 40, n. 9, 1952.

JONES, T. et al. **Evaluating Compression Algorithms for Web Content**. IEEE Communications Surveys & Tutorials, 2019.

JURISTO, N.; MORENO, A. M. **Basics of Software Engineering Experimentation**. Springer, 2010.

KAKHKI, A. M. et al. **A longitudinal analysis of cellular network performance**. IMC, ACM, 2020.

KIM, D.; LEE, J.; PARK, S. **Analyzing CPU-bound operations in Android apps**. IEEE MobileSoft, 2021.

LIU, Y.; CHEN, H.; XU, X. **Performance Profiling on Android: CPU and Network Considerations**. Journal of Systems and Software, 2020.

WANG, R. et al. **Understanding performance of mobile networks**. IEEE Transactions on Mobile Computing, 2018.

WOHLIN, C. et al. **Experimentation in Software Engineering**. Springer, 2012.

XU, X.; LI, J.; WANG, P. **Evaluating JSON parsing and processing overhead in mobile apps**. MobileSoft, IEEE, 2019.

YING, Z.; DONG, Z.; ZHOU, K. **Effects of Payload Size and Compression on Mobile Latency**. ACM MMSys, 2020.

ZHANG, H.; REN, Y. **Impact of Data Compression Techniques on Mobile Application Performance**. IEEE Access, 2022.

ZIV, J.; LEMPEL, A. **A universal algorithm for sequential data compression**. IEEE Transactions on Information Theory, v. 23, n. 3, 1977.
