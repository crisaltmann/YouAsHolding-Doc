# Arquitetura produto.

Abaixo segue o modelo de arquitetura do projeto

## Arquitetura

![](https://github.com/crisaltmann/YouAsHolding-Doc/blob/main/doc/Arquitetura.jpg)

O sistema é composto pelos componentes web, backend e banco de dados.

Na primeira versão será disponibilizada uma camada web como canal para os usuários cadastrarem os ativos e visualizarem a carteira.

O serviço fundament-stock-api é responsável por expor apis e gerenciar os dados de ativos e carteira do usuário. Os dados são salvos em um banco de dados relacional dado que a natureza dos dados é de relacionamento com chaves.

Foram criados dois componentes separados por questões de escalabilidade, pois estes podem ser alterados e incrementados com outras opções.

Um dos serviços é o de importação que nesta versão será uma planilha CSV. Esta importação de dados dos ativos e fundamentos, pode ser no futuro conectado com API's e outras fontes de dados que podem alimentar as apis de stock.

Já o serviço de job sync é responsável por conectar e buscar informações com jobs. Nesta versão será realizada a atualização da cotação de fechamento diário dos ativos.