# gitbombando â€” Bombando no GitHub

[![Bombando no GitHub](guia/assets/banner.jpg)](https://inematds.github.io/gitbombando/guia/)

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## O que Ã©

O gitbombando faz sozinho, todo dia, um reel vertical (9:16) chamado **Bombando no GitHub** (sai Ã s 11h) e dois carrossÃ©is de
Instagram: o **Top 10 do GitHub** (14h) e o **Top da Ã¡rea** (18h, uma Ã¡rea por dia da semana). O reel mostra os 10 projetos que mais
ganharam estrelas no GitHub naquele dia, em contagem regressiva do #10 ao #1. Cada projeto aparece num cartÃ£o com a posiÃ§Ã£o,
a foto do dono, o que ele faz em portuguÃªs simples e o nÃºmero de estrelas, com um contador e um grÃ¡fico embaixo. O avatar do
Nei apresenta tudo com chamada forte e fecha pedindo um comentÃ¡rio. Aos domingos sai tambÃ©m o Top 10 da semana, e no dia 1Âº o
do mÃªs. O vÃ­deo vai para o YouTube (canal lives4), para o Instagram e o TikTok @inema.tds, para o bot do Nei e para um tÃ³pico fixo
do grupo INEMA.TOOLS no Telegram. Os carrossÃ©is vÃ£o para o Instagram e o TikTok @inema.tds e para um tÃ³pico fixo do grupo
INEMA.DEV no Telegram. Ã‰ para quem quer saber o que estÃ¡ bombando em tecnologia sem ler inglÃªs nem cÃ³digo. Roda na mÃ¡quina do INEMA
(Python, Node, Codex, Claude Code e a assinatura do HeyGen).

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/gitbombando/guia/**

---

## O processo, do inÃ­cio ao fim (13 passos)

ðŸ§  = sessÃ£o com o Nei (gasta tokens) Â· âš™ï¸ = script/timer (zero token) Â· ðŸ¤– = `claude -p` curto (sessÃ£o nova)

| # | Passo | Comando / o que acontece | Quem |
|---|---|---|---|
| 0 | Retrato das estrelas | timer `gitbombando-retrato` de hora em hora: `coleta/retrato.py` guarda as estrelas dos projetos em alta em `historico/estrelas.jsonl` (vira a curva dos grÃ¡ficos) | âš™ï¸ |
| 1 | Agenda | timer `gitbombando.timer` Ã s **09:00** â†’ `auto/rodar.sh <dia>` (gera com o estÃºdio do HeyGen livre): o dia sempre, publicado Ã s **11:00** (`GB_PUBLICAR_AS`); no domingo, depois dele, a semana e, no dia 1Âº, o mÃªs, que saem assim que ficam prontos (comeÃ§o da tarde) | âš™ï¸ |
| 2 | Coleta | `coleta/trending.py <pasta> dia\|semana\|mes`: pÃ¡gina do GitHub Trending + API do GitHub (descriÃ§Ã£o, README, linguagem, estrelas, foto do dono); Top 10 ordenado pelas estrelas ganhas â†’ `pesquisa/top10.json`; com menos de 10 no Trending espera atÃ© 1 h e, se ainda faltar, segue com Top N (mÃ­nimo 5) | âš™ï¸ |
| 3 | Roteiro | `claude -p` com `auto/roteiro.md` escreve `ficha.yaml`: gancho sensacionalista com o fato mais forte, panorama, #10 â†’ #1, pergunta final | ðŸ¤– |
| 4 | PortÃ£o do roteiro | `python3 gb.py checar <pasta>`: N+3 partes na ordem (13 no Top 10), projetos certos, 1.300â€“2.500 caracteres, manchete â‰¤ 6 palavras, sem algarismo na fala, "vocÃª", CTA sÃ³ inema.club | âš™ï¸ |
| 5 | Avatar + imagens | `gb.py fazer`: fala ao estÃºdio do HeyGen (assinatura; autorizaÃ§Ã£o em pÃ© do Nei, 28/10/2026) e, ao mesmo tempo, capa com a manchete (Codex), ranking, 10 cartÃµes e print do inema.club | âš™ï¸ |
| 6 | Montagem | tempo de cada palavra (Whisper), ritmo (~182 palavras/min, pausa antes do #1), cena com contador e grÃ¡fico em cada projeto, render no motor de telejornal | âš™ï¸ |
| 7 | RevisÃ£o | `claude -p` com `auto/revisor.md` lÃª a folha de 18 quadros: aprovado segue; reprovado para e avisa no v3 | ðŸ¤– |
| 8 | Publicar | `gb.py publicar`: YouTube **lives4** (yt-pubx, tÃ­tulo com #Shorts, links dos 10 na descriÃ§Ã£o) â†’ bot **v3** â†’ tÃ³pico fixo **BOMBANDO NO GITHUB** no INEMA.TOOLS | âš™ï¸ |
| 8b | Metritds | `auto/metritds.sh <pasta>`: sobe o vÃ­deo na release `social` do repo e agenda (agora + 10 min) no **Instagram + TikTok inema.tds** (marca do lives4) pelo Metricool da conta inematds (conector `metricool-inematds`, via `claude -p`); dia ~11:10, semana 13:00, mÃªs 15:00; aviso azul no v3 | ðŸ¤– |
| 9 | Guardar | git commit + push (roteiro, dados e histÃ³rico; mÃ­dia fica fora) | âš™ï¸ |
| 10 | Carrossel Top 10 | timer `gitbombando-carrossel-top10` Ã s 12:45 â†’ `auto/carrossel.sh <dia> top10` (publica Ã s **14:00**): reusa a coleta do vÃ­deo; `claude -p` com `carrossel/textos.md` escreve gancho, "o que Ã©", 2 benefÃ­cios e o fluxo de cada um; print de cada projeto tirado do README (`carrossel/prints.py`); 12 slides 1080Ã—1350 (`carrossel/render.mjs`); portÃ£o do texto e do desenho; revisor `claude -p` (`carrossel/revisor.md`) | âš™ï¸ðŸ¤– |
| 11 | Carrossel da Ã¡rea | timer `gitbombando-carrossel-area` Ã s 16:45 â†’ `auto/carrossel.sh <dia> area` (publica Ã s **18:00**): `carrossel/area.py` busca no GitHub os repositÃ³rios da Ã¡rea do dia criados nos Ãºltimos 120 dias, ordenados por estrelas por dia, sem repetir as Ãºltimas 8 semanas e sem conteÃºdo adulto; depois o mesmo caminho do passo 10 com 8 projetos | âš™ï¸ðŸ¤– |
| 12 | Publicar o carrossel | `carrossel/carrossel.py publicar`: Ã¡lbum no tÃ³pico fixo **BOMBANDO NO GITHUB - CarrossÃ©is diÃ¡rios** do **INEMA.DEV** (Telegram) â†’ carrossel no Instagram + fotos no TikTok **inema.tech** (marca FTD = lives3, desde 09/11/2026; Metricool, agora + 10 min, legenda sem link) â†’ aviso azul no v3 â†’ git. Reprovado = nÃ£o publica e avisa no v3 | âš™ï¸ðŸ¤– |

Teste sem publicar: `ED=/tmp/teste-video AVATAR_DE=<avatar.mp4> SEM_YT=1 SEM_BOT=1 SEM_TG=1 SEM_METRI=1 SEM_GIT=1 GB_SEM_HISTORICO=1 auto/rodar.sh 2026-10-28 dia`.
Carrossel sem publicar: `ED=/tmp/teste SEM_TG=1 SEM_METRI=1 SEM_BOT=1 SEM_GIT=1 auto/carrossel.sh 2026-11-04 area`
(`RASCUNHO=1` no lugar de `SEM_METRI=1` agenda no Metricool como rascunho).
Pular um dia: linha `AAAA-MM-DD` (ou `AAAA-MM-DD semana`, `AAAA-MM-DD carrossel`, `AAAA-MM-DD carrossel-top10`, `AAAA-MM-DD carrossel-area`) em `auto/pular.txt`.

## InstalaÃ§Ã£o dos timers (uma vez)

```bash
cp auto/systemd/gitbombando* ~/.config/systemd/user/
systemctl --user daemon-reload
systemctl --user enable --now gitbombando-retrato.timer gitbombando.timer gitbombando-carrossel-top10.timer gitbombando-carrossel-area.timer
```

## O que aparece no vÃ­deo

- **Capa (quadro 0):** chamada grande "TOP 10 DO GITHUB" no alto + manchete de atÃ© 6 palavras desenhada pelo Codex, com o nÃºmero mais forte do dia em amarelo.
- **Panorama:** os 10 em barras (estrelas ganhas) e a soma num contador.
- **Cada projeto:** cartÃ£o com `#posiÃ§Ã£o`, foto do dono, nome, o que faz em portuguÃªs, linguagem, total de estrelas e data de
  criaÃ§Ã£o. Embaixo, o contador das estrelas ganhas chegando ao nÃºmero no instante em que Ã© dito e o grÃ¡fico: a curva por hora
  (dia) ou por dia (semana/mÃªs) quando jÃ¡ hÃ¡ retratos, ou "antes Ã— agora" com o crescimento em %.
- **Fecho:** pergunta em caixa vermelha, o gesto do comentÃ¡rio sendo digitado e a pÃ­lula inema.club.

## Os carrossÃ©is

- **Capa:** mosaico com os prints dos projetos, "TOP 10 DO GITHUB HOJE" (ou "TOP 8" + a Ã¡rea), uma manchete de atÃ© 6 palavras e
  a soma das estrelas.
- **Um slide por projeto** (do #1 em diante): posiÃ§Ã£o, nome, gancho de 2 linhas, o print do README com as estrelas ganhas, "O que
  Ã©", 2 benefÃ­cios, "como usa" em 3 passos e o link do repositÃ³rio com o total de estrelas.
- **Fecho:** "os links estÃ£o na legenda", a lista dos projetos, a agenda do dia e inema.club. A legenda traz os links.
- **Ãreas:** segunda agentes de IA Â· terÃ§a Claude Code e MCP Â· quarta IA para vÃ­deo e imagem Â· quinta seguranÃ§a Â· sexta
  automaÃ§Ã£o Â· sÃ¡bado dev web e apps Â· domingo IA no seu PC (`carrossel/area.py`, `AREAS`).

## Fontes e limites

- SÃ³ a pÃ¡gina github.com/trending e a API do GitHub. A lista de stargazers da API responde 404 desde 2026, por isso a curva
  nasce dos retratos de hora em hora do prÃ³prio projeto.
- O Top 10 Ã© ordenado pelas estrelas ganhas no perÃ­odo (a ordem da pÃ¡gina do Trending mistura outros sinais).

LicenÃ§a MIT.

---

Projeto adaptado da comunidade INEMA TDS - Marca Arckhe