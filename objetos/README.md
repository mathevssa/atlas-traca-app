# Objetos

Os substantivos do Traça: o que são, por quais estados passam e quem pode o quê. Os fluxos referenciam estes arquivos e não recopiam o conteúdo.

## Diagrama de dados

[modelo-de-dados.dbml](modelo-de-dados.dbml): o modelo conceitual, gerado a partir dos arquivos de objeto. Para visualizar, cole em [dbdiagram.io](https://dbdiagram.io/).

## Objetos

- [Livro](livro.md) · o ebook importado pelo leitor, com a posição de leitura e as marcações.
- [Narração](narracao.md) · o áudio da voz de IA de um capítulo, gerado sob demanda.
- [Assinatura](assinatura.md) · o direito de usar o Traça: teste de 7 dias, depois mensal ou anual.
- [Conta](conta.md) · a identidade do leitor, criada no login com a Apple ou o Google.

Capítulo e Marcação não têm página própria: o capítulo é um atributo do Livro e a unidade da Narração, e a marcação é um atributo do Livro sem lógica própria. Ganham página se aparecer regra que dois fluxos precisem consumir.
