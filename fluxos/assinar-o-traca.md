---
tipo: fluxo
titulo: Assinar o Traça
ator: leitor com conta, com o teste acabando, a assinatura expirada ou em carência
job: continuar ouvindo sem perder nada, pagando de um jeito claro e sem susto
status: Desenhado
alertas: []
versao: 2.1
aprovado: 2026-11-10
prototipo: https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL
---

# Assinar o Traça

## Protótipo

Desenhado no [canvas do Traça](https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL), página "App V1", linha ASS. Aprovado pelo Matheus em 10/11/2026.

- **ASS-001 · Assinar** · paywall sem teste, para quem já usou o teste.
- **ASS-002 · Assinatura expirada** · aviso na biblioteca.
- **ASS-003 · Cobrança não passou** · aviso no player durante a carência.
- **ASS-004 · Assinar · carregando preços** · paywall com os planos em esqueleto.
- **ASS-005 · Assinar · sem internet** · paywall sem conexão.
- **ASS-006 · Assinatura ativa** · o aviso depois da compra.
- **ASS-007 · Restaurar · compra restaurada** · o aviso de sucesso.
- **ASS-008 · Restaurar · nada encontrado** · o alerta.
- **ASS-009 · Restaurar · de outra conta** · o alerta.
- **ASS-010 · Lembrete do dia 5** · a notificação na tela bloqueada.

## Job to be Done

"Quero continuar ouvindo. Me diz quanto custa, quando cobra e como cancelo, sem letra miúda."

## Objetos

- [Assinatura](../objetos/assinatura.md) · cobre `Expirada → Ativa`, a carência e a restauração da compra.

## Fluxo

1. O leitor chega em **Assinar** por um destes caminhos:
   - tocou em play, importar ou numa ação bloqueada com a assinatura expirada;
   - tocou em **Assinatura expirada** na biblioteca;
   - abriu a assinatura na tela da conta.
2. **Assinar** mostra o plano anual pré-selecionado, com o preço por ano e o equivalente por mês, e o plano mensal.
3. O leitor confirma pela App Store.
   - Confirmou: a assinatura fica `Ativa`, e o leitor volta para onde estava.
   - Desistiu: volta para onde estava, sem nada mudar.
4. Num iPhone novo, o leitor toca em "Restaurar Compras" e a assinatura volta a valer.
   - Se a compra encontrada pertence a outra conta do Traça, o app avisa isso e a assinatura não vale para a conta atual. Decidido pelo Matheus em 10/11/2026.
5. Se a cobrança não passa no fim do período, o leitor vê **Cobrança não passou**, com o título "Não conseguimos renovar sua assinatura" e o texto "Houve um problema com o pagamento. Para continuar ouvindo o livro, atualize a forma de pagamento.", com o link para atualizar o pagamento nos Ajustes do iPhone, e continua ouvindo o que já foi gerado durante a carência.

## Regras

- O preço anual cobrado aparece como principal, e o equivalente por mês aparece como informação secundária, como exige a App Store.
- **Assinar** sempre mostra "Cancele quando quiser nos Ajustes do iPhone", "Restaurar Compras", os Termos e a Privacidade.
- Quem já usou o teste grátis na conta Apple não vê oferta de teste. O botão diz "Assinar".
- Durante o teste, o app manda um lembrete no dia 5, se o leitor permitiu notificações: "Seu teste do Traça acaba em 2 dias. Para continuar ouvindo, não precisa fazer nada."
- Depois da compra, aparece o aviso "Pronto! Sua assinatura está ativa." onde o leitor estava.
- "Restaurar Compras" tem três respostas:
  - deu certo: o aviso "Sua assinatura foi restaurada.";
  - nada encontrado: o alerta "Nenhuma assinatura encontrada", com o texto "Não encontramos uma assinatura do Traça nesta conta Apple." e o botão "OK";
  - compra de outra conta do Traça: o alerta "Essa assinatura é de outra conta", com o texto "Ela foi comprada com outra conta do Traça neste iPhone. Entre com aquela conta para usar." e o botão "OK".
- Sem internet, **Assinar** mostra "Você está sem internet. Conecte o iPhone para assinar." e o botão fica desativado.
- Em carência, o player toca o que já foi gerado e mostra **Cobrança não passou** quando o leitor tenta gerar um trecho novo.

## Estados de UI

### Assinar

- **Ideal:** planos, benefícios, botão de assinar e as linhas fixas da regra acima.
- **Erro:** compra recusada pela App Store: o motivo que ela devolver. Sem internet: aviso de que assinar precisa de conexão.
- **Carregando:** enquanto a App Store carrega os preços, os cards dos planos aparecem em esqueleto, sem valor inventado.

## Critérios de aceite

- **Quando** a compra é confirmada, as ações bloqueadas devem ser liberadas na hora, sem reiniciar o app.
- **Quando** o leitor toca em "Restaurar Compras" com uma assinatura válida, ela deve voltar a valer na conta.
- **Se** a cobrança falha, **então** o leitor deve continuar ouvindo o que já foi gerado, sem gerar trechos novos, até o fim da carência.

## Componentes e telas

As telas usam os componentes do design system do canvas (página "Marca e design system", quadros DS-01 a DS-03), com o Liquid Glass descrito no [guia de marca](../marca.md#linguagem-visual-do-app). Os nomes de voz (Clara, Davi, Helena, Rafael), os livros e os tempos que aparecem nas telas são valores de exemplo.

- **ASS-001** · Assinar
- **ASS-002** · Assinatura expirada
- **ASS-003** · Cobrança não passou
- **ASS-004** · Assinar · carregando preços
- **ASS-005** · Assinar · sem internet
- **ASS-006** · Assinatura ativa
- **ASS-007** · Restaurar · compra restaurada
- **ASS-008** · Restaurar · nada encontrado
- **ASS-009** · Restaurar · de outra conta
- **ASS-010** · Lembrete do dia 5

## Dentro do escopo

- Paywall, compra, restauração, expiração e carência.

## Fora do escopo

- Pagamento fora da App Store, como Pix ou link externo. Pode voltar se a comissão da Apple pesar no resultado.
- Oferta para quem cancelou (win-back). Volta quando houver base de ex-assinantes.

## Fluxos conectados

- [Começar a usar o Traça](comecar-a-usar-o-traca.md) · o primeiro paywall, com o teste grátis, é a mesma tela **Assinar**.
- [Gerenciar a conta](gerenciar-a-conta.md) · a assinatura aparece na tela da conta, que leva a **Assinar** ou aos Ajustes do iPhone.

## Fluxos filhos

Nenhum.

## Faz parte de

- [Fluxos](README.md)
