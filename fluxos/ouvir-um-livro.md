---
tipo: fluxo
titulo: Ouvir um livro
ator: leitor com o teste ou a assinatura ativos
job: ouvir o livro com uma voz natural, acompanhando o texto, e controlar a narração sem atrito
status: Clarificação
alertas: []
versao: 1.0
aprovado:
prototipo:
---

# Ouvir um livro

## Protótipo

Ainda não desenhado.

Telas que esta página descreve (nomes provisórios até o protótipo existir):

- **Player** · o texto acompanhando a voz, com os controles.
- **Mini player** · a barra do livro tocando, na **Biblioteca**.
- **Velocidade** · seletor de 0,75x a 2x.
- **Vozes** · lista das vozes em português do Brasil.
- **Capítulos** · lista para navegar.
- **Marcações** · lista dos pontos salvos.
- **Timer de sono** · opções para parar a narração sozinha.

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

### Marcações

- Marcar salva o ponto atual na hora, sem pedir confirmação, e mostra o aviso "Marcação salva".
- **Marcações** mostra, para cada ponto, o capítulo, a frase de onde começa e a data.
- Excluir uma marcação é deslizar a linha.

## Estados de UI

### Player

- **Ideal:** texto com a palavra falada destacada, barra de progresso do capítulo e controles.
- **Vazio:** não se aplica.
- **Erro:** a geração falhou depois das 3 tentativas: "A voz não conseguiu preparar este trecho agora.", com o botão "Tentar de novo". Sem internet e sem trecho pronto: "Sem internet. O que já foi preparado continua tocando. Para o resto, conecte-se."
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

A definir no design.

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
