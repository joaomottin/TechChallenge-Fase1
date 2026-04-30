# Tech Challenge - Fase 1

## Sobre o projeto

Este repositório contém o trabalho acadêmico desenvolvido para o **Tech Challenge - Fase 1** da FIAP, com base no case de e-commerce da Olist.

O objetivo do projeto é transformar dados transacionais em uma análise executiva voltada para tomada de decisão. A partir da base pública da Olist, o grupo avaliou como vendedores com baixa satisfação podem afetar a confiabilidade percebida do ecossistema, considerando sua participação em quantidade de vendedores, pedidos e receita.

## Pergunta central

Vendedores com baixa satisfação representam apenas casos isolados ou indicam um risco relevante para a confiança no ecossistema Olist?

## Contexto da análise

A Olist atua como um ecossistema que conecta vendedores a grandes marketplaces. Nesse modelo, a experiência entregue por cada parceiro pode impactar a percepção dos clientes sobre a marca como um todo.

Por isso, a análise considera que avaliações baixas não são apenas indicadores individuais de desempenho, mas também sinais de atenção para a reputação e a confiança da plataforma.

## Metodologia resumida

O estudo utiliza dados de pedidos, itens do pedido, avaliações e vendedores da base pública da Olist.

Principais tratamentos aplicados:

- foram mantidos apenas pedidos entregues (`delivered`) com data de entrega preenchida;
- foram consideradas avaliações válidas entre 1 e 5;
- duplicidades de avaliação por `order_id` foram removidas;
- itens sem vendedor identificado ou com preço inválido foram desconsiderados;
- a visão final foi consolidada por `seller_id`.

Para calcular satisfação, cada avaliação foi considerada uma única vez por combinação de pedido e vendedor. Esse tratamento evita que pedidos com múltiplos itens tenham peso maior na média de avaliação do vendedor.

A base operacional possui 2.970 vendedores com pedidos entregues e receita consolidada. Para a segmentação de satisfação, foram considerados apenas os 2.965 vendedores com avaliação válida. Cinco vendedores possuem pedido entregue, mas não possuem avaliação registrada e, por isso, ficam fora da classificação binária entre detratores e não detratores.

A receita foi calculada separadamente pela soma dos preços dos itens vendidos, pois cada item possui valor próprio dentro do pedido.

## Regra de classificação

A análise utilizou a média de avaliações (`review_score`) como proxy de NPS/satisfação, já que a base pública não contém a pergunta formal de NPS.

A classificação principal foi:

- **Detratores:** vendedores com `media_nota <= 3`;
- **Não detratores:** vendedores com `media_nota > 3`;
- **Faixa de atenção:** vendedores com média maior que 3 e menor ou igual a 4;
- **Saudáveis:** vendedores com média maior que 4.

## Principais resultados

Com a metodologia aplicada, foram analisados **2.965 vendedores com avaliação válida**.

| Indicador | Resultado |
|---|---:|
| Vendedores detratores | 242 |
| Participação dos detratores na base avaliada | 8,16% |
| Participação dos detratores nos pedidos | 0,91% |
| Participação dos detratores na receita | 1,83% |
| Média por vendedor com detratores | 4,18 |
| Média por vendedor sem detratores | 4,35 |
| Receita média por vendedor não detrator | R$ 4.764 |
| Receita média por vendedor detrator | R$ 1.000 |

A leitura principal é que os vendedores detratores representam uma parcela pequena da base, dos pedidos e da receita. O risco identificado está menos associado ao volume financeiro e mais à possibilidade de impacto reputacional e perda de confiança no ecossistema.

## Arquivos principais

- `Analise_vendedores_baixa_nota_V01.ipynb`: notebook com carregamento, limpeza, preparação da base, segmentação dos vendedores, cálculo dos indicadores e geração dos gráficos.
- `data/`: pasta com os arquivos CSV utilizados na análise.

## Como executar

1. Abra o notebook `Analise_vendedores_baixa_nota_V01.ipynb`.
2. Confirme que os arquivos CSV estão disponíveis na pasta `data/`.
3. Execute as células em ordem.

Bibliotecas utilizadas:

- `pandas`
- `matplotlib`

## Base de dados

A análise foi desenvolvida com o **Brazilian E-Commerce Public Dataset by Olist**, base pública com informações de pedidos, itens do pedido, vendedores, avaliações e entregas do e-commerce brasileiro.

Fonte: [Kaggle - Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

## Integrantes

| Nome | RM | E-mail |
|---|---|---|
| Felipe Macedo da Silva | RM373436 | felipemsdocs@gmail.com |
| João Pedro Mezzadri Mottin | RM372545 | joaopedromm.construtiva@outlook.com |
| Miguel Fernandes Martins de Bastos | RM373815 | miguelbastospro@gmail.com |
| Thanael Butewicz | RM373935 | zthanaelbutewicz@hotmail.com |
| Verônica de Fátima Machado Silva | RM371976 | v.machado10@hotmail.com |
