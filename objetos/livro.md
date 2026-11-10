---
tipo: objeto
titulo: Livro
definicao: Um arquivo de ebook que o leitor importou para o Traça e que aparece na biblioteca, pronto para ler e ouvir.
status: Clarificação
alertas: []
versao: 1.0
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
| Capa | Não | Vem do arquivo. O que aparece quando o arquivo não tem capa: A definir. |
| Formato | Sim | EPUB, PDF, MOBI, AZW3, FB2, TXT ou RTF, sem DRM. A lista mora nos princípios da [Constituição](../constituicao.md#princípios). |
| Arquivo original | Sim | Cópia do arquivo que o leitor escolheu. Onde fica guardado (só no aparelho ou também no iCloud): A definir. |
| Capítulos | Sim | Lista ordenada, lida do sumário do arquivo. É a unidade da [Narração](narracao.md). Como dividir um arquivo sem sumário (comum em PDF e TXT): A definir. |
| Posição atual | Sim | O ponto do livro onde o leitor parou. Começa no início do livro. Se ler e ouvir compartilham a mesma posição: A definir. |
| Marcações | Não | Lista de pontos do livro que o leitor salvou para voltar depois. Cada marcação guarda a posição, o capítulo e a data em que foi criada. A marcação não tem nota nem cor e não serve para mais nada além de voltar ao ponto. Decidido pelo Matheus em 10/11/2026. |
| Importado em | Sim | Data e hora da importação, gerada pelo app. |
| Aberto em | Não | Data e hora da última vez que o leitor abriu o livro. Vazio até a primeira abertura. |

## Ciclo de vida

Estados: `Importando` · `Disponível`

| De | Evento | Para | Quem | Efeitos |
|---|---|---|---|---|
| — | Escolher um arquivo para importar | `Importando` | Leitor | O app copia o arquivo e começa a ler os metadados e o sumário. |
| `Importando` | Leitura do arquivo termina bem | `Disponível` | App | O livro aparece na biblioteca com título, autor e capa. Nenhuma narração é gerada nesse momento. |
| `Importando` | Arquivo com DRM, corrompido ou em formato não aceito | — | App | O livro não entra na biblioteca e o leitor vê uma mensagem com o motivo. Texto das mensagens: A definir. |
| `Disponível` | Criar uma marcação | `Disponível` | Leitor | A marcação entra na lista de marcações do livro. |
| `Disponível` | Excluir uma marcação | `Disponível` | Leitor | A marcação sai da lista. A posição atual não muda. |
| `Disponível` | Excluir o livro | — | Leitor | Apaga o arquivo original, a posição, as marcações e todas as narrações do livro. Se pede confirmação antes: A definir. |

### O que NÃO tem, de propósito

- Não existe limite de livros para quem tem assinatura. Decidido pelo Matheus em 10/11/2026.
- Não existem coleções, pastas nem etiquetas na V1: a biblioteca só importa e exclui. Decidido pelo Matheus em 10/11/2026.
- Não existem destaques de texto nem anotações na V1, só marcações. Decidido pelo Matheus em 10/11/2026.
- Arquivo com DRM não abre. A proteção impede qualquer leitor de terceiros de ler o arquivo, e o Traça não tenta contornar.

## Permissões

O que o leitor pode fazer depende só do estado da [Assinatura](assinatura.md).

| Ação | Em teste ou Ativa | Expirada |
|---|---|---|
| Ver o livro na biblioteca | Sim | Sim |
| Importar um livro | Sim | Não |
| Ler o livro | Sim | Não |
| Ouvir o livro | Sim | Não |
| Criar ou excluir marcação | Sim | Não |
| Excluir o livro | Sim | Sim |

Decidido pelo Matheus em 10/11/2026.

## Relacionamentos

| Relação | Cardinalidade | Regra |
|---|---|---|
| Livro **tem** [Narrações](narracao.md) | 1:N, no máximo uma por capítulo | Vínculo vivo. Excluir o livro apaga todas as narrações dele. |
| Livro **depende da** [Assinatura](assinatura.md) do leitor | N:1 | A assinatura não guarda livros: só decide o que o leitor pode fazer com eles. Quando a assinatura expira, os livros continuam na biblioteca. |

## Usado nos fluxos

- Importar e excluir livros (a escrever) · cobre `— → Importando → Disponível` e a exclusão.
- Ler um livro (a escrever) · cobre a posição atual e as marcações.
- Ouvir um livro (a escrever) · cobre a posição atual e os capítulos.

## Faz parte de

- [Objetos](README.md)
