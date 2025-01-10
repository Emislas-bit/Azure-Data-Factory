<h1 align='left'>Azure Data Factory: Proyecto ETL con Integración Local y en la Nube</h1>

<p align='left'>
Este proyecto utiliza Azure Data Factory para implementar un flujo ETL que conecta datos locales y en la nube. Incluye la carga de un archivo Excel local en una base de datos SQL, seguido de la transferencia de datos a una segunda base de datos SQL. Hace uso de pipelines, datasets, linked services y un Self-hosted Integration Runtime (SHIR) para conectar recursos locales con la nube.
</p>

---

<h3 align='left'>Requisitos Previos:</h3>
<ul align='left'>
  <li>Una cuenta activa de <b>Azure</b> con permisos para crear y configurar recursos (por ejemplo, bases de datos y Data Factory).</li>
  <li>Un equipo local con capacidad para instalar el Self-hosted Integration Runtime (SHIR) y acceso al archivo Excel que se usará en el proyecto.</li>
</ul>

<h6>(Recordá eliminar los recursos al finalizar el proyecto para evitar gastos sopresa en tu cuenta)</h6>

---

<h3 align='left'>Instrucciones para Implementar el Proyecto:</h3>

<h4 align='left'>1. Configuración de las Bases de Datos SQL:</h4>
<p align='left'>
Crea dos bases de datos en Azure SQL.  
En cada base, crea una tabla vacía para los datos que hayas escogido, en mi caso solo usé dos columnas para algun tipo de alimento ficticio y su sabor:
</p>

```sql
-- Tabla en la Base 1
CREATE TABLE TablaBase1 (
    Tipo NVARCHAR(50),
    Sabor NVARCHAR(50)
);

-- Tabla en la Base 2
CREATE TABLE TablaBase2 (
    Tipo NVARCHAR(50),
    Sabor NVARCHAR(50)
);
```
<br> Y luego en cada base, un paso <b>super importante</b> es que le permitas acceder a ADF a tus bases, con el siguiente código (usando los nombres de tu DF), de lo contrario te dará error para conectarte a ellas: <br>

```sql
-- Crear un usuario para la identidad administrada de Azure Data Factory
CREATE USER [TuNombreDeDataFactory] FROM EXTERNAL PROVIDER;

-- Otorgar permisos de propietario (db_owner) al usuario en la base de datos
ALTER ROLE db_owner ADD MEMBER [TuNombreDeDataFactory];

-- Si deseas otorgar permisos específicos de lectura y escritura en lugar de db_owner:
-- Permisos de lectura
-- ALTER ROLE db_datareader ADD MEMBER [TuNombreDeDataFactory];

-- Permisos de escritura
-- ALTER ROLE db_datawriter ADD MEMBER [TuNombreDeDataFactory];
```


<h4 align='left'>2. Configurar Azure Data Factory:</h4><ul align='left'>

<ul><li><b>2.1 Crear Integration Runtime (SHIR):</b>

Azure Data Factory requiere un Self-hosted Integration Runtime (SHIR) para conectarse a recursos locales, como archivos en tu PC. <br> <br>Para configurarlo:

<li><b>Instalar el Integration Runtime:</b> 
<br>Descarga el SHIR desde el portal de Azure en la sección de Data Factory. Una vez descargado, instálalo en la máquina donde se encuentra el archivo Excel.</li>
<br>
<li><b>Configurar y registrar el SHIR:</b> Durante la instalación, te pedirá un token que se genera en el portal de Azure al crear el recurso de Integration Runtime. Copia y pega este token para registrar tu SHIR.</li>

<br><li><b>2.1 Crear Linked Services:</b>

Configura los servicios vinculados para conectarte al archivo Excel, la Base 1 y la Base 2.</li>
<br>
![image](https://github.com/user-attachments/assets/a57cba62-e03c-4e05-a38c-08417f79c6a7)


<li><b>2.2 Crear Datasets:</b> Definí datasets para el archivo Excel y las tablas SQL.</li> <br>

![image](https://github.com/user-attachments/assets/aaa53aa7-dae2-4594-aaee-04bf12800024)

<li><b>2.3 Crear Pipelines:</b> <ul> <br><li><b>Pipeline 1:</b> Carga los datos del archivo Excel a la tabla en la Base 1.</li>
<br>
Se hace mas llevadero, cuando imaginás el recorrido que harán tus datos, lugar 1 al lugar 2, y así mismo se configuran en la pipeline, desde un source u origen, a un destino o receptor. <br>

<h6>(Podrías dejar mucho más complejas las pipelines, insertando por ejemplo una consulta en SQL para que te filtre los datos, o usando un procedimiento almacenado entre otros, aquí estoy usando lo más simple)</h6>

![image](https://github.com/user-attachments/assets/f4bc3efe-9fb9-4410-8aab-f0eaab5a1dd0)
<br>

![image](https://github.com/user-attachments/assets/97c14b41-0a00-4586-b853-ad676fff5e69)


Aquí es importante que tengas bien configurados los accesos a tu pc, con integration services instalado y corriendo (y que tu pc no entre en modo suspensión porque se corta la conexión) <br>

<li><b>Pipeline 2:</b> Transfiere los datos desde la tabla de la Base 1 hacia la tabla en la Base 2.</li> </ul>

</li> </ul> <h4 align='left'>3. Ejecutar y Verificar:</h4> <ul align='left'>

<li>Verifica y ejecuta el <b>Pipeline 1</b> para cargar los datos del archivo Excel a la Base 1.</li>

<li>Verifica y ejecuta el <b>Pipeline 2</b> para transferir los datos de la Base 1 a la Base 2.</li>

<li>Verifica los datos finales en la tabla de la Base 2.</li> </ul>


<h3 align='left'>Diagrama del Flujo ETL:</h3> <p align='left'> <b>Flujo de trabajo:</b> </p>

[Excel Local] --> [Azure Data Factory Pipeline 1] --> [Base SQL 1] <br>
[Base SQL 1] --> [Azure Data Factory Pipeline 2] --> [Base SQL 2]


<h3 align='left'>Al terminar, los recursos creados en tu Data Factory se verán así:</h3>

<b>Captura en ADF</b>

![{14A8AEDC-649A-40C5-BE3E-65320B0FC56D}](https://github.com/user-attachments/assets/a970e94b-d39c-419e-8b7a-1527a5dbe8da)
<br>

<p align='left'> <b>Emiliano Islas</b> </p> <p align='left'> - <a href="https://www.linkedin.com/in/e-islasrivero/">LinkedIn</a> <br> - <a href="https://github.com/Emislas-bit">GitHub</a> </p>
