<div align="center">

# 🦐 Camarize

**Monitoramento IoT da qualidade da água para carcinicultura no Vale do Ribeira (SP)**

Projeto desenvolvido pela equipe **Progressus** — Desenvolvimento de Software Multiplataforma, FATEC Registro

![ESP32](https://img.shields.io/badge/ESP32-IoT-4F46E5?style=flat-square)
![Next.js](https://img.shields.io/badge/Next.js_14-PWA-2563EB?style=flat-square)
![Express](https://img.shields.io/badge/Node.js-Express-7C3AED?style=flat-square)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-4F46E5?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-Compose-2563EB?style=flat-square)
![CI](https://img.shields.io/badge/CI-GitHub_Actions-7C3AED?style=flat-square)

</div>

---

## O problema

O manejo de cativeiros de camarão na região ainda é predominantemente manual. Temperatura, pH e amônia afetam diretamente a saúde dos animais e a qualidade gastronômica do produto, e variações não percebidas a tempo geram perdas.

## A solução

Um sistema que liga sensores a um painel web e avisa o produtor quando algo sai da faixa ideal:

- **Coleta:** ESP32 lê temperatura, pH e amônia e envia à API a cada 1 minuto.
- **Painel (PWA):** valores atuais e gráficos históricos semanais por cativeiro.
- **Alertas:** os limites são definidos pelo usuário; ao ultrapassá-los, o sistema envia notificação push e e-mail.
- **Acesso por perfil:** proprietário (acesso completo) e funcionário (acesso operacional restrito).
- **Alimentação:** agendamento de horários e quantidades de ração, com acionamento por relé.

```
ESP32 ──HTTP/JSON──▶ API Express ──▶ MongoDB Atlas
(DS18B20 · Ph4502     (JWT · Swagger)      │
 · MQ-135 · relé)          │               │
                           ├──▶ alertas: push + e-mail
                           ▼
                  Front Next.js 14 (PWA)
```

## Resultados da validação

Seis testes em aquário com camarões e peixes, comparando o ESP32 com termômetro de aquário e kits químicos de referência.

| Componente | Resultado |
|---|---|
| Temperatura (DS18B20) | Erro médio 1,73% · precisão 98,27% · faixa testada 17,0–26,0 °C |
| pH (Ph4502) | Erro médio 4,02% · precisão 95,98% · desvio constante de ~0,2, corrigível por recalibração |
| Amônia (MQ-135) | Leu 0,000 ppm em todos os testes, coerente com a água recém-trocada. Não serve para quantificação em meio aquático (é um sensor de gás no ar) |
| Alerta ponta a ponta | Envio imediato |
| Alimentador | Lógica de horários e quantidades funcionou; o mecanismo físico apresentou instabilidade |

Os testes foram feitos em aquário, não em viveiro de produção. Detalhes e discussão no artigo.

## Repositórios

| Repositório | O que é | Stack |
|---|---|---|
| [**APP-0.2-CAMARIZE-V2**](https://github.com/Progressus-Camarize/APP-0.2-CAMARIZE-V2) | Plataforma completa: API, painel web, firmware do ESP32, documentação e CI. [Demo](https://app-0-2-camarize-v2.vercel.app) | Next.js 14, Express, MongoDB Atlas, Arduino/ESP32, Docker |
| [**CAMARIZE-BY-PROGRESSUS**](https://github.com/Progressus-Camarize/CAMARIZE-BY-PROGRESSUS) | Site institucional do projeto. [Ver site](https://camarize-by-progressus.vercel.app/) | Vite, React 18, TypeScript, Tailwind v4, Framer Motion |
| [**Artigo-cientifico**](https://github.com/Progressus-Camarize/Artigo-cientifico) | Artigo, slides e artefatos acadêmicos. [Ler o PDF](https://github.com/Progressus-Camarize/Artigo-cientifico/blob/main/template-paper-f299-artigo/artigo.pdf) | LaTeX, Beamer |

> `APP-0.2-CAMARIZE-V2` e `CAMARIZE-BY-PROGRESSUS` são forks de repositórios de [joaovitor101](https://github.com/joaovitor101).

## Rodando o projeto

Pré-requisitos: Node.js 18+ e Docker.

```bash
git clone https://github.com/Progressus-Camarize/APP-0.2-CAMARIZE-V2.git
cd APP-0.2-CAMARIZE-V2
cp api/.env.docker.example api/.env.docker   # preencha JWT_SECRET e as demais variáveis
cd tools && docker compose up --build
```

Frontend em `localhost:3000`, API em `localhost:4000` e documentação Swagger em `localhost:4000/api-docs`. O passo a passo completo está no README do repositório.

## Equipe

| Integrante | Atuação |
|---|---|
| [Tiago Rodrigues](https://github.com/tiagorodrigues9) | Pesquisa científica, documentação e redação do artigo |
| Leandro Augusto | IoT (Arduino e sensores) e design |
| Davi Mathais | Desenvolvimento full stack e design |

## Licença

Os repositórios estão sob licença MIT.
