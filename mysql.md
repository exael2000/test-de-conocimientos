## Sección 4: MySQL

1. **Pregunta de Código:**
- Escribe una consulta SQL para crear una base de datos llamada company y una tabla llamada employees con las siguientes columnas: id (INT, auto-increment, primary key), name (VARCHAR(100)), position (VARCHAR(50)), salary (DECIMAL(10, 2)), y hire_date (DATE).
    CREATE DATABASE company;

    USE company;

    CREATE TABLE employees (
        id INT AUTO_INCREMENT PRIMARY KEY,
        name VARCHAR(100) NOT NULL,
        position VARCHAR(50) NOT NULL,
        salary DECIMAL(10, 2) NOT NULL,
        hire_date DATE NOT NULL
    );


1. **Pregunta Teórica:**
- Explica la diferencia entre una clave primaria (Primary Key) y una clave foránea (Foreign Key) en MySQL. ¿Cuándo y por qué se utilizan?
    Primary Key: Es un campo (o combinación de campos) que identifica de manera única cada registro en una tabla. No puede contener valores nulos y debe ser único.
    Foreign Key: Es un campo en una tabla que se refiere a la clave primaria en otra tabla, estableciendo una relación entre las dos tablas. Se utiliza para mantener la integridad referencial y asegurar que los datos sean consistentes y correctos.

1. **Pregunta de Código:**
- Escribe una consulta SQL para insertar tres registros en la tabla employees creada en la pregunta 2.
    INSERT INTO employees (name, position, salary, hire_date) VALUES
    ('John Doe', 'Manager', 75000.00, '2020-01-15'),
    ('Jane Smith', 'Developer', 65000.00, '2019-03-23'),
    ('Mike Johnson', 'Analyst', 60000.00, '2018-07-11');


1. **Pregunta de Código:**
- Muestra cómo actualizar el salario de un empleado específico en la tabla employees. Por ejemplo, actualiza el salario del empleado con id = 1 a 60000.00.
    UPDATE employees
    SET salary = 60000.00
    WHERE id = 1;


1. **Pregunta de Código:**
- Escribe una consulta SQL para seleccionar todos los empleados cuyo salario sea mayor a 50000.00 y ordenarlos por el campo hire_date en orden descendente.
    SELECT * FROM employees
    WHERE salary > 50000.00
    ORDER BY hire_date DESC;


1. **Pregunta Teórica:**
- ¿Qué es una transacción en MySQL y cómo se utiliza? Proporciona un ejemplo de uso.
    Transacción: Es una secuencia de una o más consultas SQL que se ejecutan como una unidad de trabajo. Asegura que todas las operaciones se completen exitosamente antes de confirmar los cambios. Si ocurre un error, se puede deshacer la transacción para mantener la integridad de los datos.
    Codigo:
    START TRANSACTION;

    UPDATE employees SET salary = 80000.00 WHERE id = 2;
    INSERT INTO employees (name, position, salary, hire_date) VALUES ('Alice Brown', 'Designer', 70000.00, '2021-05-30');

    COMMIT;  -- Para confirmar los cambios
    -- ROLLBACK;  -- Para deshacer los cambios en caso de error


1. **Pregunta de Código:**
- Crea una vista en MySQL llamada high_earning_employees que seleccione todas las columnas de los empleados cuyo salario sea mayor a 70000.00.
    CREATE VIEW high_earning_employees AS
    SELECT * FROM employees
    WHERE salary > 70000.00;