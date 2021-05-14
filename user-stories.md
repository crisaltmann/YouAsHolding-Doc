# User stories

Abaixo as user stories criadas para implementar as necessidades do MVP.

## Storie

1. Cadastro de ativos
   Eu como **investidor**, gostaria de cadastrar os meus ativos, selecionando o ativo, data de compra, quantidade adquirida e o valor total da compra.
   **Com isso** irei poder compor a minha carteira de investimentos.
   
2. Visão da carteira
   Eu como **investidor**, gostaria de visualizar o status atual da minha carteira, podendo visualizar a quantidade detida em cada ativo, bem como o valor atual de cada um deles.
   **Com isso** poderei ter uma visão dos meus ativos e o valor atual deles.
   
3. Importação resultados das empresas
   Eu como **administrador**, gostaria de importar via api, os dados trimestrais divulgados pelas empresas no site da b3, com um arquivo no formato CSV com o seguinte formato:
   CODIGO,TRIMESTRE(ANO-T),RECEITA LÍQUIDA,EBITDA,LUCRO LÍQUIDO,DÍVIDA LÍQUIDA.
   **Com isso** poderei atualizar de forma rápida os fundamentos trimestrais das empresas.
   
4. Serviço de cálculo de resultados das empresas
   Eu como **investidor**, gostaria que os meus dados de carteira trimestral sejam atualizados sempre que um resultado for adicionado ou um ativo cadastrado no sistema. Esta atualização deve considerar a carteira no último dia do trimestre e fazer um cálculo proporcional da posição detida na companhia pelo investidor.
   **Com isso** será possível ter os dados atualizados para visualização. 
   
5. Visão holding
   Eu como **investidor**, gostaria de visualizar a minha carteira, com os dados fundamentalistas acumulados anualmente com base na posição detida por mim na empresa.
   **Com isso** será possível verificar os fundamentos atualizados da minha carteira.
   
6. Insights
   Eu como **investidor**, gostaria de receber insights sobre os destaques no último trimestre. Desta forma deve ser exibido qual ativo da minha carteira teve percentualmente o maior aumento de receita líquida, ebitda e lucro líquido.
   **Com isso** será possível verificar as empresas que mais obtiveram crescimento no trimestre.