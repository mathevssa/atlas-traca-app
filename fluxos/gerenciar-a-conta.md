---
tipo: fluxo
titulo: Gerenciar a conta
ator: leitor com conta
job: ver a assinatura, sair da conta ou apagar tudo quando quiser
status: Clarificação
alertas: []
versao: 1.1
aprovado:
prototipo:
---

# Gerenciar a conta

## Protótipo

Ainda não desenhado.

Telas que esta página descreve (nomes provisórios até o protótipo existir):

- **Conta** · dados da conta, assinatura e ações.
- **Excluir conta** · o diálogo de confirmação.

## Job to be Done

"Quero saber o que estou pagando, trocar de aparelho sem perder nada e, se eu quiser, sair de vez."

## Objetos

- [Conta](../objetos/conta.md) · cobre sair e excluir.
- [Assinatura](../objetos/assinatura.md) · só leitura: o estado e o fim do período.

## Fluxo

1. O leitor abre **Conta** pela biblioteca.
2. **Conta** mostra o e-mail, o provedor (Apple ou Google), o estado da assinatura e a data da próxima cobrança ou do fim do acesso.
3. Ações:
   - **Gerenciar assinatura** abre os Ajustes de assinaturas do iPhone.
   - **Sair** encerra a conta neste aparelho, sem confirmação, e volta para **Boas-vindas**.
   - **Excluir conta** abre o diálogo de confirmação.
4. Em **Excluir conta**, o leitor lê o que vai ser apagado e o aviso de que a assinatura da App Store continua até ser cancelada, com o link para cancelar.
   - Confirmou: tudo é apagado e o app volta para **Boas-vindas**.
   - Cancelou: nada muda.

## Regras

- Excluir a conta fica dentro do app, a no máximo dois toques da tela **Conta**, como exige a App Store.
- **Excluir conta** lista o que o leitor perde: os livros, as marcações e onde parou em cada livro. O áudio gerado também é apagado, mas não aparece no texto, porque não importa para quem lê.
- Sair não apaga nada da conta. Ao entrar de novo, a biblioteca volta.

## Estados de UI

### Conta

- **Ideal:** dados da conta, assinatura e ações.
- **Erro:** a exclusão falhou por falta de internet: aviso de que excluir precisa de conexão, e nada é apagado.
- **Carregando:** enquanto a exclusão acontece, o diálogo mostra um indicador e não pode ser fechado.

## Critérios de aceite

- **Quando** o leitor confirma a exclusão, todos os dados da conta devem ser apagados do servidor e do aparelho.
- **Se** a exclusão falha, **então** nada deve ser apagado pela metade.
- **Quando** o leitor sai da conta, a biblioteca deve sumir do aparelho e voltar ao entrar de novo.

## Componentes e telas

A definir no design.

## Dentro do escopo

- Ver a conta e a assinatura, sair e excluir a conta.

## Fora do escopo

- Trocar o e-mail ou juntar contas Apple e Google.

## Definições pendentes

- Em quanto tempo os dados apagados somem também dos backups do servidor. · Matheus, com quem construir o servidor.

## Fluxos conectados

- [Assinar o Traça](assinar-o-traca.md) · a assinatura mostrada aqui leva ao paywall quando está expirada.
- [Começar a usar o Traça](comecar-a-usar-o-traca.md) · sair ou excluir volta para **Boas-vindas**, o começo daquele fluxo.

## Fluxos filhos

Nenhum.

## Faz parte de

- [Fluxos](README.md)
