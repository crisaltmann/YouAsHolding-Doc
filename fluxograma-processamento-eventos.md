## Fluxograma processamento de eventos

Abaixo esta representado o fluxo para processar os eventos.

![](https://github.com/crisaltmann/YouAsHolding-Doc/blob/main/doc/Design_aplicacao.png "Design")

A aplicação de backend é dividida nos componentes:

<ul>
    <li>
        <p>**Importer**: Este componente possui o controle e parsers de importação de resultados. Neste momento o parser é feito de um arquivo xlsx com o balanço patrimonial e DRE trimestral de uma empresa.</p> 
        <p>Uma vez processado e salvo o resultado, é gerado um evento notificando o ativo e o trimestre que foi gerado um resultado.</p>
    </li>
    <li>
        <p>**Order**: Componente responsável por cadastrar a movimentação de um ativo. Uma vez que a movimentação é validada e salva, um evento de movimentação do usuário é gerado para o recalculo do portfólio.</p>
    </li>
    <li>
        <p>**Holding**: Componente que possui dois consumidores que leem os dados gerados e executa o fluxo detalhado abaixo. Uma vez consumido o evento, calculado o resultado e salvo é gerado um evento indicando este processo foi concluído.</p>
    </li>
    <li>
        <p>**Insights**: Uma vez que um portfólio é atualizado através da notificação do evento, o consumidor de insights processa os dados de destaques entre trimestres. Os dados são salvos no banco de dados</p>
    </li>
    <li>
        <p>**Rest api**: Os demais domínios da aplicação são disponibilizados através de uma api rest que recebe e processa as requisições. As apis existentes são: Ativo, Trimestre, Movimentação, Holding, Insights.</p>
    </li>
</ul>


O componente central desta arquitetura é o que calcula o dado de holding. Este dado, nada mais é que calcular o percentual detido por cada investidor em determinado ativo, e gerar um resultado proporcional com base no resultado divulgado pelas empresas.

Como exemplo, se um investidor deter 10% de uma empresa e esta empresa declara uma receita líquida de 1 milhão, a receita líquida deste investidor para este ativo é de: 1 Milhão * 10% = 100 mil.

Abaixo o fluxograma e a explicação das etapas do mesmo:

![](https://github.com/crisaltmann/YouAsHolding-Doc/blob/main/doc/Fluxograma_consumo_evento.png "Fluxograma consumo evento")

Para o processamento de um evento de resultado trimestral e movimentação de um usuário é executado este fluxo. Para ambos os eventos é necessário recalcular o portfólio, holding e insights do usuário pois o resultado ou movimentação cadastrado pode ser de um trimestre anterior.

<ol>
<li>Busca todos os usuário que possuem o ativo em carteira.</li>
<li>Inicia uma transação com o banco de dados e remove todos os dados das tabelas de insights e portfolio_trimestre.</li>
<li>Inicia o cálculo de portfolio.</li>
<li>Busca todos os trimestres cadastrados.</li>
<li>Para cada trimestre, busca a posição da carteira de um usuário da data final do trimestre.</li>
<li>Busca o resultado trimestral para cada ativo detido pelo investidor na data final do trimestre.</li>
<li>Executa o cálculo percentual do resultado pela posição detida pelo investidor.</li>
<li>Salva o cálculo de percentual e comita a transação.</li>
<li>Gera evento de resultado gerado.</li>
</ol>