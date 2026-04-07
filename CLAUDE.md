# Agente Helena - Projeto Continuum

## Visao Geral

Projeto de criacao de agentes inteligentes (IA Aurora) para atendimento via WhatsApp da empresa **Continuum Inteligencia Contabil**, utilizando a plataforma **Atomos Chat**. O sistema e composto por um **supervisor** que direciona as conversas para **agentes especializados**, cada um com sua propria base de conhecimento.

## Plataforma

- **Nome:** Atomos Chat
- **Provedor do Supervisor:** Aurora-supervisor
- **Modelo de raciocinio:** gpt-4.1
- **Simular tempo de digitacao:** 5 segundos

## Empresa

- **Nome:** Continuum Inteligencia Contabil
- **Desde:** 2017
- **Especialidade:** Contabilidade do Terceiro Setor
- **Clientes:** +400 ativos em todo territorio nacional
- **Referencia:** Nordeste
- **Sede:** R. Abelardo Barbosa, 200 - Nova Caruaru, Caruaru - PE, 55014-560
- **Unidades:** Caruaru (sede), Recife, Bezerros
- **Colaboradores:** +20

## Nome da IA

**AURORA** - Assistente virtual da Continuum

## Arquitetura: Supervisor vs Agentes

### Supervisor (Aurora Supervisor)
O supervisor NAO resolve duvidas. Ele apenas recebe o cliente, identifica a intencao e transfere para o agente correto. Na plataforma Atomos Chat, o supervisor tem 3 secoes:

- **Perfil** → Prompt que define a identidade do supervisor (`supervisor/prompt_perfil.txt`)
- **Logica de Distribuicao** → Lista dos 9 agentes, cada um com:
  - **Triagem** (aba) → Texto DETALHADO que o supervisor usa para decidir QUANDO transferir (`supervisor/triagens/triagem_XX_nome.txt`)
  - **Transbordo** (aba) → Texto CURTO que define a identidade do agente para todos os outros (`agentes/XX_nome/transbordo.txt`)
- **Configuracoes** → Regras de saudacao, inatividade, encerramento (`supervisor/prompt_regras.txt`)

### Agentes (9 especialistas)
Cada agente recebe o cliente ja direcionado pelo supervisor e responde com base no seu conhecimento especializado. Cada agente tem:
- **base_conhecimento.txt** → Conteudo tecnico (perguntas e respostas do setor)
- **transbordo.txt** → Texto curto de identidade (usado por todos os agentes e pelo supervisor)

## Estrutura de Pastas

```
agente_helena/
├── CLAUDE.md                              (este arquivo - documentacao do projeto)
├── supervisor/
│   ├── prompt_perfil.txt                  (identidade do supervisor)
│   ├── prompt_regras.txt                  (saudacao, roteamento, inatividade, encerramento)
│   └── triagens/
│       ├── triagem_01_departamento_pessoal.txt
│       ├── triagem_02_fiscal.txt
│       ├── triagem_03_contabil.txt
│       ├── triagem_04_financeiro.txt
│       ├── triagem_05_bpo_bancario.txt
│       ├── triagem_06_processos_societarios.txt
│       ├── triagem_07_comercial.txt
│       ├── triagem_08_sucesso_cliente.txt
│       └── triagem_09_institucional.txt
├── agentes/
│   ├── 01_departamento_pessoal/
│   │   ├── base_conhecimento.txt          (rotinas trabalhistas, CLT)
│   │   └── transbordo.txt                 (identidade curta do agente)
│   ├── 02_fiscal/
│   │   ├── base_conhecimento.txt          (notas fiscais, impostos, regimes)
│   │   └── transbordo.txt
│   ├── 03_contabil/
│   │   ├── base_conhecimento.txt          (escrituracao, balancete, DRE)
│   │   └── transbordo.txt
│   ├── 04_financeiro/
│   │   ├── base_conhecimento.txt          (boletos, pagamentos, CND)
│   │   └── transbordo.txt
│   ├── 05_bpo_bancario/
│   │   ├── base_conhecimento.txt          (acessos bancarios, 10 bancos)
│   │   └── transbordo.txt
│   ├── 06_processos_societarios/
│   │   ├── base_conhecimento.txt          (abertura/alteracao/encerramento)
│   │   └── transbordo.txt
│   ├── 07_comercial/
│   │   ├── base_conhecimento.txt          (servicos, propostas, leads)
│   │   └── transbordo.txt
│   ├── 08_sucesso_cliente/
│   │   ├── base_conhecimento.txt          (reclamacoes, fallback, CAJU)
│   │   └── transbordo.txt
│   └── 09_institucional/
│       ├── base_conhecimento.txt          (historia, localizacao, diferenciais)
│       └── transbordo.txt
└── referencias/
    ├── MINUTA TREINAMENTO DE IA – CONTINUUM.pdf
    └── screenshots/
```

## Agentes e suas Responsabilidades

### 1. Aurora Departamento Pessoal
Admissao, folha de pagamento, ferias, rescisao, eSocial, banco de horas, horas extras, beneficios, encargos trabalhistas.

