---


---

<h1 id="análisis-de-corpus-con-voyant-tools">Análisis de corpus con Voyant Tools</h1>
<p>El análisis de corpus es un tipo de <a href="http://vocabularios.caicyt.gov.ar/portal/index.php?task=fetchTerm&amp;arg=26&amp;v=42">análisis de contenido</a>, que permite hacer comparaciones a gran escala entre los textos contenidos en dichos corpus.</p>
<p>Desde el inicio de la computación, lingüistas y especialistas de la <a href="http://vocabularios.caicyt.gov.ar/portal/?task=fetchTerm&amp;arg=178&amp;v=42">recuperación de la información</a> han creado y utilizado software para apreciar patrones que no son evidentes en la lectura o bien, para corroborar hipótesis que intuían al leer ciertos textos. Por ejemplo: los patrones de uso y decaimiento de ciertos términos en una época dada, los contextos izquierdos y derechos de ciertas palabras, o las expresiones que distinguen a un grupo de textos frente a otros.</p>
<p>Voyant Tools (Sinclair y Rockwell, 2016) es una herramienta basada en Web y no requiere de la instalación de ningún tipo de software especializado pues funciona en cualquier equipo con conexión a internet.</p>
<p>Al finalizar este tutorial, tendrás la capacidad de:</p>
<ul>
<li>
<p>Armar un corpus en texto plano</p>
</li>
<li>
<p>Pensar y aplicar diferentes técnicas de segmentación de corpus</p>
</li>
<li>
<p>Identificar características básicas del corpus:</p>
<ul>
<li>Extensión de los documentos subidos</li>
<li>Densidad léxica (llamada densidad de vocabulario en la plataforma)</li>
<li>Promedio de palabras por oración</li>
<li>Relevancia (llamadas “palabras distintivas”)</li>
</ul>
</li>
<li>
<p>Realizar consultas específicas sobre el corpus:</p>
<ul>
<li>Leer diferentes estadísticas sobre los vocablos (frecuencia absoluta y relativa, tendencia y asimetría estadística)</li>
<li>Buscar palabras clave en contexto</li>
<li>Identificar patrones de uso de un término</li>
</ul>
</li>
<li>
<p>Exportar los datos y las visualizaciones en diferentes formatos (csv, png, html)</p>
</li>
</ul>
<h2 id="creando-un-corpus-en-texto-plano">Creando un corpus en texto plano</h2>
<p>Si bien VoyantTools puede trabajar con muchos tipos de formato (HTML, XML, PDF, RTF, y MS Word); en este tutorial utilizaramos texto plano. El texto plano tienen tres ventajas fundamentales: no tiene ningún tipo de formato adicional, no requiere un programa especial y tampoco  o conocimiento extra.</p>
<h3 id="buscar-textos">1. Buscar textos</h3>
<p>Lo primero que debes hacer es buscar la información que te interesa. Para este tutorial, <a href="https://twitter.com/rivaquiroga">Riva Quiroga</a> y yo preparamos un corpus de los discursos presidenciales anuales de Argentina, Chile, Colombia, México y Perú (este último gracias a <a href="https://twitter.com/madvivacious">Pamela Sertzen</a>) entre 2006 y 2010, es decir dos años antes y después de la crisis económica de 2008.</p>
<h3 id="copiar-en-editor-de-texto-plano">2. Copiar en editor de texto plano</h3>
<p>Una vez localizada la información, el segundo paso es copiar el texto que te interesa desde la primera palabra dicha hasta la última y guardarla en un editor de texto sin formato. Por ejemplo:</p>
<ul>
<li>en Windows podría guardarse en <a href="https://web.archive.org/web/20091013225307/http://windows.microsoft.com/en-us/windows-vista/Notepad-frequently-asked-questions">Bloc de Notas</a></li>
<li>en Mac, en <a href="https://support.apple.com/es-mx/guide/textedit/welcome/mac">TextEdit</a>;</li>
<li>y en Linux, en <a href="https://wiki.gnome.org/Apps/Gedit">Gedit</a>.</li>
</ul>
<h3 id="guardar-archivo">3. Guardar archivo</h3>
<p>Cuando guardes el texto debes considerar tres cosas esenciales:</p>
<p>La primera es que, si los textos de tu corpus están en español, deberás <strong>guardarlos en UTF-8</strong>, que es un formato de codificación de caracteres estándar para este idioma.</p>
<p>(gif de cómo guardar)</p>
<blockquote>
<p><strong>¿Qué es utf-8?</strong> Si bien en nuestra pantalla vemos que al teclear una “É” aprece una “É”; para una computadora “É” es una serie de ceros y unos que son interpretados en imagen dependiendo del “traductor” o “codificador” que se esté usando. El codificador que contiene códigos binarios para todas los caracteres que se usan en el español es UTF-8. Siguiendo con el ejemplo “11000011”, es una cadena de ocho bits --es decir, <strong>ocho</strong> espacios de información-- que en UTF-<strong>8</strong> son interpretados como “É”</p>
</blockquote>
<p>La segunda es que <strong>el nombre de tu archivo no debe contener acentos ni espacios</strong>, esto asegurará que pueda ser abierto en otros sistemas operativos</p>
<blockquote>
<p><strong>¿Por qué evitar acentos y espacios en los nombres de archivo?</strong> Por razones similares a el inciso anterior, un archivo que se llame Ébano.txt no siempre será entendido de forma correcta por todos los sistemas operativos pues varios tienen otro codificador por defecto. Muchos usan ASCII, por ejemplo, que sólo tiene siete bits de manera que el último bit (1) de “11000011” es interpretado como el inicio del siguiente caracter y se descuadra la interpretación.</p>
</blockquote>
<p>La tercera es que es una buena práctica integrar ciertos metadatos de contexto (v.g. fecha, género, autor, origen) en el nombre del archivo que te permitan partir tu corpus según diferentes criterios y también leer mejor los resultados. Para este tutorial hemos nombrado los archivos con el año del discurso presidencial, el<br>
código del país (<a href="https://www.iso.org/obp/ui/#search">ISO 3166-1 alfa-2</a>) y el apellido de quien profirió el disurso.</p>
<blockquote>
<p><a href="https://github.com/corpusenespanol/discursos-presidenciales/blob/master/mexico/2007_mx_calderon.txt" title="2007_mx_calderon.txt">2007_mx_calderon.txt</a> tiene el año del discurso dividido con un guión bajo, el código de dos letras del país (México = mx) y el apellido del presidente que dictó el discurso, Calderón, (sin acentos ni eñes)</p>
</blockquote>
<h2 id="cargar-el-corpus">Cargar el corpus</h2>
<p>En la página de entrada de Voyant Tools encontrarás cuatro opciones sencillas para cargar textos.<sup>1</sup> Las dos primeras opciones son en el cuadro blanco. En este cuadro puedes pegar directamente un texto que hayas copiado de algún lugar; o bien, pegar la(s) dirección(es) web --separadas por comas-- de los sitios en donde se encuentren los textos que quieres analizar.<br>
Una tercera opción es “Abrir” alguno de los dos corpus que Voyant tiene precargados (las obras de Shakespeare o las novelas de Austen: ambos en inglés).</p>
<p>Por último, está la opción que usaremos en este tutorial, en la que puedes cargar directamente los documentos que tengas en tu computadora. En este caso subiremos el <a href="https://github.com/corpusenespanol/discursos-presidenciales/tree/master/corpus-completo">corpus completo</a> de discursos presidenciales.</p>
<blockquote>
<p><strong>Para obtener los materiales</strong> de este tutorial ve <a href="https://github.com/corpusenespanol/discursos-presidenciales/tree/master/corpus-completo">a esta página de Github</a>  y descarga todos los archivos:</p>
</blockquote>
<p><img src="img/1_descargar_archivos.png" alt="Descargar corpus"></p>
<blockquote>
<p><strong>Para descomprimir en Windows</strong> haz clic derecho en el  archivo comprimido (.<strong>ZIP</strong>). En el menú desplegable, selecciona <strong>7-zip</strong>  y haz clic en “Extraer aquí”<br>
<strong>Para descomprimir en Mac</strong> da doble clic sobre el archivo comprimido<br>
<strong>Para descomprimir en Linux</strong> botón derecho + “Extraer aquí”</p>
</blockquote>
<p>Para cargar los materiales pulsas sobre el icono que dice cargar, abres tu explorador de archivos y, dejando presionada la tecla ‘Shift’ seleccionas todos los archivos que vas a usar. Para esta primera parte del tutorial subiremos todos los archivos de la carpeta <a href="https://github.com/corpusenespanol/discursos-presidenciales/tree/master/corpus-completo">“corpus completo”</a></p>
<p><img src="img/cargar.png" alt="Cargar documentos"></p>
<h2 id="explorando-el-corpus">Explorando el corpus</h2>
<p>Una vez cargados todos los archivos llegará a la ‘interfaz’ (‘skin’) que tiene cinco herramientas por defecto.</p>
<ol>
<li>
<p>Cirrus: tipo de nube de palabras que muestra los términos más frecuentes<br>
<img src="img/cirrus.png" alt="Cirrus"></p>
</li>
<li>
<p>Lector: espacio para la revisión y lectura de los textos completos con una gráfica de barras que indica la cantidad de texto que tiene cada documento</p>
</li>
</ol>
<p><img src="img/lector.png" alt="Lector"></p>
<ol start="3">
<li>Tendencias: gráfico de distribución que muestra los términos en todo el corpus (o dentro de un documento cuando sólo se carga uno)</li>
</ol>
<p><img src="img/tendencias.png" alt="Lector"></p>
<ol start="4">
<li>
<p>Sumario: proporciona una visión general de ciertas estadísticas textuales del corpus actual<br>
<img src="img/sumario.png" alt="Resumen"></p>
</li>
<li>
<p>Contextos: concordancia que muestra cada ocurrencia de una palabra clave con un poco de contexto circundante<br>
<img src="img/contextos.png" alt="Contextos"></p>
</li>
</ol>
<h3 id="sumario-de-los-documentos">Sumario de los documentos</h3>
<p>Una de las ventanas más informativas de Voyant es la del sumario. Aquí obtenemos una vista de pájaro sobre algunas estadísticas de nuestro corpus por lo que funciona como un buen punto de partida.</p>
<h4 id="número-de-textos-palabras-y-palabras-únicas">Número de textos, palabras y palabras únicas</h4>
<p>La primera frase que leemos se ve algo como esto:</p>
<blockquote>
<p>Este corpus tiene 25 documentos con 261,032  total de palabras y 18,550 formulario de palabra única. Creado  hace 8 horas atrás [el texto es producto de una traducción semi-automática del inglés y por eso se lee raro]</p>
</blockquote>
<p>De entrada con esta información sabemos exactamente cuántos documentos distintos fueron cargados (25); cuántas palabras en total hay (261,032); y cuántas palabras distintas y únicas existen (18,550).</p>
<h4 id="pencil2-actividad-1">✏️ <em>Actividad 1</em></h4>
<p>Si nuestro corpus estuviera compuesto de dos documentos; uno que dijera: “tengo hambre”; y otro que dijera: “tengo sueño”. ¿Qué información aparecería en la primera línea del sumario?<br>
Este corpus tiene ____ documentos con un total de palabras de ____ y ____ palabras únicas.</p>
<h4 id="extensión-de-documentos">Extensión de documentos</h4>
<p>Lo segundo que vemos es la sección de “extensión del documento”. Ahí aparece lo siguiente:</p>
<ul>
<li>Más largo:  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2008_cl_bachelet</a> (20702);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2007_ar_kircher</a> (20390);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2006_ar_kircher</a> (18619);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2010_cl_pinera</a> (16982);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2007_cl_bachelet</a> (15514)</li>
<li>Más corto:  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2006_pe_toledo</a> (1289);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2006_mx_fox</a> (2450);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2008_mx_calderon</a> (3317);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2006_co_uribe</a> (4709);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2009_co_uribe</a> (5807)</li>
</ul>
<h4 id="pencil2-actividad-2">✏️ <em>Actividad 2</em></h4>
<ol>
<li>¿Qué podemos concluir sobre los textos más largos y los más cortos considerando los metadatos del título?</li>
<li>¿Para qué nos servirá saber la longitud de los textos?</li>
</ol>
<h4 id="densidad-del-vocabulario">Densidad del vocabulario</h4>
<p>La densidad de vocubulario se mide dividiendo el número de palabras distintas entre el número de palabras totales. Entre más cercano a uno es el índice de densidad quiere decir que el vocabulario es más denso.</p>
<h4 id="pencil2-actividad-3">✏️ <em>Actividad 3</em></h4>
<ol>
<li>Calcula la densidad de las siguientes estrofas, compara y comenta:</li>
</ol>
<ul>
<li>Estrofa 1.</li>
</ul>
<blockquote>
<p>¿Qué humor puede ser más raro<br>
que el que, falto de consejo,<br>
él mismo empaña el espejo,<br>
y siente que no esté claro?</p>
</blockquote>
<ul>
<li>Estrofa 2.</li>
</ul>
<blockquote>
<p>Pasito a pasito, suave suavecito<br>
Nos vamos pegando poquito a poquito<br>
Cuando tú me besas con esa destreza<br>
Veo que eres malicia con delicadeza</p>
</blockquote>
<ol start="2">
<li>Lee los datos densidad léxica de los documentos de nuestro corpus, ¿qué te dicen?</li>
</ol>
<ul>
<li>Más alto:  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2006_pe_toledo</a> (0.404);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2006_co_uribe</a> (0.340);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2009_co_uribe</a> (0.336);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2008_co_uribe</a> (0.334);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2006_mx_fox</a> (0.328)</li>
<li>Más bajo:  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2008_cl_bachelet</a> (0.192);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2007_mx_calderon</a> (0.192);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2007_ar_kircher</a> (0.206);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2007_pe_garcia</a> (0.214);  <a href="https://voyant-tools.org/?corpus=b6f0e2c5ee1bc9b644ffda6b86a93740&amp;panels=cirrus,reader,trends,summary,contexts#">2010_ar_fernandez</a> (0.217)</li>
</ul>
<ol start="3">
<li>Compáralos con la información sobre su extensión, ¿qué notas?</li>
</ol>
<h4 id="palabras-por-oración">Palabras por oración</h4>
<p>La forma en Voyant calcula la longitud de las oraciones debe considerarse muy aproximada, especialmente por lo complicado que es distinguir entre el final de una abreviatura y el de una oración y otros usos de la puntuación (por ejemplo, en algunos casos un punto y coma marca el límite entre oraciones y en otros . El análisis de las oraciones es realizado por una ‘clase’ del lenguaje de programación Java (es decir, una plantilla con instrucciones) que se llama <a href="https://docs.oracle.com/javase/tutorial/i18n/text/about.html">BreakIterator</a>.</p>
<h4 id="pencil2-actividad-4">✏️ <em>Actividad 4</em></h4>
<ol>
<li>Observa las estadísticas de palabras por oración (ppo) y contesta: ¿qué patrón o patrones puedes observar si consideras el índice de ppo y los metadatos de país, presidente y año contenidos en el nombre del documento?</li>
<li>Da clic sobre los nombre de algunos documentos que te interesen por su índice de ppo. Dirige tu mirada a la ventana de “Lector” y lee algunas líneas, ¿leer el texto original agrega información nueva a tu lectura de los datos? Comenta por qué.</li>
</ol>
<h4 id="palabras-más-frecuentes-y-palabras-diferenciadas">Palabras más frecuentes y palabras diferenciadas</h4>
<p>(volveremos a este inciso en la siguiente sección)</p>
<h3 id="términos-frecuentes">Términos frecuentes</h3>
<p>Ya que tenemos una idea de algunas características globales de nuestros documentos, es momento de que empecemos con las características de los conceptos en nuestro corpus. El primer aspecto con el que vamos a trabajar es con el de <strong>frecuencia</strong> y para esto utilizaremos la ventana de Cirrus.</p>
<h4 id="pencil2-actividad-5">✏️ <em>Actividad 5</em></h4>
<p>a) ¿Qué palabras son las más frecuente en el corpus?<br>
b) ¿Qué nos dicen estas palabras del corpus?, ¿son significativas todas?</p>
<blockquote>
<p><strong>Tip</strong> pasa el mouse sobre las palabras para obtener sus frecuencias derecho</p>
</blockquote>
<p>La importancia no es un valor intrínseco y dependerá siempre de nuestros intereses. Justo por eso Voyant ofrece la opción de filtrar ciertas palabras. Un procedimiento común para obtener palabras relevantes es el de filtrar las unidades léxicas gramaticales o <em>palabras vacías</em>: artículos, preposiciones, interjecciones, pronombres, etc. (Peña y Peña, 2015)-</p>
<h4 id="pencil2-actividad-6">✏️ <em>Actividad 6</em></h4>
<p>a) ¿Qué palabras vacías están en la nube de palabras?<br>
b) ¿Cuáles eliminarías y por qué?</p>
<p>Voyant tiene ya cargada una lista de <em>stop words</em> o palabras vacías; no obstante, nosotros podemos editarla de la siguiente manera:<br>
Colocamos nuestro cursor enor superior derecha de la ventana de Cirrus. Y damos clic sobre el icono que parece un interruptor.</p>
<p><img src="img/editar_lista.png" alt="Abrir opciones"></p>
<p>Aparecerá una ventana con diferentes opciones, seleccionamos la primera “Editar lista”</p>
<p><img src="img/editarlista.png" alt="Editar lista"></p>
<p>Agregamos las palabras “vacías”, siempre separadas por un salto de línea (tecla enter)</p>
<p><img src="img/lista_ruido.png" alt="Editar palabras vacías"></p>
<p>Una vez que hayamos añadido las palabras que deseamos filtrar damos clic en “salvar”.</p>
<blockquote>
<p><strong>Ojo</strong> por defecto está seleccionado una caja que dice “Aplicar a todo”; si ésta se deja seleccionada el filtrado afectará las métricas de todas las otras herramienta. Es muy importante que documentes tus decisiones. Una buena práctica es guardar la lista de palabras vacías en un archivo de texto (.txt) Para este tutorial hemos creado una lista de palabras para filtrar y la puedes usar si así lo quieres, sólo recuerda que esto afectará tus resultados. Por ejemplo: en la lista de palabras filtradas incluí “todas” y “todos”, habrá personas para las que estas palabras podrían ser interesantes dado que muestran que “todos” es mucho más utilizado que “todas” y esto podría darnos pistas sobre el uso de lenguaje incluyente.</p>
</blockquote>
<h4 id="palabras-más-frecuentes">Palabras más frecuentes</h4>
<p>Volvamos entonces a esta sección del sumario. Como dijimos en el iniciso anterior las palabras filtradas afectan otros campos de Voyant. En este caso, si dejasta seleccionada la caja de “Aplicar a todo”  la lista debajo de la leyenda: <strong>Palabra más frecuente en el corpus</strong> , mostrará las palabras que se repiten más <strong>sin contar</strong> aquéllas que fueron filtradas. En mi caso, muestra:</p>
<blockquote>
<p><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">social</a> (437); <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">nacional</a> (427); <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">nuestro</a> (393); <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">inversión</a> (376); <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">ley</a> (369)</p>
</blockquote>
<h4 id="pencil2-actividad-7">✏️ <em>Actividad 7</em></h4>
<ol>
<li>Reflexiona sobre estas palabras y piensa qué información te proporcionan y cómo se distingue esta información de la que obtienes viendo la nube de palabras.</li>
<li>Si estás en un grupo discute las diferencias de tus resultados con los de los demás</li>
</ol>
<h4 id="frecuencia-normalizada">Frecuencia Normalizada</h4>
<p>En el apartado anterior hemos observado la “frecuencia bruta” de las palabras.<br>
Ahora, si tuviéramos un corpus de seis palabras y otro de 3,000 palabras, las frecuencias brutas son poco informativas. Tres palabras en un corpus de seis palabras representa 50% del total, tres palabras en un corpus de 6,000 representan el 0.1% del total.<br>
Para evitar la sobre-representación de un término, los lingüistas han ideado otra medida que se llama: “frecuencia relativa normalizada”.<br>
Ésta se calcula de la siguiente manera:<br>
Frecuencia Bruta * 1,000,000 / Número total de palabras.<br>
Analicemos un verso como ejemplo. Tomemos la frase: “pero mi corazón dice que no, dice que no”, que tiene ocho palabras en total. Si calculamos su frecuencia bruta y relativa tenemos que:</p>

