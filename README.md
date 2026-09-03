# Automações & RPA (Python)

> Robôs em **Python / Selenium** que coletam, extraem e alimentam painéis de gestão — **eliminando trabalho manual recorrente**.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Selenium](https://img.shields.io/badge/Selenium-43B02A?style=flat-square&logo=selenium&logoColor=white)

> ⚠️ Repositório de **portfólio**: descreve arquitetura e boas práticas. Não contém código proprietário nem credenciais.

## O problema

Times de operação e gestão dependiam de **coletas manuais** repetitivas (baixar relatórios, consolidar planilhas, atualizar painéis). Trabalho lento, sujeito a erro e que consumia horas todo dia.

## O que eu construí

**10+ automações** em produção, entre elas:

- **Volumetria de Zendesk** — _scraping_ do dashboard, consolidação e exportação da tabela, gravando direto no _share_ de rede que alimenta os painéis.
- **Extração de chargeback** — coleta agendada de dados de disputa.
- **Cargas via SFTP** e replicações entre bases.
- **Painéis alimentados automaticamente** para acompanhamento em telas de gestão.

## Boas práticas aplicadas

- **ChromeDriver automático** via `webdriver-manager` / Selenium Manager (sem caminho fixo, sem quebrar em atualização do Chrome).
- **Resiliência** — _retry_, janela fixa, logs de erro com _traceback_ e _screenshot_ do momento da falha.
- **Agendamento** (execuções de madrugada, com filtro de data D-1 corrigido para fuso).
- **Segredos protegidos** — credenciais fora do versionamento (`.gitignore`), com guia de _setup_.
- **Empacotamento em executável** para implantação simples nas máquinas de operação.

## Stack

| Item | Tecnologia |
|---|---|
| Linguagem | Python |
| Automação | Selenium · webdriver-manager |
| Entrega | Executável empacotado · agendador · _share_ de rede (UNC) |

## Impacto

**Fim da coleta manual recorrente** — os dados passam a chegar sozinhos, no horário certo, alimentando os painéis de gestão sem intervenção humana.
