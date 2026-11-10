---
tipo: fluxo
titulo: Começar a usar o Traça
ator: leitor que acabou de instalar o app
job: ouvir o próprio livro em poucos segundos e decidir se vale assinar
status: Clarificação
alertas: []
versao: 1.1
aprovado:
prototipo:
---

# Começar a usar o Traça

## Protótipo

Ainda não desenhado.

Telas que esta página descreve (nomes provisórios até o protótipo existir):

- **Boas-vindas** · primeira abertura do app.
- **Escolher o primeiro livro** · o seletor de arquivos do iOS, aberto pelo app.
- **Escolher a voz** · as vozes em português do Brasil, com amostra, antes do primeiro play.
- **Ouvir os 5 minutos** · o player, com o contador do tempo grátis.
- **Fim dos 5 minutos · Entrar** · o painel por cima do livro pausado, com o convite para continuar e o login com a Apple ou o Google. Decidido pelo Matheus em 10/11/2026.
- **Começar o teste** · o paywall com a linha do tempo do teste.

## Job to be Done

"Quero ver se isso funciona com o meu livro antes de dar o cartão." O leitor instalou o app por curiosidade e quer ouvir um livro que já tem, com uma voz boa, sem cadastro e sem esperar.

## Objetos

- [Livro](../objetos/livro.md) · cobre `— → Importando → Disponível` do primeiro livro, antes do login.
- [Narração](../objetos/narracao.md) · cobre a geração dos 5 minutos grátis.
- [Conta](../objetos/conta.md) · cobre `— → Ativa`.
- [Assinatura](../objetos/assinatura.md) · cobre `— → Em teste`.

## Fluxo

1. O leitor abre o app pela primeira vez e vê **Boas-vindas**, com dois caminhos: escolher um livro dele ou ouvir o livro de amostra.
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
- O livro de amostra é um texto de domínio público, com a narração já gerada pelo Traça em todas as vozes. Ouvir a amostra não gasta os 5 minutos grátis e não tem limite de tempo. Decidido pelo Matheus em 10/11/2026.
- O livro de amostra não conta como o livro importado antes do login: depois de ouvir a amostra, o leitor ainda pode importar um livro dele.

### Login e teste

- O login aparece só quando o leitor decide continuar depois dos 5 minutos.
- Antes do login, voltar do player leva à **Biblioteca**, que mostra o livro importado com um convite para continuar ouvindo. Decidido pelo Matheus em 10/11/2026.
- Ao fazer login, o livro, a posição e a narração já gerada passam para a conta sem o leitor fazer nada.
- O pedido de permissão de notificação vem junto com o lembrete do dia 5 em **Começar o teste**, com o texto dizendo para que serve.
- **Começar o teste** sempre mostra "Cancele quando quiser nos Ajustes do iPhone" e o link "Restaurar compras".
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

A definir no design.

## Dentro do escopo

- Primeira abertura, importação do primeiro livro, 5 minutos grátis, login e início do teste.

## Fora do escopo

- Tutorial em várias telas antes de importar. O valor aparece ouvindo, não lendo explicação.

## Definições pendentes

- Qual livro de domínio público é a amostra, e de que tamanho. · Matheus
- Em que ordem as vozes aparecem em **Escolher a voz**. · Matheus, depois do teste de escuta.

## Fluxos conectados

- [Importar e excluir livros](importar-e-excluir-livros.md) · as regras de importação e de erro valem também para o primeiro livro.
- [Ouvir um livro](ouvir-um-livro.md) · o player dos 5 minutos é o mesmo player do dia a dia.
- [Assinar o Traça](assinar-o-traca.md) · **Começar o teste** é o mesmo paywall que aparece para quem tem a assinatura expirada.

## Fluxos filhos

Nenhum.

## Faz parte de

- [Fluxos](README.md)
