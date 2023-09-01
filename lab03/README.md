# Equipe CGU23

# Subgrupo A
* Caio Melloni dos Santos - 167974
* Udson Charles Batagini - 244899
* Guilherme Segolin Selmi - 173947

## Modelo Conceitual ER Revisado

<img src="https://drive.google.com/file/d/1_FgeY1Yc060Qf8oukuzfJCG6cqMqctgK/view?ts=64ef9606" width="400px" height="auto">

*Diagrama ER Revisado*

## Mapeamento para o Modelo Relacional
~~~
ALUNO(Nome, RA , Email)
BANDEJA(ID_bandeja, Data_consumo, RA_aluno)
   -RA_aluno: chave estrangeira para ALUNO
FORMA() - falta a chave primária
CARDÁPIO(Data)
REFEIÇÃO(Tipo, Horário) - falta a chave primária - colocar grupos
REGRA(Nome_porção1, Nome_porção2)
PORÇÃO(Nome, Tipo, Quantidade, Data_preparação) - falta chave primária
INGREDIENTE(ID_ingrediente, Nome, Grupo, Quantidade, Ref_ingrediente)
   - Ref_ingrediente: chave estrangeira para INGREDIENTE
~~~
