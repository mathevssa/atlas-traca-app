---
tipo: objeto
titulo: Assinatura
definicao: O direito do leitor de usar o Traça, comprado pela App Store, com teste grátis de 7 dias e cobrança mensal ou anual depois.
status: Clarificação
alertas: []
versao: 1.4
aprovado:
---

# Assinatura

## Nome canônico

**Assinatura.** Não usar: *Traça Pro*, *premium*, *plano pago*. Os dois produtos à venda são o **Plano mensal** e o **Plano anual**.

## Atributos

| Atributo | Obrigatório | Regra |
|---|---|---|
| Plano | Sim | Plano mensal ou Plano anual. O leitor escolhe ao começar o teste grátis. |
| Preço | Sim | Um plano só na V1. Plano mensal: R$ 44,90. Plano anual: 20% menos que doze meses do mensal, cerca de R$ 429,90, a confirmar nas faixas da App Store brasileira. É o preço inicial, para testar, e pode mudar com os dados de conversão. Decidido pelo Matheus em 10/11/2026. |
| Estado | Sim | Ver Ciclo de vida. |
| Fim do período atual | Sim | Data em que o teste ou o período pago termina. Vem da App Store. |
| Renovação automática | Sim | Ligada ou desligada. Quem muda é o leitor, nos Ajustes do iOS. |

## Ciclo de vida

Estados: `Em teste` · `Ativa` · `Em carência` · `Expirada`

Antes de começar o teste, o leitor não tem assinatura. Nessa situação ele pode importar livros e gerar até 5 minutos de narração no total, como dizem as permissões do [Livro](livro.md#permissões) e da [Narração](narracao.md#permissões).

| De | Evento | Para | Quem | Efeitos |
|---|---|---|---|---|
| — | Começar o teste grátis, com o cartão cadastrado na App Store | `Em teste` | Leitor | Libera tudo por 7 dias, com um teto de 3 horas de narração gerada no teste inteiro. Decidido pelo Matheus em 10/11/2026. |
| `Em teste` | Fim dos 7 dias com a renovação ligada | `Ativa` | App Store | A App Store cobra o primeiro período do plano escolhido. |
| `Em teste` | Fim dos 7 dias com a renovação desligada | `Expirada` | App Store | Bloqueia ler, ouvir e importar. A biblioteca continua visível e permite excluir livros. |
| `Ativa` | Fim do período com a renovação ligada | `Ativa` | App Store | Cobra o período seguinte. Nada muda para o leitor. |
| `Ativa` | Fim do período com a renovação desligada | `Expirada` | App Store | O mesmo efeito da expiração do teste. |
| `Ativa` | Cobrança recusada no fim do período | `Em carência` | App Store | O leitor continua ouvindo o que já foi gerado e mantém a biblioteca, mas não gera narração nova. O app avisa que a cobrança não passou. Decidido pelo Matheus em 10/11/2026. |
| `Em carência` | A App Store consegue cobrar | `Ativa` | App Store | Tudo volta a ser liberado. |
| `Em carência` | Fim da carência sem cobrança | `Expirada` | App Store | O mesmo efeito da expiração do teste. A carência é a da App Store, de 16 dias. |
| `Expirada` | Assinar de novo | `Ativa` | Leitor | Libera tudo de novo. Livros, posição, marcações e narrações já geradas continuam onde estavam. Não há novo teste grátis: a App Store dá o teste uma vez por conta Apple. |

### O que NÃO tem, de propósito

- Não existe plano grátis permanente. Depois do teste, ou o leitor assina ou o Traça fica só com a biblioteca à vista. Decidido pelo Matheus em 10/11/2026.
- Não existe limite de livros nem de horas de narração para quem assina. Decidido pelo Matheus em 10/11/2026.
- O Traça não cancela assinatura dentro do app. O cancelamento é nos Ajustes do iOS, como em todo app da App Store.
- Não existe pagamento fora da App Store.

## Permissões

O que cada estado libera para o leitor está na tabela de permissões do [Livro](livro.md#permissões) e da [Narração](narracao.md#permissões).

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
