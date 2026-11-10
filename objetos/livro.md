---
tipo: objeto
titulo: Livro
definicao: Um arquivo de ebook que o leitor importou para o Traça e que aparece na biblioteca, pronto para virar audiolivro.
status: Clarificação
alertas: []
versao: 1.2
aprovado:
---

# Livro

## Nome canônico

**Livro.** Não usar: *arquivo*, *documento*, *ebook*, *obra*. "Arquivo" só aparece quando o assunto é o arquivo original que o leitor escolheu para importar.

## Atributos

| Atributo | Obrigatório | Regra |
|---|---|---|
| Título | Sim | Vem dos metadados do arquivo. Se o arquivo não tiver título, usa o nome do arquivo sem a extensão. |
| Autor | Não | Vem dos metadados do arquivo. Sem autor, a biblioteca não mostra nada no lugar. |
| Capa | Sim | Vem do arquivo. Se o arquivo não tiver capa, o app gera uma com o título em Young Serif sobre o Laranja-queimado, nas cores do [guia de marca](../marca.md). Decidido pelo Matheus em 10/11/2026. |
| Formato | Sim | EPUB, PDF, MOBI, AZW3, FB2, TXT ou RTF, sem DRM. A lista mora nos princípios da [Constituição](../constituicao.md#princípios). |
| Arquivo original | Sim | Cópia do arquivo que o leitor escolheu. Onde fica guardado (só no aparelho ou também no iCloud do leitor): A definir. |
| Impressão digital | Sim | Identifica o conteúdo do arquivo, para reconhecer quando o mesmo livro é importado de novo. Calculada pelo app na importação. |
| Capítulos | Não | Lista ordenada, lida do sumário do arquivo. Serve só para o leitor navegar: a narração é gerada em trechos e não depende dela. Arquivo sem sumário (comum em PDF e TXT) fica sem lista de capítulos. Decidido pelo Matheus em 10/11/2026. |
| Posição atual | Sim | O ponto do livro onde a narração parou. Começa no início do livro. A tela de texto sempre abre nessa mesma posição, e o play sempre continua dela. |
| Marcações | Não | Lista de pontos do livro que o leitor salvou para voltar depois. Cada marcação guarda a posição, o capítulo e a data em que foi criada. A marcação não tem nota nem cor e não serve para mais nada além de voltar ao ponto. Decidido pelo Matheus em 10/11/2026. |
| Importado em | Sim | Data e hora da importação, gerada pelo app. |
| Aberto em | Não | Data e hora da última vez que o leitor abriu o livro. Vazio até a primeira abertura. |

## Ciclo de vida

Estados: `Importando` · `Disponível`

| De | Evento | Para | Quem | Efeitos |
|---|---|---|---|---|
| — | Escolher um arquivo para importar | `Importando` | Leitor | O app copia o arquivo e começa a ler os metadados e o sumário. |
| `Importando` | Leitura do arquivo termina bem e o livro ainda não está na biblioteca | `Disponível` | App | O livro aparece na biblioteca com título, autor e capa. Nenhuma narração é gerada nesse momento. |
| `Importando` | A impressão digital é igual à de um livro que já está na biblioteca | — | App | A cópia é descartada, o leitor vê um aviso de que o livro já está na biblioteca e o livro existente abre. Decidido pelo Matheus em 10/11/2026. |
| `Importando` | Arquivo com DRM, corrompido ou em formato não aceito | — | App | O livro não entra na biblioteca e o leitor vê uma mensagem com o motivo. Texto das mensagens: no fluxo de importação. |
| `Disponível` | Criar uma marcação | `Disponível` | Leitor | A marcação entra na lista de marcações do livro. |
| `Disponível` | Excluir uma marcação | `Disponível` | Leitor | A marcação sai da lista. A posição atual não muda. |
| `Disponível` | Excluir o livro, depois de confirmar | — | Leitor | Apaga o arquivo original, a posição, as marcações e todas as narrações do livro. O app sempre pede confirmação antes. Decidido pelo Matheus em 10/11/2026. |

### O que NÃO tem, de propósito

- Não existe interface de leitura silenciosa. O texto na tela acompanha a narração. Decidido pelo Matheus em 10/11/2026.
- Não existe limite de livros para quem tem assinatura. Decidido pelo Matheus em 10/11/2026.
- Não existem coleções, pastas nem etiquetas na V1: a biblioteca só importa e exclui. Decidido pelo Matheus em 10/11/2026.
- Não existem destaques de texto nem anotações na V1, só marcações. Decidido pelo Matheus em 10/11/2026.
- Arquivo com DRM não abre. A proteção impede qualquer leitor de terceiros de ler o arquivo, e o Traça não tenta contornar.

## Permissões

O que o leitor pode fazer depende só do estado da [Assinatura](assinatura.md). "Antes do teste" é quem ainda não começou o teste grátis.

| Ação | Antes do teste | Em teste ou Ativa | Em carência | Expirada |
|---|---|---|---|---|
| Ver o livro na biblioteca | Sim | Sim | Sim | Sim |
| Importar um livro | Sim. Quantos: A definir | Sim | Sim | Não |
| Ouvir e acompanhar o texto | Só os 5 minutos grátis | Sim | Só o que já foi gerado | Não |
| Criar ou excluir marcação | Sim | Sim | Sim | Não |
| Excluir o livro | Sim | Sim | Sim | Sim |

Decidido pelo Matheus em 10/11/2026. O que cada estado permite gerar de narração está na [Narração](narracao.md#permissões).

## Relacionamentos

| Relação | Cardinalidade | Regra |
|---|---|---|
| Livro **tem** [Narrações](narracao.md) | 1:N | Vínculo vivo. Excluir o livro apaga todas as narrações dele. |
| Livro **depende da** [Assinatura](assinatura.md) do leitor | N:1 | A assinatura não guarda livros: só decide o que o leitor pode fazer com eles. Quando a assinatura expira, os livros continuam na biblioteca. |

## Usado nos fluxos

- Importar e excluir livros (a escrever) · cobre `— → Importando → Disponível`, o livro repetido e a exclusão.
- Ouvir um livro (a escrever) · cobre a posição atual, os capítulos e as marcações.

## Faz parte de

- [Objetos](README.md)
