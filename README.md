# Aurora - Agentes de IA | Continuum Inteligencia Contabil

Sistema de atendimento via WhatsApp com agentes de IA especializados, utilizando a plataforma **Atomos Chat**.

## Como funciona

```
Cliente (WhatsApp)
       |
       v
 AURORA SUPERVISOR
 (identifica a intencao e transfere)
       |
       v
 ┌─────┴──────────────────────────────────────┐
 │  9 Agentes Especializados                  │
 │                                            │
 │  01. Departamento Pessoal                  │
 │  02. Fiscal                                │
 │  03. Contabil                              │
 │  04. Financeiro                            │
 │  05. BPO Bancario                          │
 │  06. Processos Societarios                 │
 │  07. Comercial                             │
 │  08. Sucesso do Cliente (fallback)         │
 │  09. Institucional                         │
 └────────────────────────────────────────────┘
```

## Estrutura do repositorio

```
supervisor/           → Prompts e regras do supervisor
  prompt_perfil.txt   → Identidade do supervisor
  prompt_regras.txt   → Saudacao, roteamento, inatividade
  triagens/           → 1 arquivo por agente (texto detalhado de QUANDO transferir)

agentes/              → 9 agentes especializados
  XX_nome/
    base_conhecimento.txt  → Conteudo tecnico (FAQ do setor)
    transbordo.txt         → Identidade curta do agente (todos os agentes veem)

referencias/          → PDF de treinamento e screenshots da plataforma
```

## Onde colar na plataforma Atomos Chat

| Arquivo | Local na plataforma |
|---|---|
| `supervisor/prompt_perfil.txt` | Supervisor > Perfil > Descricao |
| `supervisor/prompt_regras.txt` | Supervisor > Perfil > Outras regras ou restricoes |
| `supervisor/triagens/triagem_XX.txt` | Supervisor > Logica de Distribuicao > [Agente] > aba **Triagem** |
| `agentes/XX/transbordo.txt` | Supervisor > Logica de Distribuicao > [Agente] > aba **Transbordo** |
| `agentes/XX/base_conhecimento.txt` | [Agente individual] > Base de Conhecimento |

## Equipe

- **Empresa:** Continuum Inteligencia Contabil
- **Plataforma:** Atomos Chat
- **IA:** Aurora
