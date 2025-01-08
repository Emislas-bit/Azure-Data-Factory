<h1 align='left'>Azure Data Factory ETL Project</h1>

<p align='left'>
Este repositorio contiene un proyecto desarrollado con <b>Azure Data Factory</b> que demuestra un flujo ETL completo, desde la carga de un archivo Excel local hasta la transferencia de datos entre dos bases de datos SQL en Azure. Este proyecto se centra en el uso de pipelines, datasets, linked services y un Self-hosted Integration Runtime (SHIR) para conectar recursos locales con la nube.
</p>

---

<h3 align='left'>Descripción del Proyecto:</h3>
<p align='left'>
El proyecto consiste en:  
</p>
<ul align='left'>
  <li><b>Carga de un archivo Excel desde un entorno local</b> a una tabla en la primera base de datos SQL.</li>
  <li><b>Transformación y transferencia de datos</b> desde la primera base de datos SQL hacia una tabla en la segunda base de datos SQL.</li>
  <li><b>Automatización del flujo ETL</b> utilizando Azure Data Factory y recursos de integración.</li>
</ul>

<p align='left'>
El objetivo principal es demostrar las capacidades de Azure Data Factory para integrar datos locales y en la nube mediante procesos automatizados, seguros y eficientes.
</p>

---

<h3 align='left'>Requisitos Previos:</h3>
<ul align='left'>
  <li>Una cuenta de <b>Azure</b> activa.</li>
  <li><b>Azure Data Factory</b> configurado.</li>
  <li><b>Self-hosted Integration Runtime (SHIR)</b> instalado para acceder a recursos locales.</li>
  <li>Dos bases de datos en <b>Azure SQL Database</b> con tablas vacías creadas.</li>
  <li>Un archivo Excel local con datos (por ejemplo, <i>example.xlsx</i>).</li>
</ul>

---

<h3 align='left'>Instrucciones para Implementar el Proyecto:</h3>

<h4 align='left'>1. Configuración de las Bases de Datos SQL:</h4>
<p align='left'>
Crea dos bases de datos en Azure SQL.  
En cada base, crea una tabla vacía para los datos:
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

<h4 align='left'>2. Configurar Azure Data Factory:</h4><ul align='left'>

<li><b>2.1 Crear Linked Services:</b>

Configura los servicios vinculados para conectarte al archivo Excel, la Base 1 y la Base 2.</li>

<li><b>2.2 Crear Datasets:</b> Define datasets para el archivo Excel y las tablas SQL.</li>

<li><b>2.3 Crear Pipelines:</b> <ul> <li><b>Pipeline 1:</b> Carga los datos del archivo Excel a la tabla en la Base 1.</li>

<li><b>Pipeline 2:</b> Transfiere los datos desde la tabla de la Base 1 hacia la tabla en la Base 2.</li> </ul>

</li> </ul> <h4 align='left'>3. Ejecutar y Verificar:</h4> <ul align='left'>

<li>Ejecuta el <b>Pipeline 1</b> para cargar los datos del archivo Excel a la Base 1.</li>

<li>Ejecuta el <b>Pipeline 2</b> para transferir los datos de la Base 1 a la Base 2.</li>

<li>Verifica los datos finales en la tabla de la Base 2.</li> </ul>


<h3 align='left'>Diagrama del Flujo ETL:</h3> <p align='left'> <b>Flujo de trabajo:</b> </p>

[Excel Local] --> [Azure Data Factory Pipeline 1] --> [Base SQL 1] <br>
[Base SQL 1] --> [Azure Data Factory Pipeline 2] --> [Base SQL 2]


<h3 align='left'>Todo armado en el menu de ADF:</h3>

<b>Captura en ADF</b>

![{14A8AEDC-649A-40C5-BE3E-65320B0FC56D}](https://github.com/user-attachments/assets/a970e94b-d39c-419e-8b7a-1527a5dbe8da)
<br>

<h3 align='left'>Licencia:</h3> <p align='left'> Este proyecto está licenciado bajo la <b>MIT License</b>. Puedes usarlo y modificarlo libremente, siempre y cuando menciones al autor. </p>

<h3 align='left'>Autor:</h3> <p align='left'> Creado por: <b>Emiliano Islas</b> </p> <p align='left'> - <a href="https://www.linkedin.com/in/e-islasrivero/">LinkedIn</a> <br> - <a href="https://github.com">GitHub</a> </p>
