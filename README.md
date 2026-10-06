<p align="center">
  <img src="imagens/logo-unifef.png" alt="UNIFEF" width="180">
</p>

<h1 align="center">O Gerente — Sistema de Gestão Agrícola Cítrica</h1>

<p align="center">
  Planejamento e cronograma de um sistema web de gestão para pequenos e médios produtores de frutas cítricas.<br>
  Atividade da AV1 de <strong>Engenharia de Software e Gerência de Projetos</strong> — UNIFEF, 6º semestre de Sistemas de Informação.<br>
  Prof. Marcelo Tadeu Boer
</p>

<p align="center">
  <a href="https://youtu.be/gffYAswOtgk"><strong>Assistir à apresentação</strong></a> ·
  <a href="https://lucassabadinimendess-team.monday.com/boards/18433545202"><strong>Cronograma no Monday.com</strong></a>
</p>

---

## Sumário

- [Sobre o projeto](#sobre-o-projeto)
- [O problema](#o-problema)
- [Finalidade e objetivos](#finalidade-e-objetivos)
- [Funcionalidades](#funcionalidades)
- [Modelagem e arquitetura](#modelagem-e-arquitetura)
- [Planejamento e cronograma](#planejamento-e-cronograma)
- [Análise e simulação de atraso](#análise-e-simulação-de-atraso)
- [A apresentação](#a-apresentação)
- [Como executar](#como-executar)
- [Estrutura do repositório](#estrutura-do-repositório)
- [Vídeo da apresentação](#vídeo-da-apresentação)
- [Participantes](#participantes)

---

## Sobre o projeto

Este repositório reúne a apresentação em slides (HTML) e os artefatos de planejamento de um
**Sistema de Gestão Agrícola para Pequenos e Médios Produtores de Frutas Cítricas**, batizado de
**O Gerente**.

O projeto está na fase de **escopo e planejamento**: não há telas nem código do sistema. O que
existe é a definição do produto (finalidade, objetivos, funcionalidades, modelagem UML e arquitetura)
e o cronograma completo elaborado no **Monday.com**, com 7 fases e 53 atividades.

### O exemplo: Seu Ricardo

Para tornar o problema concreto, a apresentação usa um caso real: o **Seu Ricardo**, citricultor em
**Urânia-SP**, conhecido na família como *o Gerente* — daí o nome do sistema.

| | |
|---|---|
| Propriedade | 12 alqueires paulistas (~29 ha), dividida em talhões |
| Cultura | Laranja |
| Venda | Fruta vendida no pé — o comprador faz a colheita |
| Pessoas envolvidas | O produtor, o funcionário Luciano, um responsável técnico (agrônomo) e diaristas na colheita |

O Seu Ricardo é **um exemplo**: o sistema foi pensado para qualquer pequeno ou médio citricultor.

> Alguns dados da apresentação são ilustrativos e estão sinalizados como tal: o nome da agrônoma
> (Carla), os nomes dos talhões, os valores do painel e os mockups de tela (selo
> "Protótipo ilustrativo").

---

## O problema

Hoje a gestão da propriedade é feita **no caderno**, o que gera quatro dores principais:

1. **Gastos que escapam** — diesel, peças de reposição e reparos de equipamentos muitas vezes nem são anotados.
2. **Faturamento incerto** — o produtor não sabe ao certo quanto a safra rendeu.
3. **Estoque sem controle** — não há saldo confiável de defensivos, adubos e demais insumos.
4. **Sem histórico de aplicações** — não se sabe quais talhões receberam defensivo, quando e em que quantidade.

---

## Finalidade e objetivos

**Finalidade:** centralizar a gestão da propriedade citrícola em um sistema web simples, do plantio à colheita.

**Objetivos:**

1. Organizar propriedades, talhões e culturas em um só lugar
2. Registrar atividades agrícolas com data, local e responsável
3. Controlar o estoque de insumos com validação de saldo
4. Rastrear aplicações e ocorrências fitossanitárias
5. Acompanhar custos (diesel, manutenção e diárias incluídos) e o faturamento de cada safra
6. Apoiar decisões com dashboard e relatórios

---

## Funcionalidades

O sistema é dividido em oito módulos:

| Área | Módulo | Exemplo no sítio |
|---|---|---|
| Campo | **Propriedades e talhões** | Sítio dividido em 4 talhões de 3 alqueires |
| Campo | **Culturas e atividades agrícolas** | Adubação, poda e roçada por talhão |
| Campo | **Estoque de insumos** | Entradas e saídas com saldo atualizado |
| Campo | **Aplicações e ocorrências fitossanitárias** | Registro de fungicida aplicado em um talhão |
| Gestão | **Colheitas e custos** | Produção por talhão, diesel, peças e diárias |
| Gestão | **Painel (dashboard) e relatórios** | Faturamento, custos, saldo da safra e alertas |
| Gestão | **Perfis de acesso** | Produtor, funcionário e responsável técnico |
| Gestão | **Regras de negócio** | Bloqueio de aplicação sem saldo em estoque |

**Fora do escopo desta versão:** aviso de vencimento de boletos — registrado como próximo passo.

### Exemplo de regra de negócio

O funcionário tenta registrar a aplicação de **40 L** de fungicida, mas o estoque tem apenas **20 L**.
O sistema bloqueia a operação com a mensagem de **saldo insuficiente**. A validação fica no backend.

---

## Modelagem e arquitetura

### Atores (casos de uso)

- **Produtor** — gerencia a propriedade, custos, colheitas e acompanha o painel
- **Funcionário** — registra atividades, movimentações de estoque e aplicações
- **Responsável técnico** — orienta e acompanha as aplicações fitossanitárias

O caso de uso *Registrar aplicação* sempre **inclui** *Validar saldo de estoque*.

### Classes principais

| Grupo | Classes |
|---|---|
| Estrutura | Propriedade, Talhão, Cultura |
| Operação | Atividade, Aplicação, Insumo (com saldo) |
| Gestão | Colheita, Usuário (com perfil), Custo (com categoria) |

### Arquitetura

Arquitetura **cliente-servidor**:

```
Angular (frontend)
      │  HTTP / JSON
      ▼
API REST — Spring Boot
  Controller → Service → Repository
      │
      ▼
PostgreSQL
```

Tudo empacotado em **containers Docker** (frontend, backend e banco). A autenticação e a autorização
por perfil ficam com o **Spring Security**.

### Fluxo da regra de negócio (diagrama de sequência)

1. O funcionário salva a aplicação; a tela envia um `POST` para a API.
2. O **Controller** chama o **Service**.
3. O **Service** pede o saldo ao **Repository**, que consulta o banco: 20 L.
4. Como 20 < 40, o **Service** lança a exceção de saldo insuficiente.
5. O **Controller** devolve `422 Unprocessable Entity` e a tela exibe o alerta.

---

## Planejamento e cronograma

O planejamento foi feito no **Monday.com**: cada atividade tem responsável, datas de início e término,
duração, folga e dependência. A duração foi definida pela complexidade de cada tarefa.

- **Período:** 21/09/2026 a 18/03/2027 (179 dias)
- **Fases:** 7
- **Atividades:** 53

| # | Fase | Destaques |
|---|---|---|
| 1 | Levantamento de Requisitos | Stakeholders, entrevistas com produtores, AS-IS / TO-BE, requisitos funcionais e não funcionais |
| 2 | Análise de Sistemas | Atores e casos de uso, entidades do domínio, diagramas UML (casos de uso, classes, atividades), regras de negócio |
| 3 | Design | Arquitetura cliente-servidor e em camadas, modelo relacional, wireframes, Design System e protótipos no Figma |
| 4 | Implementação | Spring Boot + Angular, Spring Security, módulos do domínio, telas do frontend e integração com a API REST |
| 5 | Testes | Testes unitários (JUnit/Mockito), integração, endpoints (Postman), funcionais do frontend e aceitação |
| 6 | Implantação | Ambiente de produção, Docker, banco e backups, deploy, smoke tests, treinamento e implantação piloto |
| 7 | Manutenção | Monitoramento, correções pós-implantação e coleta de feedback |

**Divisão do trabalho:** 31 atividades do Lucas, 19 da Rhiady e 3 em dupla. Na implementação, as
frentes correm em paralelo — Lucas no backend e Rhiady no frontend — e se encontram na integração.

O cronograma completo também está exportado em
[`docs/Cronograma - Sistema de Gestão Agrícola.csv`](docs/Cronograma%20-%20Sistema%20de%20Gest%C3%A3o%20Agr%C3%ADcola.csv).

**Quadro no Monday.com:** <https://lucassabadinimendess-team.monday.com/boards/18433545202>

---

## Análise e simulação de atraso

- **Primeira atividade:** Identificar stakeholders do projeto (21/09/2026)
- **Última antes da manutenção:** Liberar implantação piloto (04/03/2027)
- **Maior atividade:** Desenvolver dashboard, colheitas, custos e relatórios (9 dias)
- **Folgas:** 19 atividades têm folga de 1 a 3 dias; **34 têm folga zero**
- **Atividade crítica:** Integrar frontend Angular com API REST (06/01 a 12/01/2027), com folga zero e ponto de encontro das duas frentes

### Simulação

Aplicando **5 dias de atraso** na integração do frontend com a API:

- os testes que dependem dela são empurrados;
- os testes funcionais do frontend tinham folga e não mudam;
- no fim, a fase de testes termina **apenas 1 dia depois**, e a implantação piloto **continua em 04/03/2027**.

**Conclusão:** nem todo atraso local vira atraso no prazo final. Dependências, folgas e paralelismo
permitem agir antes que um atraso de uma atividade se torne um atraso do projeto.

---

## A apresentação

A apresentação é um **arquivo HTML único e autocontido**
([`apresentacao-gestao-agricola.html`](apresentacao-gestao-agricola.html)), com 25 slides pensados
para gravação em tela cheia 16:9.

**Recursos:**

- Revelação de conteúdo **por etapas** — cada clique mostra o próximo bloco do slide
- Mockups ilustrativos do painel e da regra de negócio
- Diagramas UML de casos de uso e de classes
- Animação do diagrama de sequência da arquitetura
- **Zoom por fase** interativo no cronograma
- **Simulação de atraso** interativa
- Link direto para o quadro do Monday.com

**Divisão da fala:**

| Parte | Apresentador | Conteúdo |
|---|---|---|
| Abertura | Lucas | Capa e divisão das partes |
| Parte 1 — O projeto | Lucas Mendes | Seu Ricardo, problema, objetivos, funcionalidades, protótipos, UML e arquitetura |
| Parte 2 — O planejamento | Rhiady Vieira | Metodologia, cronograma, zoom por fase, Monday.com, análise e simulação de atraso |
| Encerramento | Os dois | Agradecimentos |

O roteiro completo da fala, slide a slide, está em [`roteiro-video.md`](roteiro-video.md).

### Tecnologias da apresentação

- HTML, CSS e JavaScript puros, sem build nem dependências
- Fontes Outfit, Inter e Caveat (Google Fonts)
- Paleta clara com acento nas cores da UNIFEF (laranja e verde-petróleo)

---

## Como executar

Não é preciso instalar nada.

1. Clone o repositório:
   ```bash
   git clone <url-do-repositorio>
   cd trabalho-boer
   ```
2. Abra `apresentacao-gestao-agricola.html` em um navegador moderno (Chrome, Edge, Firefox ou Safari).
3. Coloque em tela cheia (`F11`, ou `Ctrl+Cmd+F` no macOS).

**Navegação:**

| Tecla | Ação |
|---|---|
| `→` / `Espaço` / `Page Down` | Avança a próxima etapa ou o próximo slide |
| `←` / `Page Up` | Volta uma etapa ou um slide |
| `Home` / `End` | Vai para o primeiro / último slide |

Também é possível navegar pelos botões na tela. A conexão com a internet só é necessária para
carregar as fontes e abrir o quadro do Monday.com.

---

## Estrutura do repositório

```
trabalho-boer/
├── apresentacao-gestao-agricola.html   # Apresentação (arquivo único)
├── roteiro-video.md                    # Roteiro da fala, slide a slide
├── PRODUCT.md                          # Contexto, público e requisitos da apresentação
├── imagens/
│   └── logo-unifef.png                 # Logo da instituição
└── docs/
    ├── Cronograma - Sistema de Gestão Agrícola.csv   # Exportação do cronograma (53 atividades)
    └── superpowers/specs/
        └── 2026-09-30-parte-lucas-design.md          # Decisões de design da parte do Lucas
```

---

## Vídeo da apresentação

[![Assistir à apresentação no YouTube](https://img.youtube.com/vi/gffYAswOtgk/hqdefault.jpg)](https://youtu.be/gffYAswOtgk)

**Link:** <https://youtu.be/gffYAswOtgk>

---

## Participantes

| Nome | Responsabilidade na apresentação |
|---|---|
| **Lucas Mendes** | Parte 1 — O projeto: problema, objetivos, funcionalidades, protótipos, UML e arquitetura |
| **Rhiady Vieira** | Parte 2 — O planejamento: cronograma no Monday.com, análise e simulação de atraso |

<p align="center">
  UNIFEF · Sistemas de Informação · 6º semestre · 2026
</p>
