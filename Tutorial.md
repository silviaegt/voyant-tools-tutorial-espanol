# Análisis de corpus con Voyant Tools


El análisis de corpus es un tipo de [análisis de contenido](http://vocabularios.caicyt.gov.ar/portal/index.php?task=fetchTerm&arg=26&v=42), que permite hacer comparaciones a gran escala entre los textos contenidos en dichos corpus.

Desde el inicio de la computación, lingüistas y especialistas de la [recuperación de la información](http://vocabularios.caicyt.gov.ar/portal/?task=fetchTerm&arg=178&v=42) han creado y utilizado software para apreciar los patrones que no son evidentes en la lectura; o bien, para corroborar hipótesis que intuían al leer ciertos textos. Por ejemplo: los patrones de uso y decaimiento de ciertos términos en una época dada, los contextos izquierdos y derechos de palabras específicas, o las expresiones que distinguen a un grupo de textos frente a otros.

Voyant Tools (Sinclair y Rockwell, 2016) es una herramienta basada en Web que permite hacer este tipo de análisis y que no requiere de la instalación de ningún tipo de software especializado pues funciona en cualquier equipo con conexión a internet. 

Es una buena puerta de entrada para inciarse en el análisis cuantitativo de textos y es por eso que se ha integrado a la lista de tutoriales de The Programming Historian en esta rama.

Al finalizar este tutorial, tendrás la capacidad de:

* Armar un corpus en texto plano
* Pensar y aplicar diferentes técnicas de segmentación de corpus
* Identificar características básicas del corpus:
	* Extensión de los documentos subidos a la plataforma
	* Densidad léxica (llamada "densidad de vocabulario" en Voyant)
	* Promedio de palabras por oración
	* Relevancia (llamadas "palabras distintivas")
	* Leer diferentes estadísticas sobre los vocablos (frecuencia absoluta y relativa, tendencia y asimetría estadística)
* Realizar consultas específicas sobre el corpus:
	*  Buscar palabras clave en contexto
	* Identificar patrones de uso de un término

* Exportar los datos y las visualizaciones en diferentes formatos (csv, png, html)

## Creando un corpus en texto plano

Si bien VoyantTools puede trabajar con muchos tipos de formato (HTML, XML, PDF, RTF, y MS Word); en este tutorial utilizaramos sólo texto plano. El texto plano tiene tres ventajas fundamentales: no tiene ningún tipo de formato adicional, no requiere un programa especial ni conocimiento extra a las habilidades básicas de cómputo (abrir archivos, copiar y pegar, "guardar como").

### 1. Buscar textos

Para armar un corpus lo primero que debes hacer es buscar la información que te interesa. Para este tutorial, [Riva Quiroga](https://twitter.com/rivaquiroga) y yo preparamos un corpus de los discursos presidenciales anuales de Argentina, Chile, Colombia, México y Perú (este último gracias a [Pamela Sertzen](https://twitter.com/madvivacious)) entre 2006 y 2010, es decir dos años antes y después de la crisis económica de 2008. Lo único que hicimos fue buscar en Google 

### 2. Copiar en editor de texto plano
Una vez localizada la información, el segundo paso es copiar el texto que te interesa desde la primera palabra dicha hasta la última y guardarla en un editor de texto sin formato. Por ejemplo:
* en Windows podría guardarse en [Bloc de Notas](https://web.archive.org/web/20091013225307/http://windows.microsoft.com/en-us/windows-vista/Notepad-frequently-asked-questions)
* en Mac, en [TextEdit](https://support.apple.com/es-mx/guide/textedit/welcome/mac); 
* y en Linux, en [Gedit](https://wiki.gnome.org/Apps/Gedit).

### 3. Guardar archivo

Cuando guardes el texto debes considerar tres cosas esenciales:

La primera es que, si los textos de tu corpus están en español, deberás **guardarlos en UTF-8**, que es un formato de codificación de caracteres estándar para este idioma. 

(gif de cómo guardar)

> **¿Qué es utf-8?** Si bien en nuestra pantalla vemos que al teclear una "É" aprece una "É"; para una computadora "É" es una serie de ceros y unos que son interpretados en imagen dependiendo del "traductor" o "codificador" que se esté usando. El codificador que contiene códigos binarios para todas los caracteres que se usan en el español es UTF-8. Siguiendo con el ejemplo "11000011", es una cadena de ocho bits --es decir, **ocho** espacios de información-- que en UTF-**8** son interpretados como "É"

La segunda es que **el nombre de tu archivo no debe contener acentos ni espacios**, esto asegurará que pueda ser abierto en otros sistemas operativos

> **¿Por qué evitar acentos y espacios en los nombres de archivo?** Por razones similares a el inciso anterior, un archivo que se llame Ébano.txt no siempre será entendido de forma correcta por todos los sistemas operativos pues varios tienen otro codificador por defecto. Muchos usan ASCII, por ejemplo, que sólo tiene siete bits de manera que el último bit (1) de "11000011" es interpretado como el inicio del siguiente caracter y se descuadra la interpretación.

La tercera es que es una buena práctica integrar ciertos metadatos de contexto (v.g. fecha, género, autor, origen) en el nombre del archivo que te permitan partir tu corpus según diferentes criterios y también leer mejor los resultados. Para este tutorial hemos nombrado los archivos con el año del discurso presidencial, el 
código del país ([ISO 3166-1 alfa-2](https://www.iso.org/obp/ui/#search)) y el apellido de quien profirió el disurso. 

> [2007_mx_calderon.txt](https://github.com/corpusenespanol/discursos-presidenciales/blob/master/mexico/2007_mx_calderon.txt "2007_mx_calderon.txt") tiene el año del discurso dividido con un guión bajo, el código de dos letras del país (México = mx) y el apellido del presidente que dictó el discurso, Calderón, (sin acentos ni eñes) 

## Cargar el corpus


En la página de entrada de Voyant Tools encontrarás cuatro opciones sencillas para cargar textos.<sup>1</sup> Las dos primeras opciones son en el cuadro blanco. En este cuadro puedes pegar directamente un texto que hayas copiado de algún lugar; o bien, pegar la(s) dirección(es) web --separadas por comas-- de los sitios en donde se encuentren los textos que quieres analizar. 
Una tercera opción es "Abrir" alguno de los dos corpus que Voyant tiene precargados (las obras de Shakespeare o las novelas de Austen: ambos en inglés).

Por último, está la opción que usaremos en este tutorial, en la que puedes cargar directamente los documentos que tengas en tu computadora. En este caso subiremos el [corpus completo](https://github.com/corpusenespanol/discursos-presidenciales/tree/master/corpus-completo) de discursos presidenciales. 

>  **Para obtener los materiales** de este tutorial ve [a esta página de Github](https://github.com/corpusenespanol/discursos-presidenciales/tree/master/corpus-completo)  y descarga todos los archivos:

![Descargar corpus](img/1_descargar_archivos.png)

>  **Para descomprimir en Windows** haz clic derecho en el  archivo comprimido (.**ZIP**). En el menú desplegable, selecciona **7-zip**  y haz clic en "Extraer aquí"
>    **Para descomprimir en Mac** da doble clic sobre el archivo comprimido
>    **Para descomprimir en Linux** botón derecho + "Extraer aquí"


Para cargar los materiales pulsas sobre el icono que dice cargar, abres tu explorador de archivos y, dejando presionada la tecla 'Shift' seleccionas todos los archivos que vas a usar. Para esta primera parte del tutorial subiremos todos los archivos de la carpeta ["corpus completo"](https://github.com/corpusenespanol/discursos-presidenciales/tree/master/corpus-completo)

![Cargar documentos](img/cargar.png)




## Explorando el corpus


Una vez cargados todos los archivos llegará a la 'interfaz' ('skin') que tiene cinco herramientas por defecto.
1. Cirrus: tipo de nube de palabras que muestra los términos más frecuentes
![Cirrus](img/cirrus.png)

2. Lector: espacio para la revisión y lectura de los textos completos con una gráfica de barras que indica la cantidad de texto que tiene cada documento

![Lector](img/lector.png)

3. Tendencias: gráfico de distribución que muestra los términos en todo el corpus (o dentro de un documento cuando sólo se carga uno)

![Lector](img/tendencias.png)

4. Sumario: proporciona una visión general de ciertas estadísticas textuales del corpus actual
![Resumen](img/sumario.png)

5. Contextos: concordancia que muestra cada ocurrencia de una palabra clave con un poco de contexto circundante
![Contextos](img/contextos.png)

### Sumario de los documentos 

Una de las ventanas más informativas de Voyant es la del sumario. Aquí obtenemos una vista de pájaro sobre algunas estadísticas de nuestro corpus por lo que funciona como un buen punto de partida.

#### Número de textos, palabras y palabras únicas
La primera frase que leemos se ve algo como esto: 
>Este corpus tiene 25 documentos con 261,032  total de palabras y 18,550 formulario de palabra única. Creado  hace 8 horas atrás [el texto es producto de una traducción semi-automática del inglés y por eso se lee raro]

De entrada con esta información sabemos exactamente cuántos documentos distintos fueron cargados (25); cuántas palabras en total hay (261,032); y cuántas palabras distintas y únicas existen (18,550).

#### :pencil2: *Actividad 1*
Si nuestro corpus estuviera compuesto de dos documentos; uno que dijera: "tengo hambre"; y otro que dijera: "tengo sueño". ¿Qué información aparecería en la primera línea del sumario? 
Este corpus tiene ____ documentos con un total de palabras de ____ y ____ palabras únicas.

#### Extensión de documentos
Lo segundo que vemos es la sección de "extensión del documento". Ahí aparece lo siguiente:

-   Más largo:  [2008_cl_bachelet](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (20702);  [2007_ar_kircher](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (20390);  [2006_ar_kircher](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (18619);  [2010_cl_pinera](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (16982);  [2007_cl_bachelet](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (15514)
-   Más corto:  [2006_pe_toledo](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (1289);  [2006_mx_fox](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (2450);  [2008_mx_calderon](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (3317);  [2006_co_uribe](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (4709);  [2009_co_uribe](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (5807)

#### :pencil2: *Actividad 2*
1. ¿Qué podemos concluir sobre los textos más largos y los más cortos considerando los metadatos del título?
2. ¿Para qué nos servirá saber la longitud de los textos?


#### Densidad del vocabulario

La densidad de vocubulario se mide dividiendo el número de palabras distintas entre el número de palabras totales. Entre más cercano a uno es el índice de densidad quiere decir que el vocabulario es más denso.

#### :pencil2: *Actividad 3*

1. Calcula la densidad de las siguientes estrofas, compara y comenta:

* Estrofa 1.
>¿Qué humor puede ser más raro 
que el que, falto de consejo, 
él mismo empaña el espejo,
y siente que no esté claro?

* Estrofa 2.
>Pasito a pasito, suave suavecito  
Nos vamos pegando poquito a poquito  
Cuando tú me besas con esa destreza  
Veo que eres malicia con delicadeza

2. Lee los datos densidad léxica de los documentos de nuestro corpus, ¿qué te dicen?
-   Más alto:  [2006_pe_toledo](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.404);  [2006_co_uribe](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.340);  [2009_co_uribe](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.336);  [2008_co_uribe](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.334);  [2006_mx_fox](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.328)
-   Más bajo:  [2008_cl_bachelet](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.192);  [2007_mx_calderon](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.192);  [2007_ar_kircher](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.206);  [2007_pe_garcia](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.214);  [2010_ar_fernandez](https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&panels=cirrus,reader,trends,summary,contexts#) (0.217)
3. Compáralos con la información sobre su extensión, ¿qué notas?

#### Palabras por oración

La forma en Voyant calcula la longitud de las oraciones debe considerarse muy aproximada, especialmente por lo complicado que es distinguir entre el final de una abreviatura y el de una oración y otros usos de la puntuación (por ejemplo, en algunos casos un punto y coma marca el límite entre oraciones y en otros . El análisis de las oraciones es realizado por una 'clase' del lenguaje de programación Java (es decir, una plantilla con instrucciones) que se llama [BreakIterator](https://docs.oracle.com/javase/tutorial/i18n/text/about.html).

#### :pencil2: *Actividad 4*
1. Observa las estadísticas de palabras por oración (ppo) y contesta: ¿qué patrón o patrones puedes observar si consideras el índice de ppo y los metadatos de país, presidente y año contenidos en el nombre del documento?
2. Da clic sobre los nombre de algunos documentos que te interesen por su índice de ppo. Dirige tu mirada a la ventana de "Lector" y lee algunas líneas, ¿leer el texto original agrega información nueva a tu lectura de los datos? Comenta por qué.

#### Palabras más frecuentes y palabras diferenciadas
(volveremos a este inciso en la siguiente sección)

### Términos frecuentes 

Ya que tenemos una idea de algunas características globales de nuestros documentos, es momento de que empecemos con las características de los conceptos en nuestro corpus. El primer aspecto con el que vamos a trabajar es con el de **frecuencia** y para esto utilizaremos la ventana de Cirrus. 

#### :pencil2: *Actividad 5*
a) ¿Qué palabras son las más frecuente en el corpus?
b) ¿Qué nos dicen estas palabras del corpus?, ¿son significativas todas?

>    **Tip** pasa el mouse sobre las palabras para obtener sus frecuencias derecho

La importancia no es un valor intrínseco y dependerá siempre de nuestros intereses. Justo por eso Voyant ofrece la opción de filtrar ciertas palabras. Un procedimiento común para obtener palabras relevantes es el de filtrar las unidades léxicas gramaticales o _palabras vacías_: artículos, preposiciones, interjecciones, pronombres, etc. (Peña y Peña, 2015)-

#### :pencil2: *Actividad 6*
a) ¿Qué palabras vacías están en la nube de palabras?
b) ¿Cuáles eliminarías y por qué?

Voyant tiene ya cargada una lista de _stop words_ o palabras vacías; no obstante, nosotros podemos editarla de la siguiente manera:
Colocamos nuestro cursor enor superior derecha de la ventana de Cirrus. Y damos clic sobre el icono que parece un interruptor. 

![Abrir opciones](img/editar_lista.png)

Aparecerá una ventana con diferentes opciones, seleccionamos la primera "Editar lista"

![Editar lista](img/editarlista.png)

Agregamos las palabras “vacías”, siempre separadas por un salto de línea (tecla enter)

![Editar palabras vacías](img/lista_ruido.png)

Una vez que hayamos añadido las palabras que deseamos filtrar damos clic en "salvar". 
  
>    **Ojo** por defecto está seleccionado una caja que dice "Aplicar a todo"; si ésta se deja seleccionada el filtrado afectará las métricas de todas las otras herramienta. Es muy importante que documentes tus decisiones. Una buena práctica es guardar la lista de palabras vacías en un archivo de texto (.txt) Para este tutorial hemos creado una lista de palabras para filtrar y la puedes usar si así lo quieres, sólo recuerda que esto afectará tus resultados. Por ejemplo: en la lista de palabras filtradas incluí "todas" y "todos", habrá personas para las que estas palabras podrían ser interesantes dado que muestran que "todos" es mucho más utilizado que "todas" y esto podría darnos pistas sobre el uso de lenguaje incluyente.

#### Palabras más frecuentes

Volvamos entonces a esta sección del sumario. Como dijimos en el iniciso anterior las palabras filtradas afectan otros campos de Voyant. En este caso, si dejasta seleccionada la caja de "Aplicar a todo"  la lista debajo de la leyenda: **Palabra más frecuente en el corpus** , mostrará las palabras que se repiten más **sin contar** aquéllas que fueron filtradas. En mi caso, muestra:

>[social](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (437); [nacional](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (427); [nuestro](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (393); [inversión](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (376); [ley](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (369)

#### :pencil2: *Actividad 7*

1. Reflexiona sobre estas palabras y piensa qué información te proporcionan y cómo se distingue esta información de la que obtienes viendo la nube de palabras. 
2. Si estás en un grupo discute las diferencias de tus resultados con los de los demás

#### Frecuencia Normalizada

En el apartado anterior hemos observado la "frecuencia bruta" de las palabras. 
Ahora, si tuviéramos un corpus de seis palabras y otro de 3,000 palabras, las frecuencias brutas son poco informativas. Tres palabras en un corpus de seis palabras representa 50% del total, tres palabras en un corpus de 6,000 representan el 0.1% del total. 
Para evitar la sobre-representación de un término, los lingüistas han ideado otra medida que se llama: "frecuencia relativa normalizada".
Ésta se calcula de la siguiente manera:
Frecuencia Bruta * 1,000,000 / Número total de palabras.
Analicemos un verso como ejemplo. Tomemos la frase: "pero mi corazón dice que no, dice que no", que tiene ocho palabras en total. Si calculamos su frecuencia bruta y relativa tenemos que:
|palabra|frecuencia bruta  |frecuencia normalizada|
|--|--|--|
| corazón | 1 |1*1,000,000/8 = 125,000|
| dice| 2 |2*1,000,000/8 = 111,000|

¿Cuál es la ventaja de esto? Que si tuviéramos un corpus en el que la palabra corazón tuviera la misma proporción, por ejemplo 1,000 ocurrencias entre 8,000 palabras; si bien la frecuencia bruta es muy distinta, la frecuencia normalizada sería la misma, pues 1,000*1,000,000/8,000 también es 125,000.

Veamos cómo funciona esto en Voyant Tools:
1. En la sección de Cirrus (la nube de palabras), damos clic sobre 'Terms' o 'Términos'. Esto abrirá una tabla que por defecto tiene tres columnas: Términos (con la lista de palabras en los documentos, sin las filtradas), Contar (con la 'frecuencia bruta o neta' de cada término) y Tendencia (con una gráfica de la distribución de una palabra tomando su frecuencia relativa). Para obtener información sobre la frecuencia relativa de un término, en la barra de los nombres de columna, en el extremo derecho, se da clic sobre el triángulo que ofrece más opciones y en 'Columnas' se selecciona la opción 'Relativo' como se muestra en la imagen a continuación:
![Editar palabras vacías](img/frecuencia_relativa.png)

2. Si ordenas las columnas en orden descendiente como lo harías en Excel, observarás que el orden de la frecuencia bruta ('Contar') y la frecuencia relativa ('Relativo') el orden es el mismo. ¿Para qué nos sirve entonces esta medida? Para cuando comparamos diferentes corpus. Un corpus es un conjunto de textos con algo en común. En este caso, Voyant está interpretando todos los discursos como un solo corpus. Si quisiéramos que cada cada país fuera un corpus distinto, tendríamos que guardar nuestro texto en una tabla, en HTML o en XML, donde los metadatos estuvieran expresados en columnas (en el caso de la tabla) o en etiquetas (en el caso de HTML o XML). Para más información, consulta la documentación en inglés.<sup>1</sup>

#### Palabras diferenciadas

Como tal vez ya sospechas, la información más interesante generalmente no se encuentra dentro de las palabras más frecuentes, pues éstas tienden a ser también las más evidentes. En el campo de la recuperación de la información se han inventado otras medidas que permiten ubicar los términos que hacen que un documento se distinga de otro. Una de las medidas más usadas se llama tf-idf (term frequency, inverse document frequency); la cual busca expresar numéricamente qué tan relevante es un documento en una colección determinada.

En Voyant el tfidf se calcula [de la siguiente manera](https://twitter.com/VoyantTools/status/1025458748574326784): 

Frecuencia Bruta  (tf) / Número de Palabras (N)  * log10( Total número de Documentos / termInDocsCount

![Fórmula de TF-IDF](img/tf_idf.png)

#### :pencil2: *Actividad 8*

Observa las **palabras diferenciadas  (comparado con el resto del corpus)** de cada uno de los documentos y anota qué hipótesis puedes derivar de ellas 

1.  [2006_ar_kircher](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [uruguay](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (12),  [2004](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (13),  [2005](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (31),  [plata](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (7),  [inclusión](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (16).
2.  [2006_cl_bachelet](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [innovación](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (15),  [rodrigo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (8),  [alegremente](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4),  [barrios](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (9),  [cobre](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (10).
3.  [2006_co_uribe](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [tutela](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [reelección](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [regalías](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (7),  [iva](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [publicación](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5).
4.  [2006_mx_fox](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [atenta](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [apego](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [federalismo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (3),  [intransigencia](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (2),  [fundamento](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (3).
5.  [2006_pe_toledo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [entrego](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [señor](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (14),  [señora](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [amigo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [tracemos](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (2).
6.  [2007_ar_kircher](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [2006](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (65),  [mercosur](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (12),  [uruguay](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (9),  [provincias](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (16),  [interanual](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5).
7.  [2007_cl_bachelet](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [macrozona](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (7),  [deudores](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (12),  [cuna](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (9),  [subvención](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (10),  [pesimismo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4).
8.  [2007_co_uribe](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [guerrilla](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (10),  [sindicalistas](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (7),  [paramilitares](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (8),  [inversionista](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (10),  [despeje](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (7).
9.  [2007_mx_calderon](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [igualar](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (9),  [transformar](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (19),  [tortilla](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4),  [acuíferos](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4),  [miseria](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (10).
10.  [2007_pe_garcia](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [huancavelica](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (9),  [redistribución](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (10),  [callao](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (8),  [407](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4),  [lima](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (7).
11.  [2008_ar_fernandez](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [abordar](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (17),  [capítulo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (12),  [presupone](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [lesa](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (8),  [articular](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5).
12.  [2008_cl_bachelet](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [desafío](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (18),  [mirada](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (10),  [aprobamos](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [adulto](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [diez](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (11).
13.  [2008_co_uribe](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [ecopetrol](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [revaluación](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4),  [juegos](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4),  [desatrasar](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (3),  [billones](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6).
14.  [2008_mx_calderon](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [cártel](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [noches](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (3),  [mexicanas](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [controlaba](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (3),  [federales](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6).
15.  [2008_pe_garcia](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [poblados](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (11),  [kilómetros](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (52),  [lima](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (11),  [carreteras](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (21),  [mineros](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4).
16.  [2009_ar_fernandez](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [sosteniendo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (7),  [dirigencia](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [coparticipación](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [catamarca](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (7),  [pbi](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (9).
17.  [2009_cl_bachelet](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [sello](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [fortalecidos](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [crisis](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (48),  [gente](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (24),  [aplauso](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4).
18.  [2009_co_uribe](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [colombia](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (20),  [calzada](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [contributivo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (5),  [desplazados](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [notificado](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (3).
19.  [2009_mx_calderon](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [federal](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (27),  [organizado](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (10),  [cambiar](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (13),  [propongo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (8),  [policiacos](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4).
20.  [2009_pe_garcia](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#):  [lima](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (11),  [1,500](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6),  [tingo](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4),  [pampas](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (4),  [desorden](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#)  (6).

### Palabras en contexto

El proyecto con el que algunas historias dan por inauguradas las Humanidades Digitales es el _Index Thomisticus_, una concordancia de la obra de Tomás de Aquino iniciada por el filólogo y religioso Roberto Busa. En la esquina inferior derecha Voyant, es posible hacer consultas de términos específicos.

La tabla que vemos tiene las siguientes columnas predeterminadas:

1. **Documento**: aquí aparece el nombre del documento en el que ocurre(n) la(s) palabra(s) clave(s)  de la consulta
2. **Izquierda**: contexto izquierdo de la palabra clave (este puede ser modificado para abarcar más palabras o menos y si se da clic sobre la celda, ésta se expande para mostrar más contexto)
3. **Términos**: palabra(s) clave(s) de la consulta
4. **Derecha**: contexto derecho

Se puede añadir la columna **Posición** que indica el lugar en el documento en el que se encuentra el término consultado:

![Agregar columna de posición](img/posicion.png)

> **Consulta avanzada** Voyant permite el uso de comodines para buscar variaciones de una palabra. Estas son algunas de las combinaciones
> * **famili***: esta consulta arrojará todas las palabras que empiecen con el prefijo "famili" (familias, familiares, familiar, familia)
> * ***ción**: términos que terminan con el sufijo "ción" (contaminación, militarización, fabricación)
> * **pobreza, desigualdad**: puedes buscar más de un término separándolos por comas* avena: términos coincidentes que terminan con el sufijo avena como un término
> **"contra la pobreza"**: buscar la frase exacta
>  **"pobreza extrema"~ 5**:  buscar los términos dentro de las comillas, el orden no importa, y pueden haber hasta 5 palabras de por medio (esa condición regresaría frases cómo "la extrema desigualdad y la pobreza" donde se encuentra la palabra "pobreza" y "extrema" 

#### :pencil2: *Actividad 9*
1. Busca el uso de algún término que te parezca interesante, utiliza alguna de las estrategias de la consulta avanzada
2. Ordena las filas usando las diferentes columnas (Documento, Izquierda, Derecha y Posición): ¿qué conclusiones puedes derivar sobre tus términos utilizando la información de estas columnas?
> **Ojo**: el orden de las palabras en la columna "Izquerda" es inverso; es decir, de derecha a izquierda desde la palabra clave.

#### Exportando las tablas
Para exportar los datos se da clic en el cuadro con flecha que aparece cuando pasas el cursor sobre la esquina derecha de "Contextos". En seguida se selecciona la opción “Exportar datos actuales” y se da clic sobre la última opción **[ExportGridAllTsv]**
  
Eso lleva a una página donde están separados los campos por un tabulador:

![Exportar contextos](img/exportar_contextos.png)

Selecciona todos los datos (Ctrl+A o Ctrl+E); copiálos (Ctrl+C) y pégalos en una hoja de cálculo (Ctrl+V). Si esto no funciona, guarda los datos como en un editor sencillo de texto como .txt (¡no olvides la codificación UTF-8) y luego en tu hoja de cálculo importa los datos. En Excel esto se hace en la pestaña de "Datos" y después “Desde un archivo de texto”

![Importar datos desde un archivo de texto](img/datos_archivo_de_texto.png)

## Respuestas a las actividades

### Actividad 1
Este corpus tiene 2 documentos con un total de palabras de 4 y 3 palabras únicas *(tengo, hambre, sueño)*
### Actividad 2
1. Podríamos observar, por ejemplo, que los textos más largos son de dos países: Chile y Argentina, y de tres presidentes distintos: Kirchner, Bachelet y Pinera. Sobre los más cortos podríamos ver que si bien el más corto es de Perú, en realidad los que más aparecen entre los breves son los de México y Colombia.
2. Saber la extensión de nuestros textos nos permite entender la homogeneidad o disparidad de nuestro corpus, así como entender ciertas tendencias (por ejemplo, en qué años tendían a ser más cortos los discursos, en qué momento cambió la extensión, etc.)
### Actividad 3
1. a) **La estrofa 1** tiene 23 palabras y 20 son palabras únicas, por lo que 20/23 da igual a una densidad de vocabulario de 0.870; en realidad de 0.869 pero Voyant Tools redondea estos números: https://voyant-tools.org/?corpus=b6b17408eb605cb1477756ce412de78e b) **La estrofa 2** tiene 24 palabras y 20 son palabras únicas, por lo que 20/24 da igual a una densidad de vocabulario de 0.833: https://voyant-tools.org/?corpus=366630ce91f54ed3577a0873d601d714. Como podemos observar la diferencia entre un verso de Sor Juana Inés de la Cruz y otro compuesto por Érika Ender, Daddy Yankee y Luis Fonsi tienen una diferencia de densidad de 0.037; por lo cual debemos tener cuidado al interpretar estos números pues sólo son un indicador cuantitativo de la riqueza del vocabulario y no incluye parámetros como la complejidad de la rima o de los términos.
2. Parece haber una correspondencia entre los discursos más cortos y los más densos, esto es natural pues entre más breve es un texto menos "oportunidad" hay para repetirse. No obstante, esto también podría decirnos algo sobre los estilos de diferentes países o presidentes. Entre menos densidad es más probable que recurran a más recursos retóricos.

### Actividad 4

Estos resultados parecen indicar que la presidenta Kirchner, además de tener los discursos más largos es la que hace frases más largas; sin embargo tenemos que tener cuidado con las conclusiones de este tipo pues se trata de discursos orales en los que la puntuación depende de quien transcribe el texto.

### Actividad 5
1. [a](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (5943); [más](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (1946); [no](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (1694); [mil](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (1045); [millones](https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#) (971)
2. La primera palabra es una preposición, la segunda un adverbio de comparición y la tercera un adverbio de negación. Estas palabras podrían ser significativas si lo que se busca comprender es el uso de este tipo de palabras funcionales. Sin embargo, si lo que se  busca son más bien sustantivos, habrá que hacer un filtrado (ver sección: "Palabras más frecuentes")


## Bibliografía

Peña, Gilberto Anguiano, y Catalina Naumis Peña. 2015. «Extracción de candidatos a términos de un corpus de la lengua general». _Investigación Bibliotecológica: Archivonomía, Bibliotecología e Información_ 29 (67): 19-45. [https://doi.org/10.1016/j.ibbai.2016.02.035](https://doi.org/10.1016/j.ibbai.2016.02.035).
Sinclair, Stéfan and Geoffrey Rockwell, 2016.  _Voyant Tools_. Web. [http://voyant-tools.org/](http://voyant-tools.org/).


## Notas al pie

<sup>1</sup> Existen formas más complejas para cargar el corpus que [puedes consultar en la documentación en inglés](https://voyant-tools.org/docs/#!/guide/corpuscreator)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMTUzOTYxNTIsMTc4MTE0NjY3MSwtMT
EzNTY0NDM3MCwtMTUxODAyMTA1MiwtMTAzMDM1NTc1OCwtNjQw
NTkxNjU4LDE5MjEyMDI3NjMsMTA5MzQ2MjY4MSw5ODg2NTQ4MT
MsMTEzMzMxNzk0NiwxMTY0NzI4MTYxLDE3MzM5NTM1NDYsLTIy
NzIzMjAxOCw0NTM1MzAxNjIsMTIxNDU4MzQyOCwtNjA1MTg1MD
A1LC0yMTQxNDYwNjU2LC0yMTM1MTE5NDEyLDE4OTExOTYwNTYs
MTcyODQ3OTQ0OV19
-->