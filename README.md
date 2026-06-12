# 🎧 Análise da Retrospectiva Spotify 2025 — *Wrapped Real*

Este projeto é a **sequência (e o upgrade)** da [Retrospectiva Spotify 2024](https://github.com/hian-stafford/retrospectiva_spotify_2024).

Se em 2024 o objetivo era **flagrar as discrepâncias** entre o que o Spotify mostra no Wrapped e o que realmente foi ouvido, em 2025 a pergunta ficou mais ambiciosa:

> **Quem eu sou musicalmente, não só o que eu ouço?**

A ideia é construir a retrospectiva que eu gostaria de ver: nada de cenários bonitinhos, "idade musical" ou métricas de vaidade. Aqui tudo é filtrado de **1º de janeiro a 31 de dezembro de 2025** e calculado a partir do meu histórico real de streaming — do número frio de minutos até o meu "DNA musical", minhas fases ao longo do ano e meus apegos.

**Mais detalhes da análise no notebook:**
[`spotify_retrospectiva_2025.ipynb`](spotify_retrospectiva_2025.ipynb)

---

## 📆 Por que analisar o ano inteiro?

O Spotify **começa a monitorar os dados do Wrapped em 1º de janeiro**, mas **encerra a coleta por volta de meados de novembro** — ou seja, o Wrapped oficial simplesmente **ignora as últimas semanas do ano** (justamente quando aparecem álbuns de fim de ano, climas natalinos e aquela playlist de virada).

Esse foi um dos achados do [projeto de 2024](https://github.com/hian-stafford/retrospectiva_spotify_2024), e é exatamente a lacuna que este projeto fecha: aqui a janela vai **até 31 de dezembro**, para uma retrospectiva mais verídica e completa.

---

## 🎯 Objetivos

- Construir uma retrospectiva **honesta e personalizada**, validando ou refutando o que o Spotify Wrapped apresenta.
- Ir além do ranking: entender **padrões de comportamento** — quando, como e com que intensidade eu ouço música.
- Traçar um **perfil de identidade musical** a partir do consumo real.
- Tornar tudo **visual**: cada padrão vira gráfico.

---

## 📊 Descrição dos Dados

Os dados vêm do **export oficial do Spotify** (a "Account Data"). O coração da análise é o **histórico de streaming**, com os campos:

- **`endTime`** — carimbo de data/hora (UTC) de quando a faixa parou de tocar.
- **`artistName`** — nome do artista/banda.
- **`trackName`** — nome da faixa.
- **`msPlayed`** — duração ouvida, em milissegundos.

Para as análises mais profundas, também foram usados:

- **`Playlist1.json`** — minhas 65 playlists (nome, data de modificação e faixas).
- **`YourLibrary.json`** — músicas, álbuns e artistas salvos.

> ⚠️ **Limitação importante:** o histórico **não traz gênero nem características de áudio** (energia, valência, BPM…). Por isso, as leituras "emocionais" usam **proxies comportamentais** (horário, repetição, diversidade, intensidade) — sem inventar "humor" que o dado não suporta.

---

## 🔍 Metodologia

1. **Conversão de tempo:** `msPlayed` → minutos, para leitura humana.
2. **Filtro de _skip_ (upgrade de 2025):** um "play" só conta a partir de **30 segundos ouvidos** (mesmo critério do Spotify), evitando que faixas puladas inflem as contagens. Os **minutos totais**, porém, somam tudo.
3. **Agregação:** agrupamentos por **dia, hora, dia da semana, mês, artista, faixa e playlist** com `pandas`.
4. **Análise honesta:** quando o dado contrariou a hipótese, a análise foi ajustada — por exemplo, como eu não "martelo" a mesma faixa dezenas de vezes no mesmo dia, o *hiperfoco* foi redefinido como obsessões concentradas numa **janela curta de tempo**.
5. **Tudo dinâmico:** os números das conclusões saem das variáveis calculadas, nunca digitados à mão.
6. **Visualização:** gráficos com `matplotlib` (barras, mapa de calor, séries temporais e **radar**).

---

## 🗂️ A história em duas partes

### Parte 1 — O Wrapped honesto (o básico, do jeito certo)

1. **Minutos totais** ouvidos no ano.
2. **Top 5 músicas** (por minutos) — *com gráfico*.
3. **A música mais ouvida.**
4. **O dia mais intenso do ano** — gráfico da janela de ±15 dias, comparação com a média, padrão de escuta (repetição × exploração) e horário dominante.
5. **Top 5 do dia mais intenso** — *com gráfico*.
6. **Top 5 artistas** — *com gráfico*.
7. **`.txt` com as 100 músicas mais ouvidas** → [`top_100_musicas_2025.txt`](top_100_musicas_2025.txt).

### Parte 2 — Quem eu sou musicalmente (o upgrade)

1. **🧬 Identidade Musical (DNA)** — scores de *exploração*, *centralização*, *repetição emocional* e *intensidade*, com interpretação automática e **gráfico de radar**.
2. **📅 Fases da Vida** — linha do tempo mensal (volume, diversidade, intensidade), classificação de cada mês (intenso / exploratório / silencioso / equilibrado) e o **artista-tema de cada mês**.
3. **🕒 Horários e Rotina** — **mapa de calor** hora × dia da semana, semana vs. fim de semana e distribuição por período do dia.
4. **📂 Playlists** — quantidade, tamanhos e como eu organizo (cronológicas, por artista, de clima/vibe, temáticas).
5. **🔁 Repetição e Apego** — taxa de repetição, **músicas de conforto**, **hiperfoco** e as músicas que **nunca me abandonaram**.

---

## 📈 Insights da análise

- **Realygust** e **MHRAP** comandaram o ano — e o **Realygust dominou todo o segundo semestre** como artista-tema mês após mês.
- **81% dos plays foram re-escutas**: eu vivo muito de voltar ao que já conheço, mas sem ficar preso a poucas faixas.
- Meu **DNA** revelou um perfil raro: **explorador com identidade forte** — circulo por muito som novo, mas sempre ancoro em poucos pilares.
- Eu sou da **noite** (38% dos minutos) e tenho **veia coruja** (18% na madrugada), com pico de escuta às **23h**.
- O ano teve **fases nítidas**: começo intenso (jan/fev), um meio bem exploratório (maio teve mais de 2.000 músicas diferentes) e um segundo semestre de companhia constante.
- **65 playlists**, mediana de 68 faixas, e em **40%** eu escrevo descrição (gosto de dar contexto.)

---

## 🎁 SEU WRAPPED REAL 2025 — RESUMO

```
====================================================
        🎁  SEU WRAPPED REAL 2025  —  RESUMO
====================================================

⏱️  44.641 minutos ouvidos  (~744 horas)
🥇  Música do ano: Novo Tango — Realygust
🎤  Artista do ano: Realygust

🧬  DNA musical:
      - exploracao: 0.67
      - centralizacao: 1.0
      - repeticao: 0.52
      - intensidade: 0.49

🔁  Repetição: 81% dos plays foram re-escutas
🛋️  Companhia do ano: Novo Tango (131 dias diferentes)
🕒  Pico às 23h  •  período dominante: Noite
📅  Mês mais musical: Jul  •  mais explorador: Mai
📂  65 playlists organizadas no ano

====================================================
```

> O Spotify te entrega cenários bonitinhos e uma "idade musical".
> Aqui você tem o que **realmente aconteceu** e por quê. 🎧

---

## 🔧 Ferramentas e Tecnologias

- **Python 3**
- **`pandas`** — manipulação e agregação dos dados.
- **`matplotlib`** — todas as visualizações (barras, mapa de calor, séries temporais e radar).
- **Ambiente:** Jupyter Notebook.

---

## 📝 Conclusão e Próximos Passos

Enquanto o projeto de 2024 mostrou **que** o Wrapped diverge da realidade, o de 2025 deu o passo seguinte: usar esses dados para entender **quem** é o ouvinte por trás dos números — minhas rotinas, fases e apegos.

### Próximos passos

- Enriquecer com **gênero e características de áudio** via API do Spotify, para uma leitura emocional de verdade.
- Cruzar com **múltiplos anos** para mapear a evolução do gosto ao longo do tempo.
- Transformar o cartão-resumo num **dashboard interativo**.

---

## 🛠️ Como Baixar Seus Dados Pessoais do Spotify

Quer rodar com os **seus** dados? O Spotify permite exportá-los:

### Passo 1 — Solicitar os dados

1. Acesse [www.spotify.com](https://www.spotify.com) e faça login.
2. Vá em **Perfil → Conta → Privacidade**.
3. Clique em **Baixar seus dados** e confirme a solicitação (inclua o histórico de reprodução / *streaming history*).

> **Nota:** o Spotify pode levar **até 30 dias** para processar e enviar os dados ao seu e-mail.

### Passo 2 — Baixar e extrair

1. Ao receber o e-mail, baixe o arquivo `.zip` e extraia o conteúdo.
2. Procure a pasta **`Spotify Account Data`**, com os arquivos `StreamingHistory_music_*.json`, `Playlist1.json`, `YourLibrary.json`, etc.

### Passo 3 — Preparar para a análise

1. Coloque a pasta `Spotify Account Data` dentro de `my_spotify_data2025_total/` (ou ajuste a variável `DATA_PATH` no notebook).
2. Instale as dependências e abra o notebook:

```bash
pip install pandas matplotlib jupyter
jupyter notebook spotify_retrospectiva_2025.ipynb
```

> 🔒 Os dados do export são **pessoais**. Este repositório já ignora a pasta de dados via [`.gitignore`](.gitignore). Não publique seu histórico sem querer.
