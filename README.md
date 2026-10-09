# Laboratorio Oracle — Actividad de Aprendizaje 1

Autor: Ricardo Ariel Anariba Armijo.

En este proyecto elaboré un modelo relacional para representar procesos de gestión académica, control de acceso, entrada de datos, reportes y estadística. El trabajo forma parte de la Actividad de Aprendizaje 1 y fue realizado con SQL Developer Data Modeler.

## Contexto del proyecto

Para desarrollar la actividad tomé como referencia mi experiencia en la Secretaría de Educación con el SACE y mi experiencia en educación superior con la Universidad Politécnica de Honduras (UPH). También utilicé documentación previa de un proyecto personal como punto de partida.

Me limité a personalizar algunos esquemas para adaptarlos al ejercicio y evitar divulgar información sobre los proyectos originales. Por ello, el modelo presentado corresponde a una adaptación académica de esa experiencia y debe interpretarse dentro de ese contexto.

## Objetivo

Organizar en un mismo diseño las entidades y relaciones de un sistema académico, integrando estructuras para administrar usuarios y permisos, registrar entradas de datos y servir de base para reportes y estadísticas.

El esquema unificado contiene 34 tablas, 220 campos y 46 relaciones mediante claves foráneas. Las tablas pertenecen al esquema `RAANARIBA` y utilizan el sufijo `_raanariba` como parte de la personalización del ejercicio.

## Estructura del modelo

### Gestión académica

El modelo incluye personas, alumnos, docentes, carreras, mallas curriculares, asignaturas, períodos académicos, secciones, aulas, horarios y matrículas.

Los datos personales se concentran en `persona_raanariba`, mientras que los perfiles de alumno y docente se mantienen en tablas relacionadas. Esto permite representar a una persona que tenga ambos perfiles. También se contemplan distintas versiones de una malla curricular, asignaturas compartidas entre planes y la asignación de varios docentes a una sección.

### Control de acceso basado en roles (RBAC)

Integré un modelo RBAC para representar la asignación de roles a los usuarios y de permisos a los roles. Sus tablas principales son `usuarios_raanariba`, `roles_raanariba`, `permisos_raanariba`, `usuarios_roles_raanariba` y `roles_permisos_raanariba`. El diseño también contempla permisos específicos por usuario mediante `usuarios_permisos_raanariba`.

Los roles académicos de una persona, como alumno o docente, se modelan por separado de los roles que determinan el acceso al sistema.

### Entrada de datos, reportes y estadística

Para esta parte utilicé una estructura referencial de Data Entry, entendida en el ejercicio como el registro y la validación de entradas de datos. Las tablas `cargas_entrada_raanariba` y `validaciones_entrada_raanariba` permiten representar las cargas, sus resultados de procesamiento y los errores encontrados.

La estructura de reportes contempla definiciones, ejecuciones, indicadores y resultados estadísticos. El diseño relaciona los reportes con los datos académicos aceptados y permite asociar una ejecución a una carga de entrada. Los resultados incluyen el período académico y la asignatura dentro de una malla curricular; además, se consideran numeradores y denominadores para los indicadores que requieren calcular tasas o porcentajes.

### Sesiones y auditoría

Incluí estructuras para sesiones, eventos de auditoría, bitácoras de operaciones, registros del sistema y seguimiento de eliminaciones. Estas tablas permiten modelar la trazabilidad de las acciones realizadas por los usuarios.

## Tecnología y versiones utilizadas

