
```sql
INSERT INTO professores (nome, area) VALUES ('Jon Oliva'),('infra');
```

```sql
INSERT INTO professores (nome)
VALUES('Adilson'),('Claudio'),('Rogério'), ('Palloma');
=======
### Criado a tabela tecinternet

```sql
CREATE TABLE `tecinternet_escola_gabriel_genovez`.`cursos` ( `id` INT NOT NULL AUTO_INCREMENT , `titulo` VARCHAR(30) NOT NULL , `carga` SMALLINT NOT NULL , `professor_id` INT NULL , PRIMARY KEY (`id`)) ENGINE = InnoDB;
```

### Criando os campos da tabela

```sql
CREATE TABLE `tecinternet_escola_gabriel_genovez`.`professores` ( `id` INT NOT NULL AUTO_INCREMENT , `nome` VARCHAR(50) NOT NULL , `area` ENUM('design','desenvolvimento','infra') NOT NULL , `curso_id` INT NOT NULL , PRIMARY KEY (`id`)) ENGINE = InnoDB;
```

```sql
CREATE TABLE `tecinternet_escola_gabriel_genovez`.`alunos` ( `id` INT NOT NULL AUTO_INCREMENT , `nome` VARCHAR(50) NOT NULL , `data` DATE NOT NULL , `primeira_nota` DECIMAL(4,2) NOT NULL , `segunda_nota` DECIMAL(4,2) NOT NULL , `curso_id` INT NOT NULL , PRIMARY KEY (`id`)) ENGINE = InnoDB;
```

### Adicionando as chaves estrangeiras
```sql
ALTER TABLE `alunos` ADD CONSTRAINT `fk_alunos_cursos` FOREIGN KEY (`curso_id`) REFERENCES `cursos`(`id`) ON DELETE RESTRICT ON UPDATE RESTRICT;
```

```sql
ALTER TABLE `professores` ADD CONSTRAINT `fk_professores_cursos` FOREIGN KEY (`curso_id`) REFERENCES `cursos`(`id`) ON DELETE RESTRICT ON UPDATE RESTRICT;
```

```sql
ALTER TABLE `cursos` ADD CONSTRAINT `fk_cursos_professores` FOREIGN KEY (`professor_id`) REFERENCES `professores`(`id`) ON DELETE RESTRICT ON UPDATE RESTRICT;
```

### Imputando os dados
```sql
INSERT INTO cursos(id, titulo, carga, professor_id) VALUES(
    1,
    'Front-End',
    '40',
    ''
),
(2,
'Back-End',
'80',
2
),
(3,
'UX/UI Design',
3),
(
    4,
    'Figma',
    '10',
    4
),
(
    5,
    'Redes de Computadores',
    '100',
    5
);
```

```sql
INSERT INTO professores(id, nome, area, curso_id) VALUES(
    1,
    'Serjão',
    'infra',
    1
),
(2,
'Luis Inácio',
'design',
2
),
(3,
'Tio Patinhas',
'design'
3),
(
    4,
    'Ignacinho',
    'desenvolvimento',
    4
),
(
    5,
    'Xispirito',
    'desenvolvimento',
    5
);
```

### Fazendo update dos índices
```sql
UPDATE `professores` SET `curso_id` = '5' WHERE `professores`.`id` = 1
UPDATE `professores` SET `curso_id` = '4' WHERE `professores`.`id` = 2
UPDATE `professores` SET `curso_id` = '2' WHERE `professores`.`id` = 4
UPDATE `professores` SET `curso_id` = '1' WHERE `professores`.`id` = 5

```
### Inserindo os alunos 
```sql
INSERT INTO alunos(id, nome, datas, primeira_nota, segunda_nota, curso_id) VALUES (
    1,
    'Gabriel Genovez',
    18/04/2000,
    6,
    10,
    1
)
(
    2,
    'Thiago Ribeiro',
    20/11/2003,
    8,
    4,
    2
)
(
    3,
    'Palloma Hortencio',
    21/03/2001,
    7,
    5,
    3
)
(
    4,
    'Lucas Mendes',
    23/07/2002,
    8,
    7,
    2
)
(
    5,
    'Rafael Augusto',
    21/06/1994
    8,
    8,
    4
)
(
    6,
    'Emanuelle Genovez',
    27/09/2003,
    6,
    9,
    2
)
(
    7,
    'Gabriel Luna',
    10/10/1993,
    7,
    8,
    4
)
(
    8,
    'Felipe Lima',
    04/01/1994,
    8,
    7,
    2
)
(
    9,
    'Veronica Silva',
    05/05/1995
    10,
    10,
    1
)
(
    10,
    'Matheus Anthony',
    12/06/2002,
    8,
    9,
    1
);

