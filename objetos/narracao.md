---
tipo: objeto
titulo: Narração
definicao: O áudio de um trecho de cerca de 5 minutos de um livro, lido pela voz de IA. É gerado sob demanda, um trecho de cada vez, para o Traça só pagar pelo que o leitor de fato ouve.
status: Pronto p/ dev
alertas: []
versao: 1.9
aprovado: 2026-11-10
---

# Narração

## Nome canônico

**Narração.** Não usar: *áudio*, *audiobook*, *leitura em voz alta*. Na interface, a ação do leitor é "ouvir".

## Atributos

| Atributo | Obrigatório | Regra |
|---|---|---|
| Livro | Sim | O [Livro](livro.md) a que pertence. |
| Trecho | Sim | O pedaço do livro que esta narração lê. Começa onde a voz vai tocar: a posição atual ou o ponto do texto em que o leitor tocou. Termina perto dos 5 minutos de áudio, no fim de um parágrafo ou na virada de capítulo, o que vier antes, em qualquer formato. Se o leitor toca num ponto mais à frente, o que ficou para trás não é gerado: o próximo trecho começa no ponto tocado. Uma parte do livro que já tem narração `Pronta` não é gerada de novo. Decidido pelo Matheus em 10/11/2026 e revisto em 12/11/2026. |
| Voz | Sim | A voz de IA usada, gerada pela Inworld, que devolve o tempo de cada palavra junto com o áudio. O modelo padrão é o TTS-2 Flash, a confirmar num teste de escuta contra o TTS-2. O leitor escolhe a voz entre todas as vozes em português do Brasil que a Inworld oferecer. Decidido pelo Matheus em 10/11/2026. Se o leitor troca de voz no meio de um livro, a voz nova vale a partir do próximo capítulo, para a voz não mudar no meio de um capítulo, e o app avisa o leitor disso na hora da troca. Decidido pelo Matheus em 10/11/2026. Em livro com um capítulo só, a voz nova começa no próximo trecho. Decidido pelo Matheus em 10/11/2026. |
| Áudio | Sim, a partir de `Pronta` | O arquivo de áudio gerado, guardado no aparelho. |
| Marcação de tempo | Sim, a partir de `Pronta` | O momento do áudio em que cada palavra ou frase é dita, para o texto na tela acompanhar a voz. |
| Duração | Sim, a partir de `Pronta` | Calculada a partir do áudio. |
| Gerada em | Sim, a partir de `Pronta` | Data e hora em que o áudio ficou pronto. |

## Ciclo de vida

Estados: `Gerando` · `Pronta` · `Com erro`

Um trecho que ainda não tem narração simplesmente não tem registro. A geração só começa quando o leitor vai precisar do áudio.

| De | Evento | Para | Quem | Efeitos |
|---|---|---|---|---|
| — | O leitor dá play, ou toca num ponto do texto, onde ainda não há narração | `Gerando` | Leitor | O texto do trecho vai para o serviço de voz. Cada geração tem custo. |
| — | O trecho que está tocando chega perto do fim e o próximo não tem narração | `Gerando` | App | Gera o próximo trecho antes de ele começar, para a voz não parar na virada. Quanto antes começar: decisão técnica de quem construir, com uma condição: o áudio nunca para entre um trecho e outro quando há internet. |
| `Gerando` | O serviço de voz devolve o áudio | `Pronta` | App | O áudio e a marcação de tempo ficam guardados no aparelho e tocam sem internet. |
| `Gerando` | O serviço de voz falha ou a internet cai | `Com erro` | App | O app tenta de novo sozinho até 3 vezes. Decidido pelo Matheus em 10/11/2026. |
| `Com erro` | As 3 tentativas automáticas falharam | `Com erro` | App | O leitor vê uma mensagem com o botão "Tentar de novo". Decidido pelo Matheus em 10/11/2026. |
| `Com erro` | O leitor toca em "Tentar de novo" | `Gerando` | Leitor | Recomeça a geração. |
| `Pronta` | O leitor exclui o livro | — | Leitor | O áudio é apagado do aparelho. |

Sem internet, o trecho com narração `Pronta` toca normalmente. Um trecho sem narração mostra um aviso de que precisa de conexão para ser gerado. Decidido pelo Matheus em 10/11/2026.

### O que NÃO tem, de propósito

- Não existe geração do livro inteiro, nem na importação nem depois. A narração nasce aos poucos, só do que o leitor está ouvindo. Decidido pelo Matheus em 10/11/2026.
- Não existe teto de horas de narração para quem tem assinatura na V1, nem visível nem escondido. O uso real é acompanhado nos primeiros meses (ver [Métricas](../metricas.md)) para decidir se entra um teto visível depois. Decidido pelo Matheus em 10/11/2026.

## Permissões

| Ação | Antes do teste | Em teste ou Ativa | Em carência | Expirada |
|---|---|---|---|---|
| Gerar narração nova | Só até 5 minutos de voz do livro importado, mesmo que passe de um capítulo para o outro | Sim | Não | Não |
| Tocar uma narração `Pronta` | Sim | Sim | Sim | Não |

Decidido pelo Matheus em 10/11/2026. A narração já gerada continua guardada quando a assinatura expira e volta a tocar se o leitor assinar de novo.

## Relacionamentos

| Relação | Cardinalidade | Regra |
|---|---|---|
| [Livro](livro.md) **tem** Narrações | 1:N, no máximo uma por trecho | Vínculo vivo. Excluir o livro apaga as narrações. |

## Usado nos fluxos

- [Ouvir um livro](../fluxos/ouvir-um-livro.md) · cobre toda a geração e a reprodução.
- [Começar a usar o Traça](../fluxos/comecar-a-usar-o-traca.md) · cobre os 5 minutos grátis antes do teste, que equivalem ao primeiro trecho.

## Faz parte de

- [Objetos](README.md)