La herramienta principal fue **Oracle SQL Developer Data Modeler**, una aplicación de escritorio para diseñar bases de datos. Permite definir tablas, columnas, claves y relaciones, visualizar su estructura y generar instrucciones SQL de definición de datos (DDL). En esta actividad la utilicé para trabajar con el modelo relacional y preparar su representación gráfica. Estas capacidades se describen en las [notas oficiales de Data Modeler 24.3.1](https://www.oracle.com/tools/datamodeler/datamodeler-relnotes-24.3.1.html).

La instalación utilizada está en la siguiente ubicación de mi equipo:

```text
C:\Users\ricardo\Desktop\PROYECTO\datamodeler
```

Las versiones se verificaron en los archivos de esa instalación:

| Tecnología o componente | Versión comprobada | Función en el entorno |
| --- | --- | --- |
| Oracle SQL Developer Data Modeler | **24.3.1.351.0831**; versión 24.3.1 y compilación 351.0831 | Herramienta para editar el diseño y visualizar el diagrama. La versión aparece en `datamodeler\bin\version.properties` y en el registro `datamodeler\log\datamodeler.log`. |
| Java incluido con la herramienta | **Oracle Java SE 17.0.13 LTS**, compilación `17.0.13+4-LTS-259`, de 64 bits | Entorno que ejecuta Data Modeler. Se verificó en `jdk\jre\release` y mediante `jdk\jre\bin\java.exe -version`. |
| Controlador Oracle JDBC incluido | **23.5.0.24.07**, especificación JDBC 4.3 | Componente disponible para conexiones a bases de datos Oracle. La versión se verificó en `META-INF/MANIFEST.MF`, dentro de `jdbc\lib\ojdbc11.jar`; su presencia no acredita una conexión usada para elaborar el diagrama. |
| Formato del diseño de Data Modeler | **3.5**, según el atributo `version` del archivo `.dmd` | Formato XML de almacenamiento del proyecto. Este número identifica el formato del archivo y es independiente de la versión 24.3.1 de la aplicación. |

El trabajo se realizó en **Windows**. El diseño utiliza tipos de datos orientados a Oracle, como `NUMBER`, `VARCHAR2` y `DATE`. La versión de un servidor **Oracle Database** queda sin especificar, porque los archivos entregados documentan el modelo y sus diagramas, sin identificar una instancia de base de datos desplegada. La versión del controlador JDBC tampoco identifica la versión de un servidor.

El enfoque utilizado fue el **modelado relacional**: cada tabla representa un conjunto de registros, sus columnas describen los datos y las claves establecen su identidad y sus vínculos. **RBAC** es el enfoque para organizar roles y permisos; **Data Entry** describe el proceso de recepción y validación de datos que se representa en el modelo.

## Cómo se elaboraron los diagramas en Data Modeler

La herramienta nueva para mí fue SQL Developer Data Modeler. Parte del trabajo consistió en familiarizarme con su manejo, organizar el esquema unificado y preparar los archivos del modelo y las exportaciones del diagrama.

Los archivos PDF, PNG y SVG muestran el mismo modelo **RAANARIBA - Esquema unificado**. El siguiente recorrido explica cómo se estructuró el diseño y cómo reproducir su edición desde la interfaz de Data Modeler.

1. **Analizar y organizar la información.** A partir de la documentación previa y de los procesos del ejercicio, identifiqué los grupos de información: gestión académica, usuarios y permisos, cargas de entrada, reportes, estadística y auditoría. Separé los datos personales en `persona_raanariba` y los perfiles de alumno y docente en sus respectivas tablas para evitar repetir información personal.

2. **Preparar el diseño relacional.** El proyecto se guardó como `RAANARIBA_Unificado`, con el modelo relacional **RAANARIBA - Esquema unificado**. Para iniciar un diseño equivalente se utiliza **File > New** y se trabaja en **Relational Models**, dentro del panel **Browser**. Para continuar este proyecto se abre `RAANARIBA_Unificado.dmd` con **File > Open**, manteniendo junto a él la carpeta del mismo nombre. Las tablas se asociaron al esquema `RAANARIBA` y se personalizaron con el sufijo `_raanariba`.

3. **Definir las tablas y sus campos.** Se especificaron el nombre, las columnas y la función de cada tabla. En la interfaz, **New Table** permite agregar una tabla al lienzo; sus propiedades permiten editar las columnas, el tipo de dato, la longitud o precisión y la admisión de valores nulos. Por ejemplo, `persona_raanariba` contiene `persona_id`, `numero_documento`, `nombre_completo`, `fecha_nacimiento` y campos de contacto.

4. **Establecer las claves.** Cada tabla tiene una clave primaria (**PK**) que identifica sus registros. Las claves únicas (**UK**) expresan restricciones adicionales: por ejemplo, la combinación de `usuarios_id` y `roles_id` es única en `usuarios_roles_raanariba`, para evitar repetir la misma asignación. Las claves foráneas (**FK**) vinculan las columnas de una tabla con una clave de otra. Estas definiciones se revisan en las propiedades de la tabla.

5. **Construir las relaciones.** Las relaciones del diagrama corresponden a las FK guardadas en el modelo. Por ejemplo, `mallas_curriculares_raanariba.carreras_id` referencia a `carreras_raanariba.carreras_id`: una carrera puede tener varias mallas y cada malla pertenece a una carrera. Las relaciones de muchos a muchos se resolvieron con tablas intermedias, como `usuarios_roles_raanariba`, `roles_permisos_raanariba` y `mallas_asignaturas_raanariba`. Al editar una FK se revisan la tabla referenciada y la correspondencia de columnas.

6. **Definir la participación obligatoria u opcional.** Una FK obligatoria exige que exista el registro relacionado; una FK que admite nulos permite omitir ese vínculo. Por ejemplo, `carreras_id` es obligatorio en una malla curricular, mientras que `cargas_entrada_id` es opcional en una matrícula, porque esta también puede registrarse por captura directa. Las restricciones únicas sobre FK permiten representar vínculos de uno a uno, como el perfil de alumno asociado a una persona.

7. **Organizar y revisar el lienzo.** Las tablas se distribuyeron en una vista unificada para consultar los distintos procesos y sus conexiones. En Data Modeler se pueden mover y ajustar los cuadros para facilitar la lectura de nombres, campos y claves. La distribución se conserva en los archivos de la vista del diagrama. El inventario complementa la revisión con las **34 tablas, 220 campos y 46 relaciones** del proyecto.

8. **Guardar y preparar las representaciones del diagrama.** El diseño editable se conserva mediante **File > Save**, en el archivo `.dmd` y su carpeta complementaria. Para obtener imágenes del modelo se utiliza **File > Print Diagram**, seleccionando PNG o SVG; SVG permite ampliar el diagrama conservando la nitidez. El PDF incluido permite consultar el esquema como documento. Para reproducir una salida PDF en esta versión puede utilizarse **File > Print** con una impresora PDF disponible en Windows, como **Microsoft Print to PDF**: las [notas de la versión 24.3.1](https://www.oracle.com/tools/datamodeler/datamodeler-relnotes-24.3.1.html) indican que la generación directa de PDF dejó de estar soportada.

Las opciones de apertura, visualización y exportación se pueden consultar en la [guía de uso de Data Modeler 24.3](https://docs.oracle.com/en/database/oracle/sql-developer-data-modeler/24.3/dmdug/data-modeler-concepts-usage.html).

### Tipos de datos representados

| Tipo de Oracle | Uso en el diseño | Ejemplo o estado |
| --- | --- | --- |
| `NUMBER` | Identificadores, cantidades y valores numéricos. | `persona_id` está definido con precisión 12: `NUMBER(12)`. |
| `VARCHAR2` | Textos de longitud variable. | `nombre_completo` está definido como `VARCHAR2(200 BYTE)`. |
| `DATE` | Fechas, como nacimiento y vigencia de planes. | `fecha_nacimiento` en `persona_raanariba`. |
| `TIMESTAMP(6) WITH TIME ZONE` | Instantes de eventos, sesiones y operaciones con zona horaria. | El tipo requerido se documenta en comentarios de los campos correspondientes. |
| `CLOB` | Textos extensos, como detalles técnicos o valores de auditoría. | El tipo requerido se documenta en comentarios de los campos correspondientes. |

En el archivo actual hay **21 columnas pendientes de asignación nativa del tipo de dato**, correspondientes a `TIMESTAMP(6) WITH TIME ZONE` y `CLOB`. Sus comentarios conservan el tipo previsto y en la exportación aparecen como `UNKNOWN`. Para generar un DDL completo, estas columnas deben recibir su tipo en las propiedades de Data Modeler.

### Lectura del diagrama y notación

Cada cuadro representa una tabla y muestra sus campos y claves; los enlaces representan las referencias entre tablas. Para interpretar la cardinalidad se revisan la FK, su obligatoriedad y las restricciones únicas: una FK sin unicidad permite varios registros asociados, mientras que una FK única limita esa asociación a un registro.

La notación **Barker** sirve como referencia para explicar cardinalidades y participación obligatoria u opcional. Data Modeler permite configurarla para el **modelo lógico** mediante **View > Logical Diagram Notation**, según la [guía de la herramienta](https://docs.oracle.com/en/database/oracle/sql-developer-data-modeler/24.3/dmdug/data-modeler-concepts-usage.html). El entregable de esta actividad es el **diagrama relacional**, cuya estructura se documenta mediante tablas, PK, UK y FK.

## Archivos del proyecto

| Archivo o carpeta | Contenido |
| --- | --- |
| [RAANARIBA_Unificado.dmd](RAANARIBA_Unificado.dmd) | Archivo principal del diseño para abrirlo en SQL Developer Data Modeler. |
| [RAANARIBA_Unificado/](RAANARIBA_Unificado/) | Archivos complementarios del modelo, incluidas las tablas, columnas, claves y relaciones. |
| [RAANARIBA_Unificado.zip](RAANARIBA_Unificado.zip) | Archivo comprimido del proyecto de modelado. |
| [RAANARIBA - Esquema unificado.pdf](RAANARIBA%20-%20Esquema%20unificado.pdf) | Diagrama exportado en formato PDF. |
| [RAANARIBA - Esquema unificado.png](RAANARIBA%20-%20Esquema%20unificado.png) | Imagen del diagrama. |
| [RAANARIBA - Esquema unificado.svg](RAANARIBA%20-%20Esquema%20unificado.svg) | Versión vectorial del diagrama para consultar con ampliación. |
| [Inventario_Tablas_Campos_Relaciones.xlsx](Inventario_Tablas_Campos_Relaciones.xlsx) | Inventario con hojas de tablas, campos, relaciones y claves. |
| [Actividad de Aprendizaje 1 .pdf](Actividad%20de%20Aprendizaje%201%20.pdf) | Documento de la actividad. |

## Cómo consultar el proyecto

1. Descargar el archivo `RAANARIBA_Unificado.dmd` y la carpeta `RAANARIBA_Unificado/`, conservando ambos en la misma ubicación.
2. Abrir SQL Developer Data Modeler y seleccionar el archivo `.dmd` desde la opción de abrir un diseño.
3. Consultar el modelo relacional **RAANARIBA - Esquema unificado** para revisar las tablas y sus relaciones.
4. Utilizar el inventario de Excel para consultar los campos y las claves. Las exportaciones en PDF, PNG y SVG permiten revisar el diagrama sin abrir la herramienta de modelado.

### Vista del esquema unificado

![Diagrama del modelo relacional RAANARIBA — Esquema unificado](RAANARIBA%20-%20Esquema%20unificado.png)

## Tiempo dedicado y aprendizaje

El ejercicio me tomó aproximadamente cinco días, dedicando alrededor de dos horas diarias, para un total estimado de diez horas. Para realizarlo aproveché la documentación previa de mi proyecto personal; este tiempo corresponde al desarrollo de la actividad y al aprendizaje de la herramienta.

La actividad me permitió trasladar parte de mi experiencia en sistemas educativos a un modelo relacional, integrar los esquemas académicos con RBAC y con la estructura de Data Entry para reportes y estadística, y aprender a trabajar con SQL Developer Data Modeler.
