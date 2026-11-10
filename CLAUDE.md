# Atlas · Traça

Este repositório é o Atlas do Traça: a especificação viva do app, versionada no Git. Segue a Metodologia Atlas.

## Regras que valem aqui

- Comece pelo `README.md`, depois `constituicao.md`, `visao-geral.md` (quando existir), `objetos/` e só então a página do fluxo. A lógica mora nos objetos; a jornada e as telas, nos fluxos.
- Página nova segue a anatomia da Metodologia Atlas: cabeçalho YAML (tipo, título, status, alertas, versão), seções em ordem fixa, seção vazia apagada em vez de deixada em branco.
- O texto descreve o que o produto é agora. Histórico, correção e "antes dizia" vão na mensagem do commit, escrita para gente ler: título curto, o que mudou, por que, quem decidiu e quando.
- Um commit por decisão ou rodada, direto na `main`. Rodada aprovada pelo Matheus sobe a versão no README (`vX.Y` e a data).
- Pergunta sem resposta vira Definição pendente com dono. Nunca invente regra, número, prazo ou decisão.
- Divergência entre especificação e protótipo fica registrada em `## Divergências`, com os dois lados. Nunca se resolve em silêncio.
- O Traça é um produto independente. Não traga para cá conteúdo, clientes, marca ou dados de outras empresas.
- Português do Brasil, sem travessão retórico. Nome de tela vem do protótipo e fica como está.
- Nunca guarde senha, token, chave de API ou dado pessoal neste repositório.
