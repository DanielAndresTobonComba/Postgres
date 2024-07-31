# Postgres
## Comandos
Ingresar: psql --host=localhost --username=postgres
Create database "nombre_db". 
\c "nombre_db": Usar una db creada. 
\l: para listar la dbs creadas.

\D describir una tabla.

## Tablas y tipos de datos 
-- CREAR UN DATO DE TIPO ENUM
CREATE TYPE mood AS ENUM ('sad', 'ok', 'happy');
CREATE TYPE estadocivil AS ENUM ('Casado(a)', 'Soltero(a)', 'Viudo(a)','Con
pelo(a)');

CREATE TABLE person (
name text,
current_mood mood
);

INSERT INTO person VALUES ('Moe', 'happy');
SELECT * FROM person WHERE current_mood = 'happy';

-- TIPOS DE CONSTRIANS 
CHECK: Asegura que los valores en una columna cumplen una condición especificada.
edad integer NOT NULL CHECK (edad > 0);


## AÑADIR CONSTRAINS A UNA TABLA
ALTER TABLE empleados ADD PRIMARY KEY (id);

ALTER TABLE empleados ADD CONSTRAINT fk_departamento
FOREIGN KEY (departamento_id) REFERENCES departamentos(id);

ALTER TABLE empleados ADD CONSTRAINT unique_nombre_departamento UNIQUE (nombre,
departamento_id);

ALTER TABLE empleados ALTER COLUMN nombre SET NOT NULL;

ALTER TABLE empleados ADD CONSTRAINT check_edad CHECK (edad > 0);

ALTER TABLE empleados ALTER COLUMN salario SET DEFAULT 0.00;

## Ejemplo importante

CREATE TABLE ejemplo (
id serial PRIMARY KEY, -- serial: Entero con auto-incremento
nombre varchar(100) NOT NULL, -- varchar: Cadena de longitud
variable con límite
descripcion text, -- text: Cadena de longitud variable
sin límite
precio numeric(10, 2) NOT NULL, -- numeric: Número de precisión
arbitraria
en_stock boolean NOT NULL, -- boolean: Valor booleano
fecha_creacion date NOT NULL, -- date: Fecha (sin hora)
hora_creacion time NOT NULL, -- time: Hora del día (sin fecha)
fecha_hora timestamp NOT NULL, -- timestamp: Fecha y hora (sin huso
horario)
fecha_hora_zona timestamp with time zone, -- timestamp with time zone: Fecha
y hora con huso horario
duracion interval, -- interval: Período de tiempo
direccion_ip inet, -- inet: Dirección IP
direccion_mac macaddr, -- macaddr: Dirección MAC
punto_geometrico point, -- point: Punto en un plano de dos
dimensiones
datos_json json, -- json: Datos en formato JSON
datos_jsonb jsonb, -- jsonb: Datos JSON en un formato
binario más eficiente
identificador_unico uuid, -- uuid: Identificador único
universal
estado_monetario money, -- money: Cantidad monetaria
rangos int4range, -- range: Rango de valores
colores_preferidos varchar(20)[] -- array: Arreglo de cadenas
);


## ENUM Y TYPE 

-- Ejemplo de tipo ENUM
CREATE TYPE estadocivil AS ENUM ('Casado(a)', 'Soltero(a)', 'Viudo(a)','Con
pelo(a)');
CREATE TYPE estado_pedido AS ENUM ('pendiente', 'en_proceso', 'completado',
'cancelado');
CREATE TABLE pedidos (
id serial PRIMARY KEY,
estado estado_pedido NOT NULL -- enum: Conjunto de valores
predefinidos
);

-- Ejemplo de tipo compuesto
CREATE TYPE direccion_completa AS (
calle varchar,
ciudad varchar,
codigo_postal integer
);

CREATE TABLE clientes (
id serial PRIMARY KEY,
nombre varchar(50),
ecivil estadocivil,
direccion direccion_completa 
);