<table>
<thead>
<tr>
<th>palabra</th>
<th>frecuencia bruta</th>
<th>frecuencia normalizada</th>
</tr>
</thead>
<tbody>
<tr>
<td>corazón</td>
<td>1</td>
<td>1*1,000,000/8 = 125,000</td>
</tr>
<tr>
<td>dice</td>
<td>2</td>
<td>2*1,000,000/8 = 111,000</td>
</tr>
</tbody>
</table><p>¿Cuál es la ventaja de esto? Que si tuviéramos un corpus en el que la palabra corazón tuviera la misma proporción, por ejemplo 1,000 ocurrencias entre 8,000 palabras; si bien la frecuencia bruta es muy distinta, la frecuencia normalizada sería la misma, pues 1,000*1,000,000/8,000 también es 125,000.</p>
<p>Veamos cómo funciona esto en Voyant Tools:</p>
<ol>
<li>
<p>En la sección de Cirrus (la nube de palabras), damos clic sobre ‘Terms’ o ‘Términos’. Esto abrirá una tabla que por defecto tiene tres columnas: Términos (con la lista de palabras en los documentos, sin las filtradas), Contar (con la ‘frecuencia bruta o neta’ de cada término) y Tendencia (con una gráfica de la distribución de una palabra tomando su frecuencia relativa). Para obtener información sobre la frecuencia relativa de un término, en la barra de los nombres de columna, en el extremo derecho, se da clic sobre el triángulo que ofrece más opciones y en ‘Columnas’ se selecciona la opción ‘Relativo’ como se muestra en la imagen a continuación:<br>
<img src="img/frecuencia_relativa.png" alt="Editar palabras vacías"></p>
</li>
<li>
<p>Si ordenas las columnas en orden descendiente como lo harías en Excel, observarás que el orden de la frecuencia bruta (‘Contar’) y la frecuencia relativa (‘Relativo’) el orden es el mismo. ¿Para qué nos sirve entonces esta medida? Para cuando comparamos diferentes corpus. Un corpus es un conjunto de textos con algo en común. En este caso, Voyant está interpretando todos los discursos como un solo corpus. Si quisiéramos que cada cada país fuera un corpus distinto, tendríamos que guardar nuestro texto en una tabla, en HTML o en XML, donde los metadatos estuvieran expresados en columnas (en el caso de la tabla) o en etiquetas (en el caso de HTML o XML). Para más información, consulta la documentación en inglés.<sup>1</sup></p>
</li>
</ol>
<h4 id="palabras-diferenciadas">Palabras diferenciadas</h4>
<p>Como tal vez ya sospechas, la información más interesante generalmente no se encuentra dentro de las palabras más frecuentes, pues éstas tienden a ser también las más evidentes. En el campo de la recuperación de la información se han inventado otras medidas que permiten ubicar los términos que hacen que un documento se distinga de otro. Una de las medidas más usadas se llama tf-idf (term frequency, inverse document frequency); la cual busca expresar numéricamente qué tan relevante es un documento en una colección determinada.</p>
<p>En Voyant el tfidf se calcula <a href="https://twitter.com/VoyantTools/status/1025458748574326784">de la siguiente manera</a>:</p>
<p>Frecuencia Bruta  (tf) / Número de Palabras (N)  * log10( Total número de Documentos / termInDocsCount</p>
<p><img src="img/tf_idf.png" alt="Fórmula de TF-IDF"></p>
<h4 id="pencil2-actividad-8">✏️ <em>Actividad 8</em></h4>
<p>Observa las <strong>palabras diferenciadas  (comparado con el resto del corpus)</strong> de cada uno de los documentos y anota qué hipótesis puedes derivar de ellas</p>
<ol>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2006_ar_kircher</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">uruguay</a>  (12),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2004</a>  (13),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2005</a>  (31),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">plata</a>  (7),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">inclusión</a>  (16).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2006_cl_bachelet</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">innovación</a>  (15),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">rodrigo</a>  (8),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">alegremente</a>  (4),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">barrios</a>  (9),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">cobre</a>  (10).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2006_co_uribe</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">tutela</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">reelección</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">regalías</a>  (7),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">iva</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">publicación</a>  (5).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2006_mx_fox</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">atenta</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">apego</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">federalismo</a>  (3),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">intransigencia</a>  (2),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">fundamento</a>  (3).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2006_pe_toledo</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">entrego</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">señor</a>  (14),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">señora</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">amigo</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">tracemos</a>  (2).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2007_ar_kircher</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2006</a>  (65),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">mercosur</a>  (12),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">uruguay</a>  (9),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">provincias</a>  (16),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">interanual</a>  (5).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2007_cl_bachelet</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">macrozona</a>  (7),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">deudores</a>  (12),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">cuna</a>  (9),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">subvención</a>  (10),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">pesimismo</a>  (4).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2007_co_uribe</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">guerrilla</a>  (10),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">sindicalistas</a>  (7),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">paramilitares</a>  (8),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">inversionista</a>  (10),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">despeje</a>  (7).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2007_mx_calderon</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">igualar</a>  (9),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">transformar</a>  (19),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">tortilla</a>  (4),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">acuíferos</a>  (4),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">miseria</a>  (10).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2007_pe_garcia</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">huancavelica</a>  (9),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">redistribución</a>  (10),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">callao</a>  (8),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">407</a>  (4),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">lima</a>  (7).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2008_ar_fernandez</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">abordar</a>  (17),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">capítulo</a>  (12),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">presupone</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">lesa</a>  (8),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">articular</a>  (5).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2008_cl_bachelet</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">desafío</a>  (18),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">mirada</a>  (10),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">aprobamos</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">adulto</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">diez</a>  (11).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2008_co_uribe</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">ecopetrol</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">revaluación</a>  (4),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">juegos</a>  (4),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">desatrasar</a>  (3),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">billones</a>  (6).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2008_mx_calderon</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">cártel</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">noches</a>  (3),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">mexicanas</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">controlaba</a>  (3),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">federales</a>  (6).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2008_pe_garcia</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">poblados</a>  (11),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">kilómetros</a>  (52),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">lima</a>  (11),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">carreteras</a>  (21),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">mineros</a>  (4).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2009_ar_fernandez</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">sosteniendo</a>  (7),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">dirigencia</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">coparticipación</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">catamarca</a>  (7),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">pbi</a>  (9).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2009_cl_bachelet</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">sello</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">fortalecidos</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">crisis</a>  (48),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">gente</a>  (24),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">aplauso</a>  (4).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2009_co_uribe</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">colombia</a>  (20),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">calzada</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">contributivo</a>  (5),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">desplazados</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">notificado</a>  (3).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2009_mx_calderon</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">federal</a>  (27),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">organizado</a>  (10),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">cambiar</a>  (13),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">propongo</a>  (8),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">policiacos</a>  (4).</li>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">2009_pe_garcia</a>:  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">lima</a>  (11),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">1,500</a>  (6),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">tingo</a>  (4),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">pampas</a>  (4),  <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">desorden</a>  (6).</li>
</ol>
<h3 id="palabras-en-contexto">Palabras en contexto</h3>
<p>El proyecto con el que algunas historias dan por inauguradas las Humanidades Digitales es el <em>Index Thomisticus</em>, una concordancia de la obra de Tomás de Aquino iniciada por el filólogo y religioso Roberto Busa. En la esquina inferior derecha Voyant, es posible hacer consultas de términos específicos.</p>
<p>La tabla que vemos tiene las siguientes columnas predeterminadas:</p>
<ol>
<li><strong>Documento</strong>: aquí aparece el nombre del documento en el que ocurre(n) la(s) palabra(s) clave(s)  de la consulta</li>
<li><strong>Izquierda</strong>: contexto izquierdo de la palabra clave (este puede ser modificado para abarcar más palabras o menos y si se da clic sobre la celda, ésta se expande para mostrar más contexto)</li>
<li><strong>Términos</strong>: palabra(s) clave(s) de la consulta</li>
<li><strong>Derecha</strong>: contexto derecho</li>
</ol>
<p>Se puede añadir la columna <strong>Posición</strong> que indica el lugar en el documento en el que se encuentra el término consultado:</p>
<p><img src="img/posicion.png" alt="Agregar columna de posición"></p>
<blockquote>
<p><strong>Consulta avanzada</strong> Voyant permite el uso de comodines para buscar variaciones de una palabra. Estas son algunas de las combinaciones</p>
<ul>
<li><strong>famili</strong>*: esta consulta arrojará todas las palabras que empiecen con el prefijo “famili” (familias, familiares, familiar, familia)</li>
<li>*<strong>ción</strong>: términos que terminan con el sufijo “ción” (contaminación, militarización, fabricación)</li>
<li><strong>pobreza, desigualdad</strong>: puedes buscar más de un término separándolos por comas* avena: términos coincidentes que terminan con el sufijo avena como un término<br>
<strong>"contra la pobreza"</strong>: buscar la frase exacta<br>
<strong>"pobreza extrema"~ 5</strong>:  buscar los términos dentro de las comillas, el orden no importa, y pueden haber hasta 5 palabras de por medio (esa condición regresaría frases cómo “la extrema desigualdad y la pobreza” donde se encuentra la palabra “pobreza” y “extrema”</li>
</ul>
</blockquote>
<h4 id="pencil2-actividad-9">✏️ <em>Actividad 9</em></h4>
<ol>
<li>Busca el uso de algún término que te parezca interesante, utiliza alguna de las estrategias de la consulta avanzada</li>
<li>Ordena las filas usando las diferentes columnas (Documento, Izquierda, Derecha y Posición): ¿qué conclusiones puedes derivar sobre tus términos utilizando la información de estas columnas?</li>
</ol>
<blockquote>
<p><strong>Ojo</strong>: el orden de las palabras en la columna “Izquerda” es inverso; es decir, de derecha a izquierda desde la palabra clave.</p>
</blockquote>
<h4 id="exportando-las-tablas">Exportando las tablas</h4>
<p>Para exportar los datos se da clic en el cuadro con flecha que aparece cuando pasas el cursor sobre la esquina derecha de “Contextos”. En seguida se selecciona la opción “Exportar datos actuales” y se da clic sobre la última opción <strong>[ExportGridAllTsv]</strong></p>
<p>Eso lleva a una página donde están separados los campos por un tabulador:</p>
<p><img src="img/exportar_contextos.png" alt="Exportar contextos"></p>
<p>Selecciona todos los datos (Ctrl+A o Ctrl+E); copiálos (Ctrl+C) y pégalos en una hoja de cálculo (Ctrl+V). Si esto no funciona, guarda los datos como en un editor sencillo de texto como .txt (¡no olvides la codificación UTF-8) y luego en tu hoja de cálculo importa los datos. En Excel esto se hace en la pestaña de “Datos” y después “Desde un archivo de texto”</p>
<p><img src="img/datos_archivo_de_texto.png" alt="Importar datos desde un archivo de texto"></p>
<h2 id="respuestas-a-las-actividades">Respuestas a las actividades</h2>
<h3 id="actividad-1">Actividad 1</h3>
<p>Este corpus tiene 2 documentos con un total de palabras de 4 y 3 palabras únicas <em>(tengo, hambre, sueño)</em></p>
<h3 id="actividad-2">Actividad 2</h3>
<ol>
<li>Podríamos observar, por ejemplo, que los textos más largos son de dos países: Chile y Argentina, y de tres presidentes distintos: Kirchner, Bachelet y Pinera. Sobre los más cortos podríamos ver que si bien el más corto es de Perú, en realidad los que más aparecen entre los breves son los de México y Colombia.</li>
<li>Saber la extensión de nuestros textos nos permite entender la homogeneidad o disparidad de nuestro corpus, así como entender ciertas tendencias (por ejemplo, en qué años tendían a ser más cortos los discursos, en qué momento cambió la extensión, etc.)</li>
</ol>
<h3 id="actividad-3">Actividad 3</h3>
<ol>
<li>a) <strong>La estrofa 1</strong> tiene 23 palabras y 20 son palabras únicas, por lo que 20/23 da igual a una densidad de vocabulario de 0.870; en realidad de 0.869 pero Voyant Tools redondea estos números: <a href="https://voyant-tools.org/?corpus=b6b17408eb605cb1477756ce412de78e">https://voyant-tools.org/?corpus=b6b17408eb605cb1477756ce412de78e</a> b) <strong>La estrofa 2</strong> tiene 24 palabras y 20 son palabras únicas, por lo que 20/24 da igual a una densidad de vocabulario de 0.833: <a href="https://voyant-tools.org/?corpus=366630ce91f54ed3577a0873d601d714">https://voyant-tools.org/?corpus=366630ce91f54ed3577a0873d601d714</a>. Como podemos observar la diferencia entre un verso de Sor Juana Inés de la Cruz y otro compuesto por Érika Ender, Daddy Yankee y Luis Fonsi tienen una diferencia de densidad de 0.037; por lo cual debemos tener cuidado al interpretar estos números pues sólo son un indicador cuantitativo de la riqueza del vocabulario y no incluye parámetros como la complejidad de la rima o de los términos.</li>
<li>Parece haber una correspondencia entre los discursos más cortos y los más densos, esto es natural pues entre más breve es un texto menos “oportunidad” hay para repetirse. No obstante, esto también podría decirnos algo sobre los estilos de diferentes países o presidentes. Entre menos densidad es más probable que recurran a más recursos retóricos.</li>
</ol>
<h3 id="actividad-4">Actividad 4</h3>
<p>Estos resultados parecen indicar que la presidenta Kirchner, además de tener los discursos más largos es la que hace frases más largas; sin embargo tenemos que tener cuidado con las conclusiones de este tipo pues se trata de discursos orales en los que la puntuación depende de quien transcribe el texto.</p>
<h3 id="actividad-5">Actividad 5</h3>
<ol>
<li><a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">a</a> (5943); <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">más</a> (1946); <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">no</a> (1694); <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">mil</a> (1045); <a href="https://voyant-tools.org/?corpus=77227f21c006f5ef083d820d77667627#">millones</a> (971)</li>
<li>La primera palabra es una preposición, la segunda un adverbio de comparición y la tercera un adverbio de negación. Estas palabras podrían ser significativas si lo que se busca comprender es el uso de este tipo de palabras funcionales. Sin embargo, si lo que se  busca son más bien sustantivos, habrá que hacer un filtrado (ver sección: “Palabras más frecuentes”)</li>
</ol>
<h2 id="bibliografía">Bibliografía</h2>
<p>Peña, Gilberto Anguiano, y Catalina Naumis Peña. 2015. «Extracción de candidatos a términos de un corpus de la lengua general». <em>Investigación Bibliotecológica: Archivonomía, Bibliotecología e Información</em> 29 (67): 19-45. <a href="https://doi.org/10.1016/j.ibbai.2016.02.035">https://doi.org/10.1016/j.ibbai.2016.02.035</a>.<br>
Sinclair, Stéfan and Geoffrey Rockwell, 2016.  <em>Voyant Tools</em>. Web. <a href="http://voyant-tools.org/">http://voyant-tools.org/</a>.</p>
<h2 id="notas-al-pie">Notas al pie</h2>
<p><sup>1</sup> Existen formas más complejas para cargar el corpus que <a href="https://voyant-tools.org/docs/#!/guide/corpuscreator">puedes consultar en la documentación en inglés</a></p>

