# Automações & RPA (Python)

> Robôs em **Python / Selenium** que coletam, extraem e alimentam painéis de gestão — **eliminando trabalho manual recorrente**.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Selenium](https://img.shields.io/badge/Selenium-43B02A?style=flat-square&logo=selenium&logoColor=white)

> ⚠️ Repositório de **estudo de caso**: descreve arquitetura e boas práticas — sem código proprietário nem credenciais.
>
> ▶️ **Quer ver um robô rodando?** Fiz um de código aberto com as mesmas práticas: **[rpa-coletor](https://github.com/raul-caetano/rpa-coletor)** (Selenium + testes).

## ▶️ Um robô do mesmo tipo, rodando

_(execução do meu robô de demonstração — [rpa-coletor](https://github.com/raul-caetano/rpa-coletor))_

![Execução do robô](https://raw.githubusercontent.com/raul-caetano/rpa-coletor/main/docs/execucao.png)

## O problema

Times de operação e gestão dependiam de **coletas manuais** repetitivas (baixar relatórios, consolidar planilhas, atualizar painéis). Trabalho lento, sujeito a erro e que consumia horas todo dia.

## O que eu construí

**10+ automações** em produção: volumetria de Zendesk, extração de chargeback, cargas via SFTP, replicações e painéis alimentados automaticamente — agendados, gravando direto no _share_ de rede que alimenta os painéis.

## 🔧 Prática em destaque (reescrita de forma ilustrativa)

**Resiliência é o que faz um robô sobreviver em produção.** Cada passo tenta de novo com _backoff_ e, na falha, salva um _screenshot_ da tela para diagnóstico:

```python
def coletar_com_retry(driver, url, logger, tentativas, dir_saida):
    for tentativa in range(1, tentativas + 1):
        try:
            return coletar_pagina(driver, url, logger)
        except Exception as e:
            logger.warning("  falha na tentativa %d/%d: %s", tentativa, tentativas, e)
            _screenshot_erro(driver, dir_saida, logger)   # print no momento do erro
            if tentativa == tentativas:
                raise
            time.sleep(2 * tentativa)                      # backoff crescente
```

Somado a: **ChromeDriver automático** (não quebra quando o Chrome atualiza), **log estruturado**, **CSV pt-BR** (`;` + BOM), **nome de arquivo D-1** para execuções de madrugada e **segredos por ambiente** (`.env`, nunca no código).

## Stack

| Item | Tecnologia |
|---|---|
| Linguagem | Python |
| Automação | Selenium · Selenium Manager |
| Entrega | Executável empacotado · agendador · _share_ de rede (UNC) |

## Impacto

**Fim da coleta manual recorrente** — os dados passam a chegar sozinhos, no horário certo, alimentando os painéis de gestão sem intervenção humana.
