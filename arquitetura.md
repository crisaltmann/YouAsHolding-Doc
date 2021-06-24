# Arquitetura produto.

Abaixo segue o modelo de arquitetura do projeto

## Arquitetura

![](https://github.com/crisaltmann/YouAsHolding-Doc/blob/main/doc/Arquitetura.jpg)

O sistema é composto pelos componentes web, backend, banco de dados e filas.

A camada web é responsável por exibir os dados para o usuário e permite o cadastro de movimentações.

O serviço fundament-stock-api é responsável por expor apis e gerenciar os dados de ativos e carteira do usuário. Os dados são salvos em um banco de dados relacional dado que a natureza dos dados é de relacionamento com chaves.

O serviço gera e consome eventos relacionados a cadastro de movimentação e resultado trimestrais. Tais ações devem recalcular os dados de holding da carteira do investidor. O uso de fila aqui, permite que a transação seja processada e os cálculos, que podem ser custosos em tempo de processamento, sejam, executados de forma assíncrona.

O componente de importação, permite receber dados de empresas e faz o parser de um xlsx para o formato de dados da aplicação. Quando este parser é realizado, além do cadastro em banco é gerado um evento para reprocessamento.

Já o componente de job sync é responsável por conectar e buscar informações com jobs. Nesta versão será realizada a atualização da cotação de fechamento diário dos ativos.