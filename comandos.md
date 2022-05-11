
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