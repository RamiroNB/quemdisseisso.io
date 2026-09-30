# Quem disse isso?

**Ao vivo:** https://ramironb.github.io/quemdisseisso.io/

Portal e jogo da equipe **Ocarandu** no desafio *Ideias em Rede* do Instituto Kunumi (tema "IA e a Esfera Pública").

Audiências públicas da Câmara dos Deputados duram horas, e cada vez mais é uma IA que resume o que cada pessoa
disse. Às vezes o resumo põe na boca de alguém algo que a pessoa não disse. Este portal mostra, audiência por
audiência e pessoa por pessoa:

- o resumo gerado por um modelo aberto (Qwen3-4B), com cada linha conferida contra a própria fala da pessoa por
  juízes automáticos cegos;
- como o resumo ficaria **sem a correção**: um detector lê o estado interno do modelo e toca um alarme uma palavra
  antes de o texto sair da fala; então o sistema busca os trechos da própria fala e reescreve a linha;
- quem a matéria oficial da Agência Câmara citou e quem ficou de fora, e o que explica isso (tempo de fala e presidir
  a sessão; gênero, não).

E um jogo, **Seja o probe**: você faz o papel do detector e aperta ESPAÇO quando o alarme tocar. No alarme, as
ativações escapam do painel e tomam a tela; quem aperta a tempo vê o plano do probe (2.560 palavras reais, com o
limiar como uma reta), e quem não aperta vê as ativações caírem e o modelo seguir escrevendo.

## O que é real

Tudo o que aparece é pré-computado a partir de execuções reais; nada roda ao vivo no site.

- **Audiências e resumos:** as 100 audiências e 480 pessoas do experimento de busca e regeneração. O resumo sem
  correção e o corrigido saíram das mesmas execuções que foram julgadas às cegas.
- **Vereditos:** juízes automáticos cegos (Claude Sonnet e Claude Opus), calibrados contra os rótulos humanos do
  dataset.
- **Jogo:** as leituras do probe que de fato rodou como gatilho (camada 21 do Qwen3-4B, limiar 0,978).
- **Estimado ou automático:** os minutos de fala são estimados pelo número de palavras (140 por minuto), e os temas do
  mapa são extraídos automaticamente da transcrição.

O efeito da correção é pequeno e às vezes a reescrita erra; o portal mostra os dois lados. Os dados vêm do
[PublicHearingBR](https://huggingface.co/datasets/unicamp-dl/PublicHearingBR) (transcrições oficiais e matérias da
Agência Câmara).

## Rodar localmente

```bash
python3 serve.py 8803      # e abrir http://localhost:8803
```

É um site estático, sem build.

## Créditos

- **Equipe:** Ocarandu. O design partiu de um rascunho feito no Claude Design.
- **Bibliotecas:**
  - [Preact](https://preactjs.com) (MIT) e [htm](https://github.com/developit/htm) (Apache-2.0), em `vendor/`;
  - ícones [Lucide](https://lucide.dev) (ISC);
  - fontes Work Sans, Plus Jakarta Sans e IBM Plex Mono (Google Fonts, OFL).
