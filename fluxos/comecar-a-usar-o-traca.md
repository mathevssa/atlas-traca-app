---
tipo: fluxo
titulo: Começar a usar o Traça
ator: leitor que acabou de instalar o app
job: ouvir o próprio livro em poucos segundos e decidir se vale assinar
status: Desenhado
alertas: []
versao: 2.1
aprovado: 2026-11-10
prototipo: https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL
---

# Começar a usar o Traça

## Protótipo

Desenhado no [canvas do Traça](https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL), página "App V1", linha CMC. Aprovado pelo Matheus em 10/11/2026.

- **CMC-001 · Boas-vindas** · três caminhos: escolher um livro do iPhone, ouvir o livro de amostra e "Já tenho conta".
- **CMC-002 · Importando o primeiro livro** · o botão vira a barra de progresso da importação.
- **CMC-003 · Erro de importação (DRM)** · a mensagem de proteção contra cópia acima do botão.
- **CMC-004 · Escolher a voz** · lista de vozes com amostra, a primeira já marcada.
- **CMC-005 · Ouvir os 5 minutos** · player com o contador de tempo grátis.
- **CMC-006 · Preparando a voz** · player enquanto o primeiro trecho é gerado.
- **CMC-007 · Fim dos 5 minutos · Entrar** · painel de login com a Apple ou o Google por cima do livro pausado.
- **CMC-008 · Começar o teste** · paywall com a linha do tempo do teste e o plano anual marcado.
- **CMC-009 · Livro de amostra** · player da amostra, com o convite para ouvir um livro do leitor.

## Job to be Done

"Quero ver se isso funciona com o meu livro antes de dar o cartão." O leitor instalou o app por curiosidade e quer ouvir um livro que já tem, com uma voz boa, sem cadastro e sem esperar.

## Objetos

- [Livro](../objetos/livro.md) · cobre `— → Importando → Disponível` do primeiro livro, antes do login.
- [Narração](../objetos/narracao.md) · cobre a geração dos 5 minutos grátis.
- [Conta](../objetos/conta.md) · cobre `— → Ativa`.
- [Assinatura](../objetos/assinatura.md) · cobre `— → Em teste`.

## Fluxo

1. O leitor abre o app pela primeira vez e vê **Boas-vindas**, com três caminhos: escolher um livro dele, ouvir o livro de amostra ou "Já tenho conta".
   - "Já tenho conta": abre o login com a Apple ou o Google e, depois de entrar, leva à **Biblioteca** da conta. O resto deste fluxo não se aplica.
2. Escolhendo um livro dele, o app abre o seletor de arquivos do iOS. O leitor também pode chegar aqui pelo "Compartilhar" de outro app, e aí este passo é pulado.
3. O livro é importado.
   - Deu certo: segue para **Escolher a voz**.
   - Deu errado (DRM, arquivo corrompido, formato não aceito): o leitor vê o motivo e volta para **Boas-vindas** para escolher outro arquivo.
4. Em **Escolher a voz**, o leitor ouve a amostra de cada voz e escolhe uma. Ao confirmar, o player abre e a narração começa sozinha, do início do livro.
5. O leitor ouve com o texto acompanhando. Um contador mostra quanto resta dos 5 minutos grátis.
6. Os 5 minutos acabam. A voz para no fim da frase e aparece **Fim dos 5 minutos · Entrar**, por cima do livro pausado.
7. O leitor entra com a Apple ou o Google nesse mesmo painel.
   - Desistiu do login: volta ao player, que fica parado no ponto onde a voz parou.
8. **Começar o teste** mostra o plano anual pré-selecionado, o mensal e a linha do tempo do teste (hoje, lembrete no dia 5, cobrança no dia 7).
9. O leitor confirma pela App Store.
   - Confirmou: a narração continua do ponto onde parou.
   - Desistiu: volta ao player parado. O livro e a conta continuam lá.

## Regras

### Antes do login

- O app não pede login, nome nem e-mail para importar o primeiro livro e ouvir os 5 minutos.
- Antes do login, só um livro pode ser importado. Tentar importar outro leva direto a **Fim dos 5 minutos · Entrar**.
- Os 5 minutos contam o tempo em que a voz tocou, e não o áudio gerado. Antes do login, só o primeiro trecho do livro é gerado. Decidido pelo Matheus em 10/11/2026.
- Os 5 minutos grátis valem uma vez por aparelho. Reinstalar o app não renova o tempo.

### Voz e livro de amostra

- O leitor escolhe a voz antes do primeiro play. A primeira voz da lista vem pré-selecionada, para quem só quer confirmar. Decidido pelo Matheus em 10/11/2026.
- O livro de amostra é *O Alienista*, de Machado de Assis, em domínio público, com a narração já gerada pelo Traça em todas as vozes. Ouvir a amostra não gasta os 5 minutos grátis e não tem limite de tempo. Decidido pelo Matheus em 10/11/2026.
- O livro de amostra não conta como o livro importado antes do login: depois de ouvir a amostra, o leitor ainda pode importar um livro dele.

