---
tipo: objeto
titulo: Conta
definicao: A identidade do leitor no Traça, criada no primeiro login com a Apple ou o Google. Guarda os livros, as posições, as marcações e a assinatura.
status: Clarificação
alertas: []
versao: 1.0
aprovado:
---

# Conta

## Nome canônico

**Conta.** Não usar: *perfil*, *usuário*, *cadastro*.

## Atributos

| Atributo | Obrigatório | Regra |
|---|---|---|
| Provedor | Sim | Apple ou Google, o que o leitor usou para entrar. Não existe senha do Traça. |
| Identificador do provedor | Sim | O identificador que a Apple ou o Google devolve. É o que reconhece o leitor no próximo login. |
| E-mail | Sim | O e-mail que o provedor entrega. Com a Apple, pode ser o e-mail oculto que ela gera, e o Traça aceita esse e-mail como qualquer outro. |
| Nome | Não | O nome que o provedor entrega, quando entrega. |
| Aceita receber e-mails | Sim | Começa desligado. Só com ele ligado o Traça manda e-mail que não seja sobre a conta ou a assinatura. Onde o leitor liga essa opção: A definir. |
| Criada em | Sim | Data e hora do primeiro login. |

## Ciclo de vida

Estados: `Ativa`

| De | Evento | Para | Quem | Efeitos |
|---|---|---|---|---|
| — | Primeiro login, ao começar o teste grátis | `Ativa` | Leitor | O livro importado antes do login, a posição dele e a narração já gerada passam para a conta. O arquivo do livro sobe para o servidor. |
| `Ativa` | Entrar com a mesma conta em outro iPhone | `Ativa` | Leitor | Os livros, as posições e as marcações aparecem no aparelho novo. A narração é gerada de novo conforme o leitor ouve, porque o áudio fica só no aparelho onde foi gerado. |
| `Ativa` | Sair da conta | `Ativa` | Leitor | O aparelho volta ao estado de antes do login: a biblioteca some dele, e tudo continua guardado na conta. |
| `Ativa` | Excluir a conta, depois de confirmar | — | Leitor | Apaga os livros, as posições, as marcações e os dados da conta no servidor, e o áudio do aparelho. Antes de confirmar, o app avisa que excluir a conta não cancela a assinatura da App Store e mostra como cancelar. |

### O que NÃO tem, de propósito

- Não existe senha do Traça. O login é sempre pela Apple ou pelo Google. Decidido pelo Matheus em 10/11/2026.
- Não existe login antes do teste grátis. Importar o primeiro livro e ouvir os 5 minutos grátis funcionam sem conta. Decidido pelo Matheus em 10/11/2026.
- Não existe junção de uma conta Apple com uma conta Google. Quem entra com provedores diferentes tem duas contas separadas.

## Relacionamentos

| Relação | Cardinalidade | Regra |
|---|---|---|
| Conta **tem** [Livros](livro.md) | 1:N | Vínculo vivo. Excluir a conta apaga os livros. |
| Conta **tem** uma [Assinatura](assinatura.md) | 1:1 | A assinatura fica ligada à conta que estava logada na compra. O que acontece quando outra Conta do Traça entra no mesmo iPhone com a mesma conta Apple que pagou: A definir. |

## Usado nos fluxos

- [Começar a usar o Traça](../fluxos/comecar-a-usar-o-traca.md) · cobre `— → Ativa`.
- [Gerenciar a conta](../fluxos/gerenciar-a-conta.md) · cobre sair e excluir.

## Faz parte de

- [Objetos](README.md)
