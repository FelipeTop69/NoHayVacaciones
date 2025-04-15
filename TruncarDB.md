# 📦 Procedimientos Almacenados para Truncar Base de Datos y Tablas

Este documento describe procedimientos almacenados para **eliminar todos los registros** de una base de datos o de una tabla específica y **reiniciar los valores autoincrementales** en los sistemas de gestión de bases de datos: **SQL Server**, **PostgreSQL** y **MySQL**.

---

## :floppy_disk: SQL Server

### `sp_Kill_All`

```sql
CREATE PROCEDURE sp_Kill_All
AS
BEGIN
    SET NOCOUNT ON;

    -- Desactiva temporalmente todas las claves foráneas
    EXEC sp_msforeachtable 'ALTER TABLE ? NOCHECK CONSTRAINT ALL';

    -- Elimina los datos de todas las tablas
    EXEC sp_msforeachtable 'DELETE FROM ?';

    -- Reinicia los valores IDENTITY en las tablas que los tengan
    EXEC sp_msforeachtable '
        IF EXISTS (
            SELECT 1 FROM sys.identity_columns 
            WHERE object_id = OBJECT_ID(''?'')) 
        BEGIN 
            DBCC CHECKIDENT (''?'', RESEED, 0) 
        END';

    -- Reactiva las claves foráneas
    EXEC sp_msforeachtable 'ALTER TABLE ? WITH CHECK CHECK CONSTRAINT ALL';
END;
```

### ¿Como Usar?

```sql
EXEC sp_Kill_All;
```


### `sp_Kill_Table`

```sql
CREATE PROCEDURE sp_Kill_Table
    @NombreTabla NVARCHAR(128)
AS
BEGIN
    SET NOCOUNT ON;

    DECLARE @SQL NVARCHAR(MAX);

    -- Elimina los registros de la tabla
    SET @SQL = 'DELETE FROM [' + @NombreTabla + '];';
    EXEC sp_executesql @SQL;

    -- Reinicia el IDENTITY si existe
    SET @SQL = '
        IF EXISTS (
            SELECT 1 
            FROM sys.identity_columns 
            WHERE object_id = OBJECT_ID(''' + @NombreTabla + ''')
        )
        BEGIN
            DBCC CHECKIDENT (''' + @NombreTabla + ''', RESEED, 0);
        END';
    EXEC sp_executesql @SQL;
END;
```

### ¿Como Usar?

```sql
EXEC sp_Kill_Table 'NombreDeLaTabla'; 
```


---
---
---


##  PostgreSQL

### `sp_Kill_All`

```sql
CREATE OR REPLACE PROCEDURE sp_Kill_All()
LANGUAGE plpgsql
AS $$
DECLARE
    tabla RECORD;
BEGIN
    -- Desactiva claves foráneas
    EXECUTE 'SET session_replication_role = replica';

    FOR tabla IN
        SELECT tablename FROM pg_tables WHERE schemaname = 'public'
    LOOP
        EXECUTE 'TRUNCATE TABLE ' || quote_ident(tabla.tablename) || ' RESTART IDENTITY CASCADE';
    END LOOP;

    -- Reactiva claves foráneas
    EXECUTE 'SET session_replication_role = origin';
END;
$$;

```

### ¿Como Usar?

```sql
CALL sp_Kill_All();
```


### `sp_Kill_Table`

```sql
CREATE OR REPLACE PROCEDURE sp_Kill_Table(nombre_tabla TEXT)
LANGUAGE plpgsql
AS $$
BEGIN
    EXECUTE 'TRUNCATE TABLE ' || quote_ident(nombre_tabla) || ' RESTART IDENTITY CASCADE';
END;
$$;
```

### ¿Como Usar?

```sql
CALL sp_Kill_Table('nombre_tabla');
```


---
---
---


##  MySQL

### `sp_Kill_All`

```sql
DELIMITER $$

CREATE PROCEDURE sp_Kill_All()
BEGIN
    DECLARE done INT DEFAULT 0;
    DECLARE tabla VARCHAR(255);
    DECLARE cur CURSOR FOR 
        SELECT table_name 
        FROM information_schema.tables 
        WHERE table_schema = DATABASE();
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET done = 1;

    SET FOREIGN_KEY_CHECKS = 0;

    OPEN cur;
    read_loop: LOOP
        FETCH cur INTO tabla;
        IF done THEN
            LEAVE read_loop;
        END IF;
        SET @sql = CONCAT('TRUNCATE TABLE `', tabla, '`;');
        PREPARE stmt FROM @sql;
        EXECUTE stmt;
        DEALLOCATE PREPARE stmt;
    END LOOP;
    CLOSE cur;

    SET FOREIGN_KEY_CHECKS = 1;
END$$

DELIMITER ;
```
### ¿Como Usar?

```sql
CALL sp_Kill_All();
```


### `sp_Kill_Table`

```sql
DELIMITER $$

CREATE PROCEDURE sp_Kill_Table(IN nombre_tabla VARCHAR(255))
BEGIN
    SET @sql = CONCAT('TRUNCATE TABLE `', nombre_tabla, '`;');
    PREPARE stmt FROM @sql;
    EXECUTE stmt;
    DEALLOCATE PREPARE stmt;
END$$

DELIMITER ;
```

### ¿Como Usar?

```sql
CALL sp_Kill_Table('nombre_tabla');
```