### 2. Aurora Fiscal
Notas fiscais (NFS-e, NF-e), impostos (ISS, ICMS, PIS, COFINS), CFOP, regimes tributarios, retencoes, SPED, Fator R, CBS/IBS, IRPF, parcelamentos.

### 3. Aurora Contabil
Escrituracao contabil, balancete, DRE, balanco patrimonial, conciliacao, rateio, prestacao de contas, laudos, ITG 2002.

### 4. Aurora Financeiro
Boletos, comprovantes de pagamento, contas a pagar/receber, conciliacao bancaria, CND, parcelamentos, fornecedores.

### 5. Aurora BPO Bancario
Liberacao de acessos bancarios para BPO: Itau, Sicredi, Sicoob, Cora, Mercado Pago, Hinova Pay, Banco do Brasil, Caixa, Inter, Bradesco.

### 6. Aurora Processos Societarios
Abertura/encerramento de empresa, alteracoes contratuais, certificado digital, CNAEs, Junta Comercial.

### 7. Aurora Comercial
Apresentacao de servicos, propostas, orcamentos, captacao de leads, agendamento comercial, diferenciais.

### 8. Aurora Sucesso do Cliente
Reclamacoes, feedbacks, duvidas ambiguas, fallback universal, ponto digital, CAJU, mensagens genericas.

### 9. Aurora Institucional
Historia da empresa, localizacao, unidades, diferenciais, segmentos atendidos, dados institucionais.

## Onde colar cada texto na plataforma Atomos Chat

| Arquivo | Onde colar na plataforma |
|---|---|
| `supervisor/prompt_perfil.txt` | Supervisor > Perfil > Descricao |
| `supervisor/prompt_regras.txt` | Supervisor > Perfil > Outras regras ou restricoes |
| `supervisor/triagens/triagem_XX.txt` | Supervisor > Logica de Distribuicao > [Agente] > Editar > aba **Triagem** |
| `agentes/XX/transbordo.txt` | Supervisor > Logica de Distribuicao > [Agente] > Editar > aba **Transbordo** |
| `agentes/XX/base_conhecimento.txt` | [Agente individual] > Base de Conhecimento |

## Padrao de Respostas (aplicado em todos os agentes)

### Regras de comportamento
- Tom de WhatsApp: conversacional, simpatico, profissional
- Respostas curtas: maximo 3-4 linhas por bloco
- Apresentacao so 1 vez na conversa
- Hierarquia textual: negrito no essencial, pergunta de fechamento
- Prefere resumir e oferecer "quer que eu detalhe?" em vez de jogar tudo
- Entende girias e linguagem informal (opa, blz, vlw, eita, saquei, etc.)
- Emojis com moderacao (1-2 por mensagem no maximo)

### O que NAO pode (18 itens do PDF)
1. Omitir que se trata de uma inteligencia artificial
2. Enviar ou assinar documentos
3. Tomar decisoes em nome de terceiros
4. Emitir recomendacao unica de carater decisorio
5. Realizar fiscalizacoes
6. Criar autos de infracao
7. Registrar ou documentar multas
8. Enviar ou conduzir processos administrativos ou judiciais
9. Inventar prazos ou informacoes
10. Interpretar a legislacao de forma autonoma
11. Prometer resultados
12. Alterar procedimentos internos de cada empresa
13. Responder sem base documental valida
14. Enviar dados sensiveis (nome, telefone, e-mail, contas bancarias)
15. Alterar respostas com base exclusivamente em conversas anteriores
16. Utilizar jargoes tecnicos excessivos sem necessidade
17. Se apresentar mais de uma vez na mesma conversa
18. Enviar blocos enormes de texto

## Documentos de Referencia

- `referencias/MINUTA TREINAMENTO DE IA – CONTINUUM.pdf` — Documento principal com todas as regras, fluxos e base de treinamento
- `referencias/screenshots/` — Capturas de tela da plataforma Atomos Chat

## Legislacao Base

- Lei no 5.172/1966 (Codigo Tributario Nacional)
- Lei Complementar no 123/2006 (Simples Nacional)
- Instrucao Normativa da Receita Federal no 2.278/2025
- Lei Complementar no 213/2025
- CLT - Decreto-Lei no 5.452/1943
- Portaria 671/2021 do MTE

## Historico de Alteracoes

- **v1** — Bases de conhecimento criadas com conteudo completo do PDF (2.007 linhas, 96% compativel)
- **v2** — Reescrita para WhatsApp: respostas curtas, tom conversacional, girias, apresentacao unica (1.333 linhas, 91% compativel)
- **v3** — Reestruturacao completa do projeto:
  - Separacao de 5 agentes para 9 agentes especializados
  - Criacao da pasta `supervisor/` com perfil, regras e 9 triagens individuais
  - Criacao de `transbordo.txt` para cada agente (identidade curta)
  - Documentacao da arquitetura Supervisor vs Agentes
  - Tabela de mapeamento "onde colar cada texto" na plataforma Atomos Chat
  - Lista completa dos 18 itens "NAO PODE" do PDF
  - Inicializacao do repositorio git para distribuicao com a equipe
