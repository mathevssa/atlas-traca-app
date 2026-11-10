---
tipo: fluxo
titulo: Importar e excluir livros
ator: leitor com conta
job: pôr na biblioteca o livro que quer ouvir e tirar o que não quer mais
status: Clarificação
alertas: []
versao: 1.0
aprovado:
prototipo:
---

# Importar e excluir livros

## Protótipo

Ainda não desenhado.

Telas que esta página descreve (nomes provisórios até o protótipo existir):

- **Biblioteca** · a tela inicial do app para quem já tem conta.
- **Importando** · o card do livro enquanto o arquivo é lido.
- **Livro já está na biblioteca** · aviso quando o mesmo arquivo é importado de novo.
- **Excluir livro** · o diálogo de confirmação.

## Job to be Done

"Comprei ou baixei um livro e quero ouvir agora." E, do outro lado: "terminei, não quero mais esse livro aqui."

## Objetos

- [Livro](../objetos/livro.md) · cobre `— → Importando → Disponível`, o livro repetido e a exclusão.
- [Narração](../objetos/narracao.md) · a exclusão do livro apaga as narrações.

## Fluxo

1. O leitor toca em importar na **Biblioteca**, ou usa o "Compartilhar" de outro app (Arquivos, Mail, navegador) e escolhe o Traça.
2. O livro aparece na **Biblioteca** como **Importando**.
3. A leitura do arquivo termina.
   - Livro novo: o card mostra capa, título e autor, pronto para tocar.
   - Mesmo livro já na biblioteca: o leitor vê **Livro já está na biblioteca** e o livro existente abre.
   - Arquivo com DRM, corrompido ou em formato não aceito: o card some e o leitor vê o motivo.
4. Para excluir, o leitor escolhe excluir no livro e confirma em **Excluir livro**.
   - Confirmou: o livro, as marcações e o áudio gerado somem.
   - Cancelou: nada muda.

## Regras

- Importar funciona pelo botão da **Biblioteca** e pelo "Compartilhar" do iOS. Os dois caminhos dão o mesmo resultado.
- O leitor pode importar vários arquivos de uma vez pelo seletor do iOS. Cada um vira um card **Importando**.
- Importar não gera narração. A voz só é gerada quando o leitor dá play.
- **Excluir livro** sempre explica que as marcações e o áudio já gerado também serão apagados.
- Com a assinatura expirada, o botão de importar leva ao paywall de [Assinar o Traça](assinar-o-traca.md). Excluir continua liberado.

## Estados de UI

### Biblioteca

- **Ideal:** "Continuar ouvindo" com o último livro, e a lista de livros, do mais recente para o mais antigo.
- **Vazio:** convite para importar o primeiro livro, com o botão de importar e a lista de formatos aceitos.
- **Erro:** a mensagem do motivo da importação que falhou, como aviso no rodapé da tela.
- **Parcial:** livros em **Importando** aparecem junto com os prontos.
- **Carregando:** não se aplica, porque a biblioteca vem do aparelho.

## Critérios de aceite

- **Quando** o leitor importa um arquivo aceito, o livro deve aparecer na biblioteca com título, autor e capa (gerada, se o arquivo não tiver).
- **Se** o arquivo tem DRM, **então** o app deve dizer que livros protegidos não abrem, sem tentar converter.
- **Se** o mesmo arquivo é importado de novo, **então** o app não deve criar um segundo livro.
- **Quando** o leitor confirma a exclusão, o livro, as marcações e o áudio devem ser apagados do aparelho e da conta.

## Componentes e telas

A definir no design.

## Dentro do escopo

- Importar pelo app e pelo "Compartilhar", vários de uma vez, livro repetido, erro de importação e exclusão.

## Fora do escopo

- Coleções, pastas, etiquetas e busca na biblioteca. Voltam quando a biblioteca de um leitor típico passar de umas 30 obras.
- Editar título, autor ou capa.

## Definições pendentes

- Texto literal das mensagens de erro de importação (DRM, corrompido, formato não aceito). · Matheus, na rodada de design.

## Fluxos conectados

- [Começar a usar o Traça](comecar-a-usar-o-traca.md) · a primeira importação, antes do login, segue as mesmas regras.
- [Ouvir um livro](ouvir-um-livro.md) · tocar num livro da biblioteca abre o player.

## Fluxos filhos

Nenhum.

## Faz parte de

- [Fluxos](README.md)
