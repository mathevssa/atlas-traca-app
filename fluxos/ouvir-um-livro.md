---
tipo: fluxo
titulo: Ouvir um livro
ator: leitor com o teste ou a assinatura ativos
job: ouvir o livro com uma voz natural, acompanhando o texto, e controlar a narração sem atrito
status: Desenhado
alertas: []
versao: 2.2
aprovado: 2026-11-10
prototipo: https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL
---

# Ouvir um livro

## Protótipo

Desenhado no [canvas do Traça](https://claude.ai/artifact/Wf6LhNjyW8UGYz895H35JL), página "App V1", linha OUV. Aprovado pelo Matheus em 10/11/2026.

- **OUV-001 · Player** · texto acompanhando a voz e a barra de controles em vidro.
- **OUV-002 · Player · modo escuro** · fica para depois do MVP, que é sempre claro. Está no canvas só como referência.
- **OUV-003 · Player · rolagem manual** · a pílula "Voltar para onde estou".
- **OUV-004 · Velocidade** · painel de velocidade de 0,75x a 2x.
- **OUV-005 · Vozes** · painel de vozes com amostra.
- **OUV-006 · Aviso de troca de voz** · "A nova voz começa no próximo capítulo.".
- **OUV-007 · Capítulos** · painel Capítulos e Marcações, na aba Capítulos.
- **OUV-008 · Marcações** · o mesmo painel, na aba Marcações.
- **OUV-009 · Marcações · vazio** · a aba Marcações sem nenhuma marcação.
- **OUV-010 · Timer de sono** · opções do timer.
- **OUV-011 · Erro na voz** · aviso de falha na geração com "Tentar de novo".
- **OUV-012 · Sem internet** · aviso de sem internet.
- **OUV-013 · Player · timer ligado** · o botão Timer mostrando o tempo que falta.
- **OUV-014 · Marcação salva** · o aviso depois de marcar.
- **OUV-015 · Player · preparando a voz** · ao tocar numa frase ainda não gerada.
- **OUV-016 · Fim do livro** · o aviso de que o livro acabou.
- **OUV-017 · Capítulos · livro sem capítulos** · a lista com um capítulo só.

## Job to be Done

"Quero ouvir meu livro como um audiolivro de verdade, no ônibus, na academia ou antes de dormir, e saber onde estou no texto quando olhar a tela."

## Objetos

- [Livro](../objetos/livro.md) · cobre a posição atual, os capítulos e as marcações.
- [Narração](../objetos/narracao.md) · cobre toda a geração e a reprodução.

## Fluxo

1. O leitor toca num livro da **Biblioteca** ou no **Mini player**.
2. O **Player** abre na posição atual e a voz começa.
   - O trecho ainda não foi gerado: "Preparando a voz" até o áudio chegar.
3. Enquanto ouve, o leitor pode:
   - pausar e continuar;
   - voltar ou avançar 15 segundos;
   - arrastar a barra de progresso do capítulo;
   - tocar numa frase do texto para a voz ir até ela;
   - mudar a velocidade, a voz ou ligar o timer de sono;
   - abrir **Capítulos** e ir para outro capítulo;
   - marcar o ponto atual e abrir **Marcações** para voltar a um ponto salvo.
4. O leitor fecha o **Player**. A narração continua tocando, com o **Mini player** na **Biblioteca** e os controles na tela bloqueada.
5. O livro termina, o timer de sono para a voz, ou o leitor pausa. A posição fica salva.

## Regras

### Texto acompanhando

- O texto rola sozinho para manter a frase falada visível, e a palavra falada fica destacada.
- Se o leitor rola o texto com o dedo, a rolagem automática para, e aparece um botão para voltar ao ponto da voz.
- Tocar numa frase leva a voz para o começo dela. Se o trecho daquela frase ainda não foi gerado, aparece "Preparando a voz".

### Controles

- Os saltos são de 15 segundos para trás e para frente.
- A velocidade vai de 0,75x a 2x, em passos de 0,25x, e vale para todos os livros.
- O timer de sono oferece 15, 30 e 45 minutos, 1 hora e "fim do capítulo".
- A narração continua com a tela bloqueada e com o app em segundo plano, com os controles do iOS na tela bloqueada e nos fones.

### Voz

- **Vozes** lista as vozes em português do Brasil, cada uma com uma amostra curta para ouvir antes de escolher.
- Trocar a voz no meio do livro vale a partir do próximo capítulo, e o app avisa isso na hora da troca: "A nova voz começa no próximo capítulo." As regras moram na [Narração](../objetos/narracao.md#atributos).
- A voz escolhida vale para os próximos livros também.
- Depois de uma troca no meio do capítulo, o botão de voz já mostra a voz escolhida, mesmo antes de ela começar a tocar. Decidido pelo Matheus em 10/11/2026.

### Timer e fim do livro

- Com o timer ligado, o botão Timer mostra o tempo que falta (por exemplo, "22 min").
- Quando o livro acaba, aparece **Fim do livro**, com o título "Você terminou <título>" e dois botões: "Voltar para a biblioteca" (principal) e "Ouvir de novo", que volta a posição para o começo. Na biblioteca, o livro passa a mostrar "Terminado".

### Marcações

- Marcar salva o ponto atual na hora, sem pedir confirmação, e mostra o aviso "Marcação salva".
- **Marcações** mostra, para cada ponto, o capítulo, a frase de onde começa e a data.
- Excluir uma marcação é deslizar a linha.

## Estados de UI

### Player

- **Ideal:** texto com a palavra falada destacada, barra de progresso do capítulo e controles.
- **Vazio:** não se aplica.
- **Erro:** a geração falhou depois das 3 tentativas: "Não deu para preparar a voz deste trecho agora.", com o botão "Tentar de novo". Sem internet e sem trecho pronto: "Você está sem internet. Conecte o iPhone para continuar ouvindo."
- **Parcial:** o trecho atual está pronto e o próximo ainda está sendo gerado: nada aparece, a não ser que a voz chegue ao fim do trecho antes; aí mostra "Preparando a voz".
- **Carregando:** "Preparando a voz" no lugar do botão de play.

### Marcações

- **Vazio:** explicação curta de como marcar.

## Critérios de aceite

- **Quando** o leitor dá play num livro, a voz deve começar da posição atual salva.
- **Quando** a voz passa de um trecho para o outro com internet, o áudio não deve parar.
- **Quando** o leitor toca numa frase, a voz deve ir para o começo daquela frase.
- **Se** o leitor troca de voz no meio de um capítulo, **então** o app deve avisar que a voz nova começa no próximo capítulo.
- **Quando** o leitor bloqueia a tela, a narração deve continuar e os controles devem aparecer na tela bloqueada.
- **Se** a assinatura expirou, **então** o play deve levar ao paywall de [Assinar o Traça](assinar-o-traca.md).

## Componentes e telas

As telas usam os componentes do design system do canvas (página "Marca e design system", quadros DS-01 a DS-03), com o Liquid Glass descrito no [guia de marca](../marca.md#linguagem-visual-do-app). Os nomes de voz (Clara, Davi, Helena, Rafael), os livros e os tempos que aparecem nas telas são valores de exemplo.

- **OUV-001** · Player
- **OUV-002** · Player · modo escuro
- **OUV-003** · Player · rolagem manual
- **OUV-004** · Velocidade
- **OUV-005** · Vozes
- **OUV-006** · Aviso de troca de voz
- **OUV-007** · Capítulos
- **OUV-008** · Marcações
- **OUV-009** · Marcações · vazio
- **OUV-010** · Timer de sono
- **OUV-011** · Erro na voz
- **OUV-012** · Sem internet

## Dentro do escopo

- Player com texto acompanhando, mini player, controles na tela bloqueada, velocidade, vozes, capítulos, marcações e timer de sono.

## Fora do escopo

- Leitura silenciosa, ajuste de tamanho, fonte e cor do texto. O texto só acompanha a voz. Decidido pelo Matheus em 10/11/2026.
- Destaques de texto e anotações.
- CarPlay e Apple Watch. Voltam depois da V1, se o uso no carro aparecer nas métricas.

## Rabbit holes

- Fazer o texto acompanhar a voz em PDF, onde o texto às vezes sai fora de ordem ao ser extraído. Destrava com um teste em PDFs reais antes do desenvolvimento.

## Fluxos conectados

- [Importar e excluir livros](importar-e-excluir-livros.md) · é da biblioteca que o leitor abre o livro para ouvir.
- [Assinar o Traça](assinar-o-traca.md) · com a assinatura expirada ou em carência, o player limita o que gera e toca.

## Fluxos filhos

Nenhum.

## Faz parte de

- [Fluxos](README.md)