```

<!-- PARTE 3 EXERCÍCIO SQL -->

<!-- Faça uma consulta que mostre os alunos que nasceram antes do ano 2009 -->
```sql
SELECT * FROM alunos WHERE datas >= 2009/12/31;
```

<!--Capturando as notas inseridas no sistema e calculando a média definindo casas decimais -->
```sql
SELECT primeira_nota, segunda_nota, ROUND((primeira_nota + segunda_nota)/2 ,2) AS 'Média' FROM alunos;
```

<!-- Capturando os dados do curso/ carga e realizando o calculo de limite de faltas = 25%. -->
```sql
SELECT titulo, carga, (carga * 0.25) FROM cursos ORDER BY titulo;
```

<!-- Consultando os professores da área de desenvolvimento. -->
```sql
SELECT nome, area FROM professores WHERE area = 'desenvolvimento';
```


<!-- Consultando a quantidade de professores por área de atuação -->
```sql
SELECT area, COUNT(nome) AS professores FROM professores GROUP BY area;
```


<!-- Fazendo uma consulta que mostra o nome dos alunos ultilizando o INNER JOIN que busca dados de uma outra tabela. -->
```sql
SELECT alunos.nome AS alunos, titulo, cursos.carga FROM
 alunos INNER JOIN cursos
  ON alunos.curso_id = cursos.id 
  ORDER BY alunos.nome;
```

<!-- Fazendo uma consulta que mostra o nome dos professores  ultilizando o INNER JOIN que busca busca dados -->
```sql
SELECT professores.nome AS alunos, titulo, professores FROM
 professores INNER JOIN cursos
  ON alunos.curso_id = cursos.id 
  ORDER BY professores.nome;
```

<!-- Realizando uma consulta que mostre a quantidade de alunos que cada curso possui  -->
```sql
SELECT alunos.nome AS 'Alunos', cursos.titulo AS 'Cursos', professores.nome AS 'Professores' FROM alunos INNER JOIN cursos ON alunos.curso_id = cursos.id INNER JOIN professores ON cursos.professor_id = professores.id;
```


<!-- Realizando uma consulta de que cada curso possui. Classificando os resultados em ordem decrescente com o DESC.  -->
```sql
SELECT(cursos.titulo) AS 'Cursos', COUNT(alunos.cursos_id) AS "Qtd Alunos" FROM alunos INNER JOIN cursos ON alunos.curso_id = cursos.id GROUP BY curso_id ORDER BY curso_id DESC 
```

<!-- Fazendo uma consulta que traz o nome dos alunos,notas,médias e os titulos dos cursos. e estão sendo exibidos apenas os alunos de FRONT/BACK-End -->
```sql
SELECT nome, primeira_nota, segunda_nota, ROUND((primeira_nota + segunda_nota)/2) AS 'Média',cursos.titulo FROM alunos INNER JOIN cursos ON alunos.curso_id = cursos.id WHERE cursos.titulo = 'Front-End' OR cursos.titulo = 'Back-End' GROUP BY alunos.nome ORDER BY alunos.nome ASC;
```

```sql
UPDATE cursos SET titulo 'Adobe XD' WHERE id = 4  UPDATE cursos SET carga = 15 WHERE id = 4
```

```sql
SELECT alunos.nome, cursos.titulo FROM alunos INNER JOIN cursos ON alunos.curso_id = cursos.id ORDER BY alunos.nome;
```

<!-- DESAFIOS -->

```sql
--Criar uma consulta que calcule a idade do aluno
SELECT nome AS Nome, TIMESTAMPDIFF(YEAR, nascimento, curdate()) AS Idade FROM alunos;
```

```sql
--Criar uma consulta  que calcule a média das notas de cada aluno e mostre somente os alunos que tiveram a nota >= 7
SELECT nome, primeira_nota, segunda_nota, ROUND((primeira_nota+segunda_nota)/2) AS Média FROM alunos WHERE (primeira_nota+segunda_nota)/2 >= 7;
```

```sql
-- Criar uma consulta que calcule a média das notas de cada aluno e mostre somente os alunos que tiveram a média menor que 7
SELECT nome, primeira_nota, segunda_nota, ROUND((primeira_nota+segunda_nota)/2) AS Média FROM alunos WHERE (primeira_nota+segunda_nota)/2 < 7;
```

```sql
-- Criar uma consulta que mostre a quantidade de alunos com média <= 7
SELECT COUNT((primeira_nota+segunda_nota)/2) AS 'Qtd alunos com média acima ou igual à 7' FROM alunos WHERE (primeira_nota+segunda_nota)/2 >= 7;
```
<!-- FIM Desafios -->