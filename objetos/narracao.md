---
tipo: objeto
titulo: Narração
definicao: O áudio de um capítulo de um livro lido pela voz de IA. É gerado sob demanda, capítulo por capítulo, para o Traça só pagar pelo que o leitor de fato ouve.
status: Clarificação
alertas: []
versao: 1.0
aprovado:
---

# Narração

## Nome canônico

**Narração.** Não usar: *áudio*, *audiobook*, *leitura em voz alta*. Na interface, a ação do leitor é "ouvir".

## Atributos

| Atributo | Obrigatório | Regra |
|---|---|---|
| Livro | Sim | O [Livro](livro.md) a que pertence. |
| Capítulo | Sim | O capítulo do livro que esta narração lê. Existe no máximo uma narração por capítulo. |
| Voz | Sim | A voz de IA usada. Se o leitor escolhe a voz ou se existe uma voz só: A definir. |
| Áudio | Sim, a partir de `Pronta` | O arquivo de áudio gerado, guardado no aparelho. |
| Duração | Sim, a partir de `Pronta` | Calculada a partir do áudio. |
| Gerada em | Sim, a partir de `Pronta` | Data e hora em que o áudio ficou pronto. |

## Ciclo de vida

Estados: `Gerando` · `Pronta` · `Com erro`

Um capítulo que ainda não tem narração simplesmente não tem registro. A geração começa só quando o leitor vai precisar do áudio.

| De | Evento | Para | Quem | Efeitos |
|---|---|---|---|---|
| — | O leitor toca para ouvir um capítulo que não tem narração | `Gerando` | Leitor | O texto do capítulo vai para o serviço de voz. Cada geração tem custo. |
| — | Faltam poucas páginas para acabar o capítulo atual e o próximo não tem narração | `Gerando` | App | Gera a narração do próximo capítulo antes de ele começar, para o áudio não parar na virada. Quantas páginas antes: A definir. Se isso vale também quando o leitor só está lendo, sem ouvir: A definir. |
| `Gerando` | O serviço de voz devolve o áudio | `Pronta` | App | O áudio fica guardado no aparelho e pode tocar sem internet. |
| `Gerando` | O serviço de voz falha ou a internet cai | `Com erro` | App | O que o leitor vê e se o app tenta de novo sozinho: A definir. |
| `Com erro` | Nova tentativa | `Gerando` | Leitor ou App | Quem dispara e quantas vezes: A definir. |
| `Pronta` | O leitor exclui o livro | — | Leitor | O áudio é apagado do aparelho. |

### O que NÃO tem, de propósito

- Não existe geração do livro inteiro na importação. A narração nasce capítulo por capítulo, só para o que está sendo lido. Decidido pelo Matheus em 10/11/2026.
- Não existe limite de horas de narração para quem tem assinatura. Limitar o uso frustraria o leitor e não é a forma de rentabilizar o Traça. Decidido pelo Matheus em 10/11/2026.

## Permissões

| Ação | Em teste ou Ativa | Expirada |
|---|---|---|
| Disparar a geração | Sim | Não |
| Tocar uma narração `Pronta` | Sim | Não |

A narração já gerada continua guardada quando a assinatura expira e volta a tocar se o leitor assinar de novo.

## Relacionamentos

| Relação | Cardinalidade | Regra |
|---|---|---|
| [Livro](livro.md) **tem** Narrações | 1:N, no máximo uma por capítulo | Vínculo vivo. Excluir o livro apaga as narrações. |

## Usado nos fluxos

- Ouvir um livro (a escrever) · cobre toda a geração e a reprodução.

## Faz parte de

- [Objetos](README.md)
