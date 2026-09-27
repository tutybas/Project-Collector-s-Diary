# Project Collector's Diary

Aplicação web em arquivo único para acompanhar **coleta, estoque e refino no Albion Online**.

O Collector's Diary foi feito para **jogadores iniciantes e experientes** que querem gastar menos tempo conferindo preços, fazendo contas manualmente e tentando descobrir se compensa mais refinar, vender os materiais ou comprar o que está faltando.

A ideia é simples: você informa e acompanha seu estoque, escolhe o que pretende produzir e deixa o aplicativo cruzar esses dados com **preços de mercado obtidos pela API do Albion Online Data Project**. Assim, o painel concentra as informações necessárias para ajudar na decisão sem precisar ficar alternando entre mercado, calculadora e anotações.

O Collector's Diary reúne cálculo de refino, consulta de mercado, controle de estoque e histórico de movimentações em uma interface que funciona tanto no computador quanto no celular. Ele não joga nem negocia por você: funciona como uma ferramenta de apoio para tornar o processo de coleta e refino mais rápido e organizado.

## O que você pode fazer

- Alternar entre os diários de **Minerador, Lenhador, Curtidor, Tecelão e Pedreiro**.
- Consultar preços do mercado pela Albion Online Data Project.
- Escolher cidade, servidor e critérios de preço usados nas contas.
- Calcular uma produção usando o estoque atual.
- Descobrir quais materiais ainda precisam ser comprados.
- Ver quanto você recebe depois da taxa configurada do mercado.
- Comparar o valor de refinar com o valor de vender os materiais diretamente.
- Registrar recursos e refinados no estoque.
- Registrar aportes e saídas manualmente.
- Confirmar um refino e atualizar o estoque automaticamente.
- Consultar o histórico das movimentações e cancelar movimentações reversíveis.
- Usar a mesma base de estoque entre os diferentes diários.

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

Em **Configurações**, defina os parâmetros usados nos cálculos.

**Servidor e cidade** determinam de onde os preços serão consultados.

**Taxa de retorno** representa a porcentagem esperada de materiais devolvidos durante o refino. O valor padrão usado pelo projeto é 15,2%, mas pode ser alterado.

**Taxa do mercado** é descontada do valor final recebido na venda. Configure de acordo com a situação da sua conta/personagem.

Também é possível escolher qual referência de compra e venda será usada nos dados de mercado.

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

## Versão

### v1.0.0

Primeira versão pública funcional do Project Collector's Diary.

Inclui os cinco diários, consulta de mercado, cálculo de refino, dois modos de produção, estoque persistente, aportes e saídas, histórico reversível e interface responsiva.

## Créditos e dados

Este é um projeto independente para auxiliar jogadores de Albion Online.

Dados de mercado: Albion Online Data Project.

Albion Online e seus recursos visuais pertencem aos seus respectivos proprietários.
