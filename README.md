# Project Collector's Diary

Aplicação web em arquivo único para acompanhar **coleta, estoque e refino no Albion Online**.

O Collector's Diary foi feito para **jogadores iniciantes e experientes** que querem gastar menos tempo conferindo preços, fazendo contas manualmente e tentando descobrir se compensa mais refinar, vender os materiais ou comprar o que está faltando.

A ideia é simples: você informa e acompanha seu estoque, escolhe o que pretende produzir e deixa o aplicativo cruzar esses dados com **preços de mercado obtidos pela API do Albion Online Data Project**. Assim, o painel concentra as informações necessárias para ajudar na decisão sem precisar ficar alternando entre mercado, calculadora e anotações.

O Collector's Diary reúne cálculo de refino, consulta de mercado, controle de estoque e histórico de movimentações em uma interface que funciona tanto no computador quanto no celular. Ele não joga nem negocia por você: funciona como uma ferramenta de apoio para tornar o processo de coleta e refino mais rápido e organizado.

## Download

**Versão atual: v1.0.0**

[Baixar Collector's Diary v1.0.0](https://github.com/tutybas/Project-Collector-s-Diary/releases/download/v1.0.0/Collectors-Diary-v1.0.0.html)

Salve o arquivo HTML e abra-o no navegador. Consulte também a [Release v1.0.0](https://github.com/tutybas/Project-Collector-s-Diary/releases/tag/v1.0.0).

## O que você pode fazer

| Funcionalidade | Descrição |
| --- | --- |
| Cinco diários | Coleta e refino para Minerador, Lenhador, Curtidor, Tecelão e Pedreiro. |
| Mercado | Consulta preços pela Albion Online Data Project com servidor, cidade e referências escolhidos pelo jogador. |
| Completar com compras | Calcula materiais faltantes, compras necessárias, receita após taxa e lucro da operação. |
| Somente estoque | Limita a produção aos materiais disponíveis e compara refino com venda dos materiais. |
| Estoque compartilhado | Registra recursos e refinados dos cinco diários no navegador. |
| Aportes e saídas | Registra vários itens por movimentação e agrupa itens repetidos. |
| Refino confirmado | Atualiza o estoque e registra a operação no histórico. |
| Histórico reversível | Cancela movimentações compatíveis sem permitir estoque negativo. |
| Interface responsiva | Navegação lateral no desktop e menu compacto no celular. |

## Como usar

Abra o `index.html` em um navegador moderno. Não é necessário instalar dependências nem executar servidor local.

### 1. Escolha o diário

O seletor de diários troca o tipo de coleta/refino usado no painel:

| Diário | Recurso | Refinado |
| --- | --- | --- |
| Minerador | Minério | Barra |
| Lenhador | Madeira | Tábua |
| Curtidor | Pele | Couro |
| Tecelão | Fibra | Tecido |
| Pedreiro | Pedra | Bloco de pedra |

No celular, os diários ficam no menu hambúrguer. No computador, a navegação usa o layout lateral.

### 2. Configure o mercado

No primeiro uso, abra **Configurações**, escolha servidor, cidade, modo de produção e referências de compra e venda, informe as taxas e salve. Essas escolhas permitem usar o aplicativo em diferentes servidores, cidades e situações de mercado.

**Servidor e cidade** determinam de onde os preços serão consultados. Ambos começam em **---**, assim como os modos de produção, compra e venda; nenhuma dessas opções é escolhida automaticamente.

**Taxa de retorno** representa a porcentagem esperada de materiais devolvidos durante o refino. Começa em **0** e deve ser informada conforme a situação do jogador.

**Taxa do mercado** é descontada do valor final recebido na venda. Começa em **0**; informe a taxa correspondente à sua conta/personagem.

A **quantidade padrão** começa em **0**, mantendo o cálculo a partir do estoque. Escolha também as referências de compra e venda que serão usadas nos dados de mercado.

Os padrões neutros se aplicam a quem ainda não possui configurações salvas. Configurações existentes no `localStorage` são preservadas. O botão **Restaurar padrões** aplica os valores neutros quando acionado pelo jogador.

Sem servidor ou cidade, a consulta de mercado é bloqueada com uma orientação no painel. Os cálculos também aguardam a escolha dos modos de produção, compra e venda.

> O custo cobrado pela estação de refino não é incluído, porque esse valor varia de acordo com a estação utilizada pelo jogador.

### 3. Atualize o mercado

No **Painel de refino**, escolha o item desejado e use **Atualizar mercado**.

Os preços são consultados através da API pública do Albion Online Data Project. O aplicativo mostra quando a consulta foi concluída ou quando ocorreu uma falha.

### 4. Escolha como quer produzir

Existem dois modos principais.

#### Completar com compras

Use quando você pretende aproveitar seu estoque e **comprar o que estiver faltando**.

O painel informa:

- quantidade a produzir;
- materiais que precisam ser comprados;
- total necessário para essas compras;
- valor final recebido pela venda;
- lucro da operação.

**Lucro da operação = valor recebido - compras necessárias naquele momento.**

Materiais que já estão no estoque não são tratados como uma nova saída de caixa nesse modo.

#### Somente estoque

Use quando você **não quer comprar nada**.

A produção fica limitada pelo primeiro ingrediente necessário que acabar. O painel compara:

- quanto os refinados produzidos valeriam;
- quanto valeriam os materiais usados se fossem vendidos diretamente;
- diferença a favor ou contra o refino.

Esse modo não mostra custo de compra, porque nenhuma compra faz parte da operação.

### 5. Controle o estoque

A página **Estoque** guarda recursos brutos e refinados.

Os dados ficam salvos localmente no navegador usando `localStorage`.

Você pode filtrar a visualização entre recursos e refinados e também zerar o estoque quando quiser começar um controle novo.

> Limpar dados do navegador, usar outro navegador ou trocar de dispositivo não transfere automaticamente esse estoque.

### 6. Registre aportes e saídas

Em **Aportes e saídas**, use:

- **Novo aporte** para registrar itens que entraram no estoque;
- **Nova saída** para registrar itens que saíram.

O formulário começa com uma linha **Item + Quantidade**. Ao preencher uma linha válida, outra linha é criada automaticamente, permitindo registrar vários itens na mesma movimentação.

Itens repetidos são agrupados antes do registro.

### 7. Confirme o refino

Depois de calcular uma produção, **Refinar e atualizar estoque** registra a operação.

O aplicativo:

1. consome do estoque os materiais disponíveis usados na receita;
2. considera materiais faltantes comprados para a operação como consumidos imediatamente;
3. adiciona ao estoque os itens refinados produzidos;
4. registra a operação no histórico.

### 8. Histórico e cancelamento

O histórico reúne aportes, saídas e refinamentos confirmados.

Movimentações compatíveis podem ser canceladas para desfazer seu efeito no estoque. A aplicação impede uma reversão quando ela faria algum item ficar com quantidade negativa.

## Quantidade de produção

A quantidade padrão pode ser definida em **Configurações**.

Quando o valor é **0**, o aplicativo calcula a produção possível a partir do estoque.

No modo **Completar com compras**, se não houver materiais no estoque e a quantidade padrão também estiver em 0, o painel libera uma quantidade temporária para simular uma produção sem alterar a configuração padrão.

## Preços de mercado

Os preços vêm do **Albion Online Data Project**. Portanto, a precisão e a atualização dos valores dependem dos dados disponíveis no projeto no momento da consulta.

Sprites dos itens são carregados pelo serviço de renderização de itens do Albion Online.

## Dados locais

Configurações, estoque, histórico e diário selecionado são mantidos no navegador. O projeto não possui conta própria, banco de dados ou sincronização em nuvem.

## Interface responsiva

O layout foi ajustado separadamente para desktop e celular:

- **Desktop:** menu lateral e área de trabalho ampla.
- **Mobile:** navegação compacta e menu hambúrguer dedicado à troca de diário.

## Sobre a organização do código

O aplicativo concentra estrutura HTML, estilos CSS e lógica JavaScript em um único arquivo, permitindo distribuir e abrir o HTML sem instalação ou build. As funções separam consulta de mercado, cálculo, renderização do estoque e registro de movimentações dentro desse arquivo.

A tabela `PROFESSIONS` reúne os nomes e identificadores de recursos e refinados de cada profissão. As mesmas funções de receita, estoque e interface usam a profissão selecionada, reaproveitando a lógica nos cinco diários. Configurações, estoque e histórico usam chaves separadas no `localStorage`.

## Aprendizados aplicados

- Manipulação do DOM e eventos de formulários e navegação.
- Layout responsivo com CSS Grid, Flexbox e media queries.
- Consulta assíncrona de API com `fetch` e tratamento de falhas.
- Persistência de objetos em `localStorage` com JSON.
- Cálculo de produção, retorno de recursos, custos e receitas.
- Validação de configurações antes de consultar o mercado e calcular.
- Registro e reversão de movimentações com validação do estoque.

## Créditos e dados

Este é um projeto independente para auxiliar jogadores de Albion Online.

Dados de mercado: Albion Online Data Project.

Albion Online e seus recursos visuais pertencem aos seus respectivos proprietários.
