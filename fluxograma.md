# Fluxograma.

Segue abaixo o fluxograma das principais atividades realizadas no sistema.

![](https://github.com/crisaltmann/YouAsHolding-Doc/blob/main/doc/Fluxo-youasholding.jpeg "Fluxograma")

O fluxograma acima cita 4 processos distintos:

## Cadastro movimentação ativo

1. Usuário cadastra a movimentação de um ativo.
2. Movimentação é salva na base.
3. Com base na data da movimentação recalcula a carteiras finais dos trimestres.
4. Executa recalculo.

## Administrador insere resultado trimestral (CSV)

1. Administrador insere resultado em CSV.
2. Para cada linha válida, insere evento de atualização trimestre.
3. Consome evento e atualiza resultado trimestral da empresa.
4. Executa recalculo.

## Atualiza cotação diária
1. Job executa atualização diária dos ativos existentes.
2. Cada ativo é inserido em fila de atualização.
3. Busca dado de cotação de fechamento na api yahoo finance.
4. Atualiza cotação fechamento no sistema.

## Executa recalculo
1. Com base na data base de recalculo.
2. Remove dados de calculo proporcional de fundamentos.
3. Calculo fechamento proporcional por ativo no trimestre.
4. Consolida e salva o dado do ativo.