# Equipe Data Miners

# Subgrupo B
* Caio Melloni dos Santos - 167974
* Udson Charles Batagini - 244899
* Guilherme Segolin Selmi - 173947

## Tarefa de Cypher sobre Patologias, Medicamentos e Efeitos Colaterais

## Exercício

Faça a projeção em relação a Patologia, ou seja, conecte patologias que são tratadas pela mesma droga.

### Resolução
~~~cypher
MATCH (p1:Pathology)<-[a]-(d:Drug)-[b]->(p2:Pathology)
MERGE (p1)<-[r:Relates]->(p2)
ON CREATE SET r.weight=1
ON MATCH SET r.weight=r.weight+1
~~~

# Trabalhando com Efeitos Colaterais

Considere o seguinte arquivo que indica um conjunto de pessoas (identificadas por código) e as drogas que elas usam:

[https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv]

Considere este outro arquivo que indica as mesmas pessoas e efeitos colaterais que elas experimentaram:

[https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv]

## Exercício

Construa um grafo ligando os medicamentos aos efeitos colaterais (com pesos associados) a partir dos registros das pessoas, ou seja, se uma pessoa usa um medicamento e ela teve um efeito colateral, o medicamento deve ser ligado ao efeito colateral.

### Resolução
~~~cypher
//Create Persons and their relations
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/drug-use.csv' as persons
MATCH (d:Drug {code: persons.codedrug})
MATCH (h:Pathology {code: persons.codepathology})
MERGE (p:Person {id: persons.idperson})
CREATE (p)-[a:Uses]->(d)
CREATE (h)-[b:Affects]->(p)
~~~
~~~cypher
//Index for Person Id
CREATE INDEX FOR (var:Person) ON var.id
~~~
~~~cypher
//Creates relations
LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/santanche/lab2learn/master/data/faers-2017/sideeffect.csv' as sideef

MATCH (p:Person {id: sideef.idPerson})-[:Uses]->(d:Drug)
MATCH (h:Pathology {code: sideef.codePathology})
MERGE (d)-[r:SideEffect]->(h)
ON CREATE SET r.weight=1
ON MATCH SET r.weight=r.weight+1
~~~

## Exercício

Que tipo de análise interessante pode ser feita com esse grafo?

Proponha um tipo de análise e escreva uma sentença em Cypher que realize a análise.

### Resolução

Quais as drogas com maiores incidências de colaterais
~~~cypher
MATCH (d:Drug)-[s:SideEffect]->(p:Pathology)
WHERE s.weight > 20
return d,s,p
~~~
