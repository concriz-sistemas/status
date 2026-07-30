# Status Concriz

<!--start: description-->
<!--end: description-->

Monitoramento de disponibilidade dos servicos Concriz, verificado a cada 5 minutos.

**Pagina de status:** https://qremmax.github.io/status

[![Uptime CI](https://github.com/qremmax/status/workflows/Uptime%20CI/badge.svg)](https://github.com/qremmax/status/actions/workflows/uptime.yml)
[![Response Time CI](https://github.com/qremmax/status/workflows/Response%20Time%20CI/badge.svg)](https://github.com/qremmax/status/actions/workflows/response-time.yml)
[![Graphs CI](https://github.com/qremmax/status/workflows/Graphs%20CI/badge.svg)](https://github.com/qremmax/status/actions/workflows/graphs.yml)
[![Static Site CI](https://github.com/qremmax/status/workflows/Static%20Site%20CI/badge.svg)](https://github.com/qremmax/status/actions/workflows/site.yml)
[![Summary CI](https://github.com/qremmax/status/workflows/Summary%20CI/badge.svg)](https://github.com/qremmax/status/actions/workflows/summary.yml)

## [📈 Status ao vivo](https://qremmax.github.io/status): <!--live status--> **🟩 Todos os servicos operacionais**

<!--start: status pages-->
<!--end: status pages-->

## O que e monitorado

| Servico | Endpoint | Criterio de queda |
| --- | --- | --- |
| API | `https://concriz.com/api/health` | HTTP nao-2xx **ou** corpo sem `"status":"ok"` |
| Site | `https://concriz.com/` | HTTP nao-2xx |
| Gestor Web | `https://concriz.com/web/` | HTTP nao-2xx **ou** corpo sem `flutter_bootstrap` |

Resposta acima de 5 s conta como **degradado**, nao como queda.

A API e o sinal mais confiavel de queda: sendo dinamica, a resposta vem sempre da
origem (HostGator) e nunca do cache do Cloudflare. Por isso ela tambem valida o
corpo — uma pagina de erro devolvida com HTTP 200 conta como queda.

## Como funciona

Nao existe servidor. O GitHub Actions faz o ping, o resultado e commitado em
`history/`, os graficos vao para `graphs/`, o resumo em JSON para `api/` e a
pagina estatica e publicada no GitHub Pages (branch `gh-pages`).

Cada queda abre uma **Issue** automaticamente neste repositorio, fechada sozinha
quando o servico volta — e isso alimenta o historico de incidentes da pagina.

**Latencia de deteccao:** o cron do GitHub Actions tem intervalo minimo de 5
minutos e costuma atrasar sob carga, entao uma queda aparece aqui em ~5 a 20 min.
Alerta mais rapido exigiria um monitor proprio rodando fora do GitHub.

## Configuracao

Tudo vive em [`.upptimerc.yml`](./.upptimerc.yml). Os arquivos em
`.github/workflows/` sao **gerados** a partir dele — nao editar na mao, porque a
atualizacao semanal do template sobrescreve.

<!--start: docs-->
<!--end: docs-->

Feito com [Upptime](https://upptime.js.org), que nao tem vinculo com o GitHub.
