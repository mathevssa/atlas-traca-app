# Atlas · Traça

A especificação do Traça, um app de iOS para ler e ouvir os livros do próprio usuário. Primeiro os objetos, depois os fluxos. Quem aprova é o Matheus. O Atlas segue a Metodologia Atlas: os objetos e suas regras vêm antes das jornadas, e o texto descreve o produto como ele é agora, enquanto o histórico fica nos commits.

| | |
|---|---|
| **Fontes** | Decisões do Matheus, registradas neste repositório. A hierarquia está na [Constituição](constituicao.md). |
| **Design** | [Canvas do Traça](https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL): marca e design system na primeira página, as 55 telas da V1 na página "App V1". Aprovado em 10/11/2026. |
| **Versão atual** | `v1.0` · 10/11/2026 · V1 completa e aprovada: Constituição, marca, objetos, fluxos e design |

## Base

- [Constituição](constituicao.md) · o que o produto é, para quem, os princípios e a hierarquia das fontes.
- Visão geral · escrita por último, quando houver três ou mais fluxos.
- [Objetos](objetos/README.md) · as coisas do app e suas regras: Livro, Narração, Assinatura e Conta.
- [Fluxos](fluxos/README.md) · o caminho do leitor, do primeiro livro à conta.

## Medida e marca

- [Métricas e eventos da jornada](metricas.md) · o que medimos e para quê.
- [Guia de marca](marca.md) · nome, cores, tipografia e ícone.

## Pendências da entrega

O que fica para resolver durante o desenvolvimento e antes de publicar na App Store. Quem desenvolve é o Claude, e cada item volta para o Matheus quando precisar de decisão.

| Pendência | Quando | Dono |
|---|---|---|
| Definir o painel administrativo: quem acessa, o que mostra (por exemplo, as horas geradas de [Métricas](metricas.md)) e se ele também gerencia as assinaturas. | Fase de conta e assinatura | Matheus |
| Teste de escuta da voz: Inworld TTS-2 Flash contra o TTS-2, com trechos reais em sequência. Define o modelo padrão e a ordem das vozes em [Escolher a voz](fluxos/comecar-a-usar-o-traca.md#definições-pendentes). | Antes de fechar o servidor de voz | Claude prepara, Matheus decide |
| Trocar os nomes de voz de exemplo (Clara, Davi, Helena, Rafael) pelas vozes reais em português do Brasil da Inworld. | Depois do teste de escuta | Claude |
| Trocar os logos de referência pelos componentes oficiais: o botão nativo de Entrar com a Apple e o asset oficial do Google. | No desenvolvimento do login | Claude |
| Gerar a narração do livro de amostra, *O Alienista*, em todas as vozes. | Depois do teste de escuta | Claude |
| Conferir na App Store se a faixa de R$ 429,90 existe para o Plano anual; se não, usar R$ 399,90. | Ao cadastrar os produtos na App Store | Claude |
| Abrir a conta de desenvolvedor da Apple como pessoa física, em nome do Matheus, que aparece como vendedor na App Store. Decidido pelo Matheus em 11/11/2026. | Antes da fase de conta e assinatura: o login com a Apple, as compras de teste e o TestFlight dependem dela | Matheus |
| Conversar com um contador sobre abrir um CNPJ (ME) e migrar a conta da Apple para a empresa antes de a receita crescer. | Antes de a receita crescer | Matheus |
| Consulta jurídica sobre direito autoral (converter o livro do usuário em áudio e guardar o arquivo no servidor do Traça) e LGPD (texto enviado para a Inworld). | Antes da publicação | Matheus |
| Política de privacidade e Termos de uso, com o que a consulta jurídica definir. | Antes da publicação | Claude escreve, Matheus aprova |
| Levar os fluxos de Desenhado para Pronto p/ dev, conferindo cada tela contra as regras do fluxo. | Antes de programar cada fluxo | Claude |

