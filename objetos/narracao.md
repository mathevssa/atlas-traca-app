---
tipo: objeto
titulo: Narração
definicao: O áudio de um trecho de cerca de 5 minutos de um livro, lido pela voz de IA. É gerado sob demanda, um trecho de cada vez, para o Traça só pagar pelo que o leitor de fato ouve.
status: Clarificação
alertas: [Travado]
versao: 1.2
aprovado:
---

# Narração

## Nome canônico

**Narração.** Não usar: *áudio*, *audiobook*, *leitura em voz alta*. Na interface, a ação do leitor é "ouvir".

## Atributos

| Atributo | Obrigatório | Regra |
|---|---|---|
| Livro | Sim | O [Livro](livro.md) a que pertence. |
| Trecho | Sim | O pedaço do livro que esta narração lê: cerca de 5 minutos de áudio, sempre cortado no fim de um parágrafo, em qualquer formato. O trecho não depende dos capítulos do livro, que servem só para navegar. Existe no máximo uma narração por trecho. Decidido pelo Matheus em 10/11/2026. |
| Voz | Sim | A voz de IA usada. Qual serviço de voz e quantas vozes: A definir, em pesquisa. |
| Áudio | Sim, a partir de `Pronta` | O arquivo de áudio gerado, guardado no aparelho. |
| Marcação de tempo | Sim, a partir de `Pronta` | O momento do áudio em que cada palavra ou frase é dita, para o texto na tela acompanhar a voz. |
| Duração | Sim, a partir de `Pronta` | Calculada a partir do áudio. |
| Gerada em | Sim, a partir de `Pronta` | Data e hora em que o áudio ficou pronto. |

## Ciclo de vida

Estados: `Gerando` · `Pronta` · `Com erro`

Um trecho que ainda não tem narração simplesmente não tem registro. A geração só começa quando o leitor vai precisar do áudio.

| De | Evento | Para | Quem | Efeitos |
|---|---|---|---|---|
| — | O leitor dá play num trecho que não tem narração | `Gerando` | Leitor | O texto do trecho vai para o serviço de voz. Cada geração tem custo. |
| — | O trecho que está tocando chega perto do fim e o próximo não tem narração | `Gerando` | App | Gera o próximo trecho antes de ele começar, para a voz não parar na virada. Quanto antes começar: decisão técnica de quem construir, com uma condição: o áudio nunca para entre um trecho e outro quando há internet. |
| `Gerando` | O serviço de voz devolve o áudio | `Pronta` | App | O áudio e a marcação de tempo ficam guardados no aparelho e tocam sem internet. |
| `Gerando` | O serviço de voz falha ou a internet cai | `Com erro` | App | O app tenta de novo sozinho até 3 vezes. Decidido pelo Matheus em 10/11/2026. |
| `Com erro` | As 3 tentativas automáticas falharam | `Com erro` | App | O leitor vê uma mensagem com o botão "Tentar de novo". Decidido pelo Matheus em 10/11/2026. |
| `Com erro` | O leitor toca em "Tentar de novo" | `Gerando` | Leitor | Recomeça a geração. |
| `Pronta` | O leitor exclui o livro | — | Leitor | O áudio é apagado do aparelho. |

Sem internet, o trecho que já está `Pronta` toca normalmente. Um trecho sem narração mostra um aviso de que precisa de conexão para ser gerada. Decidido pelo Matheus em 10/11/2026.

### O que NÃO tem, de propósito

- Não existe geração do livro inteiro, nem na importação nem depois. A narração nasce aos poucos, só do que o leitor está ouvindo. Decidido pelo Matheus em 10/11/2026.
- Não existe limite de horas de narração para quem tem assinatura. Limitar o uso frustraria o leitor e não é a forma de rentabilizar o Traça. Decidido pelo Matheus em 10/11/2026.

## Permissões

| Ação | Antes do teste | Em teste ou Ativa | Em carência | Expirada |
|---|---|---|---|---|
| Gerar narração nova | Até 5 minutos de áudio no total, somando todos os livros | Sim | Não | Não |
| Tocar uma narração `Pronta` | Sim | Sim | Sim | Não |

Decidido pelo Matheus em 10/11/2026. A narração já gerada continua guardada quando a assinatura expira e volta a tocar se o leitor assinar de novo.

## Relacionamentos

| Relação | Cardinalidade | Regra |
|---|---|---|
| [Livro](livro.md) **tem** Narrações | 1:N, no máximo uma por trecho | Vínculo vivo. Excluir o livro apaga as narrações. |

## Usado nos fluxos

- Ouvir um livro (a escrever) · cobre toda a geração e a reprodução.
- Começar a usar o Traça (a escrever) · cobre os 5 minutos grátis antes do teste, que equivalem ao primeiro trecho.

## Faz parte de

- [Objetos](README.md)
