---
tipo: fluxo
titulo: Gerenciar a conta
ator: leitor com conta
job: ver a assinatura, sair da conta ou apagar tudo quando quiser
status: Desenhado
alertas: []
versao: 2.1
aprovado: 2026-11-10
prototipo: https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL
---

# Gerenciar a conta

## Protótipo

Desenhado no [canvas do Traça](https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL), página "App V1", linha CON. Aprovado pelo Matheus em 10/11/2026.

- **CON-001 · Conta** · conta, assinatura, notificações, sair e excluir.
- **CON-002 · Excluir conta** · painel de confirmação.
- **CON-003 · Excluindo a conta** · o painel durante a exclusão.
- **CON-004 · Conta · em teste** · a assinatura durante o teste grátis.
- **CON-005 · Conta · assinatura expirada** · com o botão para assinar.
- **CON-006 · Excluir conta · sem internet** · o erro, sem apagar nada.

## Job to be Done

"Quero saber o que estou pagando, trocar de aparelho sem perder nada e, se eu quiser, sair de vez."

## Objetos

- [Conta](../objetos/conta.md) · cobre sair e excluir.
- [Assinatura](../objetos/assinatura.md) · só leitura: o estado e o fim do período.

## Fluxo

1. O leitor abre **Conta** pela biblioteca.
2. **Conta** mostra o e-mail, o provedor (Apple ou Google), o estado da assinatura, a data da próxima cobrança ou do fim do acesso e as notificações.
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

### Estados da assinatura na Conta

- Ativa: o selo "Ativa" e a próxima cobrança.
- Em teste: o selo "Teste grátis" e o texto "Seu teste termina em <data>. Depois, <preço do plano>."
- Expirada: o selo "Expirada", o texto "Sua assinatura terminou em <data>." e o botão "Assinar", que abre **Assinar**.
- Sem internet ao excluir: "Você está sem internet. Conecte o iPhone para excluir a conta." Nada é apagado.

### Notificações

- **Avisos no iPhone** liga e desliga as notificações do Traça, como o lembrete do fim do teste. Se o leitor negou a permissão no iOS, ligar abre os Ajustes do iPhone, porque só lá dá para mudar.
- **Novidades por e-mail** começa desligado e só com ele ligado o Traça manda e-mail que não seja sobre a conta ou a assinatura.

Decidido pelo Matheus em 10/11/2026.

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

As telas usam os componentes do design system do canvas (página "Marca e design system", quadros DS-01 a DS-03), com o Liquid Glass descrito no [guia de marca](../marca.md#linguagem-visual-do-app). Os nomes de voz (Clara, Davi, Helena, Rafael), os livros e os tempos que aparecem nas telas são valores de exemplo.

- **CON-001** · Conta
- **CON-002** · Excluir conta
- **CON-003** · Excluindo a conta
- **CON-004** · Conta · em teste
- **CON-005** · Conta · assinatura expirada
- **CON-006** · Excluir conta · sem internet

## Dentro do escopo

- Ver a conta e a assinatura, ajustar as notificações, sair e excluir a conta.

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