### Login e teste

- "Já tenho conta" abre o painel **Entrar · Já tenho conta** por cima de **Boas-vindas**, com o título "Entrar na sua conta", o texto "Use a mesma conta Apple ou Google que você usou antes." e "Agora não".
- Antes do login, a **Biblioteca** mostra só o livro importado e o convite "Continue ouvindo <título>", com o texto "Entre na sua conta para continuar de onde parou." e o botão "Continuar", que abre **Fim dos 5 minutos · Entrar**.

- Para quem ainda não tem conta, o login aparece só quando o leitor decide continuar depois dos 5 minutos.
- Quem já tem conta (por exemplo, num iPhone novo) entra pelo botão "Já tenho conta" em **Boas-vindas**. O que pode fazer depois de entrar depende do estado da assinatura, como em qualquer outro aparelho. Decidido pelo Matheus em 10/11/2026.
- Antes do login, voltar do player leva à **Biblioteca**, que mostra o livro importado com um convite para continuar ouvindo. Decidido pelo Matheus em 10/11/2026.
- Ao fazer login, o livro, a posição e a narração já gerada passam para a conta sem o leitor fazer nada.
- O pedido de permissão de notificação vem junto com o lembrete do dia 5 em **Começar o teste**, com o texto dizendo para que serve.
- **Começar o teste** sempre mostra "Cancele quando quiser nos Ajustes do iPhone" e o link "Restaurar Compras".
- A linha do tempo do teste diz, nesta ordem: "Hoje: acesso completo, sem cobrança", "Dia 5: a gente te lembra que o teste está acabando" e "Dia 7: começa a cobrança. Cancele antes, se quiser".

## Estados de UI

### Boas-vindas

- **Ideal:** marca, uma frase do que o app faz e o botão para escolher um livro.
- **Vazio:** não se aplica.
- **Erro:** a mensagem do motivo da importação que falhou, acima do botão.
- **Parcial:** não se aplica.
- **Carregando:** enquanto o livro importa, o botão vira um indicador de progresso.

### Ouvir os 5 minutos

- **Ideal:** player com o texto acompanhando e o contador do tempo grátis.
- **Vazio:** não se aplica.
- **Erro:** a geração falhou: as regras da [Narração](../objetos/narracao.md#ciclo-de-vida). Sem internet: o aviso de que a voz precisa de conexão.
- **Parcial:** não se aplica.
- **Carregando:** "Preparando a voz" enquanto o primeiro trecho é gerado.

### Fim dos 5 minutos · Entrar e Começar o teste

- **Erro:** login cancelado ou recusado volta ao player sem mensagem de erro. Compra recusada pela App Store mostra o motivo que a App Store devolver.

## Critérios de aceite

- **Quando** o leitor importa o primeiro livro, a voz deve começar sem nenhum toque a mais.
- **Quando** os 5 minutos acabam, a voz deve parar no fim de uma frase, nunca no meio de uma palavra.
- **Se** o leitor reinstala o app, **então** os 5 minutos grátis não devem ser renovados.
- **Quando** o leitor faz login, o livro importado antes deve continuar na biblioteca, na mesma posição.
- **Se** o leitor desiste do login ou do teste, **então** o app deve voltar ao player parado, sem perder o livro.

## Componentes e telas

As telas usam os componentes do design system do canvas (página "Marca e design system", quadros DS-01 a DS-03), com o Liquid Glass descrito no [guia de marca](../marca.md#linguagem-visual-do-app). Os nomes de voz (Clara, Davi, Helena, Rafael), os livros e os tempos que aparecem nas telas são valores de exemplo.

- **CMC-001** · Boas-vindas
- **CMC-002** · Importando o primeiro livro
- **CMC-003** · Erro de importação (DRM)
- **CMC-004** · Escolher a voz
- **CMC-005** · Ouvir os 5 minutos
- **CMC-006** · Preparando a voz
- **CMC-007** · Fim dos 5 minutos · Entrar
- **CMC-008** · Começar o teste
- **CMC-009** · Livro de amostra

## Dentro do escopo

- Primeira abertura, importação do primeiro livro, 5 minutos grátis, login e início do teste.

## Fora do escopo

- Tutorial em várias telas antes de importar. O valor aparece ouvindo, não lendo explicação.

## Definições pendentes

- Em que ordem as vozes aparecem em **Escolher a voz**. · Matheus, depois do teste de escuta.

## Fluxos conectados

- [Importar e excluir livros](importar-e-excluir-livros.md) · as regras de importação e de erro valem também para o primeiro livro.
- [Ouvir um livro](ouvir-um-livro.md) · o player dos 5 minutos é o mesmo player do dia a dia.
- [Assinar o Traça](assinar-o-traca.md) · **Começar o teste** é o mesmo paywall que aparece para quem tem a assinatura expirada.

## Fluxos filhos

Nenhum.

## Faz parte de

- [Fluxos](README.md)
