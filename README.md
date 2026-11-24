# VendasPortifolio
Resumo do projeto
 De onde partimos
O ponto de partida eram planilhas de vendas de um e-commerce de moda (Amazon India): vendas Amazon (mar–jun/2022, com status, categoria, estado e valor líquido), vendas internacionais (jun/2021–mai/2022, por cliente e sem número de pedido), uma planilha de estoque por SKU e uma lista de preços. Os dados estavam crus: categorias com grafias diferentes entre fontes, 6 SKUs duplicados no estoque, linhas internacionais sem categoria e taxonomias que não batiam entre si (ex.: SET na Amazon x KURTA SET no estoque).

O que foi feito
Silver: limpeza e normalização dos dados brutos — categorias normalizadas, estoque deduplicado por sku_code, tipagem de datas e valores, marcando cancelamentos (is_cancelled).
Gold: três tabelas prontas para análise em workspace.gold:
product_stock — 1 linha por SKU (9.171 SKUs), com categoria, tamanho, cor e estoque total;
sales_consolidated — fato unificada das duas fontes (147.610 linhas), com esquema comum (source = AMAZON | INTERNACIONAL), categoria herdada do estoque apenas para a fonte internacional e preços unitários padronizados;
sales_monthly_summary — 16 meses agregados por fonte: receita bruta/líquida, unidades, pedidos e taxa de cancelamento.
Validação: contagens e receitas conferidas; a lista de preços ficou de fora após testes de join (sku e style) — 0 sobreposições com as vendas.

Resultado
De planilhas dispersas e inconsistentes para um modelo analítico confiável e pronto para dashboards: receita bruta Amazon de ₹ 78,6 M (líquida ₹ 71,7 M) e internacional de ₹ 15,8 M consolidadas na mesma tabela, com métricas mensais e taxa de cancelamento por fonte. Os 1.807 registros internacionais sem categoria (~2% da receita) foram mantidos e sinalizados como SEM CATEGORIA em vez de descartados, preservando a integridade dos totais.
