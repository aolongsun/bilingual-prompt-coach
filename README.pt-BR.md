# Bilingual Prompt Coach

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español mexicano](README.es-MX.md) | [Português (Brasil)](README.pt-BR.md) | [Türkçe](README.tr.md)

Pratique um idioma enquanto realiza tarefas reais. Este Skill do Codex precisa ser ativado explicitamente: ele oferece comentários breves sobre sua escrita antes de atender ao pedido e acrescenta explicações no idioma de apoio apenas quando elas ajudam.

O padrão é usar chinês como idioma de apoio e praticar inglês americano claro de nível B2–C1. Você pode escolher os dois idiomas, a variante e o nível do idioma de prática, a profundidade dos comentários e a proporção entre os idiomas.

Os links acima mudam apenas o idioma da documentação. Eles não alteram a configuração da prática; informe suas preferências na conversa.

![Exemplo em inglês com as correções em negrito](docs/output-example.png)

*A imagem mostra um exemplo de resposta em inglês. Somente as alterações na correção mínima aparecem em negrito.*

![Fluxograma em inglês sobre quando oferecer comentários](docs/decision-map.jpg)

*Este fluxograma está em inglês e mostra quando os comentários sobre o idioma aparecem.*

## Visão geral

Faça seus pedidos habituais de estudo, pesquisa, programação ou trabalho cotidiano enquanto aprende com comentários curtos que podem ser aplicados em outras situações. A resposta ao pedido original vem em seguida.

- Textos em inglês ou em outro idioma de prática recebem uma correção mínima e uma versão natural quando isso é útil.
- Textos inteiramente no seu idioma principal recebem uma versão natural no idioma de prática.
- Textos que misturam idiomas são convertidos para o idioma de prática sem mudar o significado.
- Se o texto já estiver claro e natural, uma nota breve substitui reescritas desnecessárias.
- Trechos difíceis podem receber uma explicação curta no idioma de apoio logo abaixo. Respostas comuns não são traduzidas parágrafo por parágrafo.

## Instalação

Peça ao Codex para usar o instalador integrado:

```text
Use $skill-installer to install the skill from https://github.com/aolongsun/bilingual-prompt-coach.
```

Como alternativa, clone o repositório no seu diretório pessoal de skills:

```bash
git clone https://github.com/aolongsun/bilingual-prompt-coach ~/.agents/skills/bilingual-prompt-coach
```

Reinicie o Codex se o skill não aparecer imediatamente.

## Como usar

Invoque o skill explicitamente junto com um pedido concreto:

```text
$bilingual-prompt-coach I read a paper yesterday. Can you help me understand its main argument?
```

A prática continua ativa durante a tarefa atual sem precisar invocar o skill novamente. Cada nova tarefa começa com o modo de prática desativado. Qualquer uma destas expressões o desativa:

```text
off
OFF!
stop coaching
Desative a prática de idiomas.
```

Você também pode pedir para parar no seu próprio idioma. Uma instrução sem relação com a prática, como `turn the server off`, não desativa os comentários sobre o idioma.

## Escolha os idiomas e os comentários

O idioma principal ou de apoio e o idioma de prática são configurações separadas. Defina os dois com linguagem natural, inclusive ao ativar o skill:

```text
$bilingual-prompt-coach Meu idioma principal é japonês e quero praticar inglês.
Meu idioma principal é chinês e quero praticar japonês.
Use inglês britânico de nível B1.
Somente inglês.
Inclua mais chinês, por favor.
Sem notas sobre as correções.
Não destaque as alterações.
Corrija o texto completo.
```

Na tarefa atual, vale a última escolha explícita. Sem outra configuração, continuam valendo o apoio em chinês e a prática de inglês americano B2–C1. Trocar de README não configura nenhum dos dois idiomas.

Se você especificar o idioma do resultado, ele terá prioridade na resposta à tarefa. Por exemplo, “Responda a esta pergunta em chinês” gera uma resposta em chinês, mantendo o bloco de prática quando aplicável. As notas `Why` normalmente usam o idioma de prática, com ajuda no idioma principal apenas quando necessário.

## Exemplo

Entrada:

```text
$bilingual-prompt-coach I want practice English while I work. Can you helps me?
```

Exemplo de resposta, mantido em inglês para mostrar as correções:

> ### Language practice
>
> Minimal correction: I want **to** practice English while I work. Can you **help** me?
>
> Natural phrasing: I'd like to practice English as I work. Can you help me?
>
> Why: Use “want to” before a verb. After “can,” use the base form “help.”
>
> Yes. Send your next work-related request, and I'll give brief language feedback before answering it.

Somente as inserções e substituições em `Minimal correction` aparecem em negrito. `Natural phrasing` e a resposta à tarefa não destacam alterações. As exclusões são removidas do texto; por padrão, não há texto tachado, cores em HTML nem marcação diff. Você pode pedir correções sem destaque.

Quando todo o texto está no idioma principal, o bloco usa `Natural version` no lugar de `Minimal correction` e `Natural phrasing`.

## Limites de funcionamento

- Os comentários aparecem no máximo uma vez por turno, no início da resposta final. Não aparecem em atualizações de progresso nem no planejamento intermediário. Formatos obrigatórios, como somente JSON ou código, têm prioridade.
- Saudações, confirmações, escolha de opções, anexos sem texto substantivo e mensagens breves como “continue” ou “implemente o plano” não recebem o bloco de comentários.
- Citações, fontes coladas, código, comandos, logs, nomes de arquivos e dados ficam de fora, a menos que você peça para editá-los.
- Se revisão, reescrita ou tradução já for o resultado solicitado, não é acrescentado outro bloco de comentários, salvo se você pedir.
- Para textos com mais de 150 palavras, são selecionados até três trechos úteis em vez de repetir o texto completo duas vezes. Você pode pedir uma revisão completa para mudar esse comportamento.
- As reescritas preservam significado, tom, afirmações e grau de detalhe. Não acrescentam ideias nem tornam o pedido mais forte ou mais fraco.

Este skill contém apenas instruções: não tem scripts de execução, dependências de ferramentas externas nem memória oculta entre tarefas. O modo de prática depende da conversa atual. [SKILL.md](SKILL.md) contém o único conjunto de instruções, em inglês; os READMEs traduzidos explicam o mesmo skill, sem criar versões separadas. A [lista de verificação de comportamento](tests/behavior-cases.md) documenta os cenários de validação.

## Licença

[MIT](LICENSE)
