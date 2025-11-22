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
