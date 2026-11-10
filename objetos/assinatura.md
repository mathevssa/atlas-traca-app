---
tipo: objeto
titulo: Assinatura
definicao: O direito do leitor de usar o Traça, comprado pela App Store, com teste grátis de 7 dias e cobrança mensal ou anual depois.
status: Clarificação
alertas: []
versao: 1.0
aprovado:
---

# Assinatura

## Nome canônico

**Assinatura.** Não usar: *Traça Pro*, *premium*, *plano pago*. Os dois produtos à venda são o **Plano mensal** e o **Plano anual**.

## Atributos

| Atributo | Obrigatório | Regra |
|---|---|---|
| Plano | Sim | Plano mensal ou Plano anual. O leitor escolhe ao começar o teste grátis. |
| Preço | Sim | Definido na App Store. O Plano anual custa 20% menos que doze meses do Plano mensal. Valores: A definir. |
| Estado | Sim | Ver Ciclo de vida. |
| Fim do período atual | Sim | Data em que o teste ou o período pago termina. Vem da App Store. |
| Renovação automática | Sim | Ligada ou desligada. Quem muda é o leitor, nos Ajustes do iOS. |

## Ciclo de vida

Estados: `Em teste` · `Ativa` · `Expirada`

| De | Evento | Para | Quem | Efeitos |
|---|---|---|---|---|
| — | Começar o teste grátis, com o cartão cadastrado na App Store | `Em teste` | Leitor | Libera tudo por 7 dias. |
| `Em teste` | Fim dos 7 dias com a renovação ligada | `Ativa` | App Store | A App Store cobra o primeiro período do plano escolhido. |
| `Em teste` | Fim dos 7 dias com a renovação desligada | `Expirada` | App Store | Bloqueia ler, ouvir e importar. A biblioteca continua visível e permite excluir livros. |
| `Ativa` | Fim do período com a renovação ligada | `Ativa` | App Store | Cobra o período seguinte. Nada muda para o leitor. |
| `Ativa` | Fim do período com a renovação desligada | `Expirada` | App Store | O mesmo efeito da expiração do teste. |
| `Ativa` | Cobrança recusada no fim do período | A definir | App Store | Se o leitor mantém acesso enquanto a App Store tenta cobrar de novo (período de carência): A definir. |
| `Expirada` | Assinar de novo | `Ativa` | Leitor | Libera tudo de novo. Livros, posição, marcações e narrações já geradas continuam onde estavam. Não há novo teste grátis: a App Store dá o teste uma vez por conta Apple. |

### O que NÃO tem, de propósito

- Não existe plano grátis permanente. Depois do teste, ou o leitor assina ou o Traça fica só com a biblioteca à vista. Decidido pelo Matheus em 10/11/2026.
- Não existe limite de livros nem de horas de narração para quem assina. Decidido pelo Matheus em 10/11/2026.
- O Traça não cancela assinatura dentro do app. O cancelamento é nos Ajustes do iOS, como em todo app da App Store.
- Não existe pagamento fora da App Store.

## Permissões

O que cada estado libera para o leitor está na tabela de permissões do [Livro](livro.md#permissões) e da [Narração](narracao.md#permissões). Se o leitor consegue entrar no app sem começar o teste grátis: A definir.

## Relacionamentos

| Relação | Cardinalidade | Regra |
|---|---|---|
| Assinatura **pertence à** conta Apple do leitor | 1:1 | Vale em qualquer iPhone com a mesma conta Apple, depois de restaurar a compra. |
| Assinatura **libera** os [Livros](livro.md) | 1:N | A assinatura não guarda livros. Quando expira, os livros ficam, e só o uso é bloqueado. |

## Usado nos fluxos

- Começar a usar o Traça (a escrever) · cobre `— → Em teste`.
- Assinar o Traça (a escrever) · cobre `Expirada → Ativa`, a escolha do plano e a restauração da compra.

## Faz parte de

- [Objetos](README.md)
