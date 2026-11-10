---
tipo: fluxo
titulo: Importar e excluir livros
ator: leitor com conta
job: pôr na biblioteca o livro que quer ouvir e tirar o que não quer mais
status: Desenhado
alertas: []
versao: 2.2
aprovado: 2026-11-10
prototipo: https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL
---

# Importar e excluir livros

## Protótipo

Desenhado no [canvas do Traça](https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL), página "App V1", linha IMP. Aprovado pelo Matheus em 10/11/2026.

- **IMP-001 · Biblioteca vazia** · convite para importar e os formatos aceitos.
- **IMP-002 · Biblioteca** · "Continuar ouvindo", grade de capas e mini player.
- **IMP-003 · Biblioteca · importando** · cards em importação junto com os livros prontos.
- **IMP-004 · Livro já está na biblioteca** · o aviso sobre o player do livro que já existia.
- **IMP-005 · Menu do livro** · menu com Excluir livro.
- **IMP-006 · Excluir livro** · diálogo de confirmação.
- **IMP-007 · Erro de formato** · aviso de formato não aceito na biblioteca.
- **IMP-008 · Busca com resultado** · a busca em uso, com os livros encontrados.
- **IMP-009 · Busca sem resultado** · "Nenhum livro encontrado".
- **IMP-010 · Erro de importação (DRM)** · aviso de proteção contra cópia na biblioteca.
- **IMP-011 · Erro · arquivo danificado** · aviso de arquivo danificado na biblioteca.

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
- **Excluir livro** sempre avisa que as marcações do livro também serão apagadas.
- A **Biblioteca** tem uma busca por título e autor, logo abaixo do título da tela. O resultado filtra a lista enquanto o leitor digita, sem precisar confirmar. Enquanto busca, "Continuar ouvindo" some e o botão "Cancelar" aparece ao lado do campo. Sem resultado, a tela diz "Nenhum livro encontrado", com o texto "Confira o nome ou importe o livro." e o botão "Importar livro". Decidido pelo Matheus em 10/11/2026.
- Com a assinatura expirada, o botão de importar leva ao paywall de [Assinar o Traça](assinar-o-traca.md). Excluir continua liberado.

### Mensagens

- DRM: "Este livro tem proteção contra cópia (DRM) e não abre fora da loja onde foi comprado. Tente um arquivo sem proteção."
- Arquivo corrompido: "Não conseguimos abrir este arquivo. Ele pode estar danificado. Tente baixar de novo."
- Formato não aceito: "O Traça ainda não abre esse tipo de arquivo. Ele abre EPUB, PDF, MOBI, AZW3, FB2, TXT e RTF."
- Livro repetido: "Este livro já está na sua biblioteca."
- Os avisos de erro de importação ficam na tela até o leitor fechar ou sair da biblioteca. Decidido pelo Matheus em 10/11/2026.
- **Excluir livro**: título "Excluir este livro?", texto "As marcações dele também serão apagadas. Não dá para desfazer.", botões "Excluir" e "Cancelar".

## Estados de UI

### Biblioteca

- **Ideal:** "Continuar ouvindo" com o último livro, e a lista de livros, pela última vez que foram abertos (as regras moram no [Livro](../objetos/livro.md#atributos)).
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

As telas usam os componentes do design system do canvas (página "Marca e design system", quadros DS-01 a DS-03), com o Liquid Glass descrito no [guia de marca](../marca.md#linguagem-visual-do-app). Os nomes de voz (Clara, Davi, Helena, Rafael), os livros e os tempos que aparecem nas telas são valores de exemplo.

- **IMP-001** · Biblioteca vazia
- **IMP-002** · Biblioteca
- **IMP-003** · Biblioteca · importando
- **IMP-004** · Livro já está na biblioteca
- **IMP-005** · Menu do livro
- **IMP-006** · Excluir livro
- **IMP-007** · Erro de formato

## Dentro do escopo

- Importar pelo app e pelo "Compartilhar", vários de uma vez, livro repetido, erro de importação, busca e exclusão.

## Fora do escopo

- Coleções, pastas e etiquetas. Voltam quando a biblioteca de um leitor típico passar de umas 30 obras.
- Editar título, autor ou capa.

## Fluxos conectados

- [Começar a usar o Traça](comecar-a-usar-o-traca.md) · a primeira importação, antes do login, segue as mesmas regras.
- [Ouvir um livro](ouvir-um-livro.md) · tocar num livro da biblioteca abre o player.

## Fluxos filhos

Nenhum.

## Faz parte de

- [Fluxos](README.md)
