---


---

<h1 id="análisis-de-corpus-con-voyant-tools">Análisis de corpus con Voyant Tools</h1>
<p>El análisis de corpus es un tipo de <a href="http://vocabularios.caicyt.gov.ar/portal/index.php?task=fetchTerm&amp;arg=26&amp;v=42">análisis de contenido</a>, que permite hacer comparaciones a gran escala entre los textos contenidos en dichos corpus.</p>
<p>Desde el inicio de la computación, lingüistas y especialistas de la <a href="http://vocabularios.caicyt.gov.ar/portal/?task=fetchTerm&amp;arg=178&amp;v=42">recuperación de la información</a> han creado y utilizado software para apreciar patrones que no son evidentes en la lectura o bien, para corroborar hipótesis que intuían al leer ciertos textos. Por ejemplo: los patrones de uso y decaimiento de ciertos términos en una época dada, los contextos izquierdos y derechos de ciertas palabras, o las expresiones que distinguen a un grupo de textos frente a otros.</p>
<p>Voyant Tools (Sinclair y Rockwell, 2016) es una herramienta basada en Web y no requiere de la instalación de ningún tipo de software especializado pues funciona en cualquier equipo con conexión a internet.</p>
<p>Como se ha dicho en este otro <a href="https://programminghistorian.org/es/lecciones/analisis-de-corpus-con-antconc">tutorial</a>,</p>
<p>Al finalizar este tutorial, tendrás la capacidad de:</p>
<ul>
<li>Armar un corpus en texto plano</li>
<li>Pensar y aplicar diferentes técnicas de segmentación de corpus</li>
<li>Identificar características básicas del corpus:
<ul>
<li>Extensión de los documentos subidos</li>
<li>Densidad léxica (llamada densidad de vocabulario en la plataforma)</li>
<li>Promedio de palabras por oración</li>
<li>Relevancia (llamadas “palabras distintivas”)</li>
</ul>
</li>
<li>Realizar consultas específicas sobre el corpus:
<ul>
<li>Buscar palabras clave en contexto</li>
<li>Identificar patrones de uso de un término</li>
<li>Leer diferentes estadísticas sobre los vocablos (frecuencia absoluta y relativa, tendencia, curtosis, asimetría estadística)</li>
</ul>
</li>
<li>Exportar los datos y las visualizaciones en diferentes formatos (csv, png, html)</li>
</ul>
<h2 id="creando-un-corpus-en-texto-plano">Creando un corpus en texto plano</h2>
<p>Si bien VoyantTools puede trabajar con muchos tipos de formato (HTML, XML, PDF, RTF, y MS Word); en este tutorial utilizaramos texto plano. El texto plano tienen tres ventajas fundamentales: no tiene ningún tipo de formato adicional, no requiere un programa especial y tampoco  o conocimiento extra.</p>
<h3 id="buscar-textos">1. Buscar textos</h3>
<p>Lo primero que debes hacer es buscar la información que te interesa. Para este tutorial, <a href="https://twitter.com/rivaquiroga">Riva Quiroga</a> y yo preparamos un corpus de los discursos anuales de presidentes de Argentina, Chile, Colombia, México y Perú (¡gracias <a href="https://twitter.com/madvivacious">Pamela Sertzen</a>!) entre 2006 y 2010, es decir dos años antes y después de la crisis económica de 2008.</p>
<h3 id="copiar-en-editor-de-texto-plano">2. Copiar en editor de texto plano</h3>
<p>Una vez localizada la información, el segundo paso es copiar el texto que te interesa desde la primera palabra dicha hasta la última y guardarla en un editor de texto sin formato. Por ejemplo:</p>
<ul>
<li>en Windows podría guardarse en Bloc de Notas</li>
</ul>
<p><img src="https://upload.wikimedia.org/wikipedia/en/4/44/Windows_Notepad.png" alt="Bloc de notas"></p>
<ul>
<li>en Mac, en TextEdit;<br>
<img src="https://upload.wikimedia.org/wikipedia/commons/7/7a/TextEdit_1.10_screenshot.png" alt="Text Edit"></li>
<li>y en Linux, en Gedit.<br>
<img src="https://upload.wikimedia.org/wikipedia/commons/7/7a/TextEdit_1.10_screenshot.png" alt="Gedit"></li>
</ul>
<h3 id="guardar-archivo">3. Guardar archivo</h3>
<p>Cuando guardes el texto debes considerar tres cosas esenciales:</p>
<p>La primera es que, si los textos de tu corpus están en español, deberás <strong>guardarlos en UTF-8</strong>, que es un formato de codificación de caracteres estándar para este idioma.</p>
<p>(gif de cómo guardar)</p>
<blockquote>
<p><strong>¿Qué es utf-8?</strong> Si bien en nuestra pantalla vemos que al teclear una “É” aprece una “É”; para una computadora “É” es una serie de ceros y unos que son interpretados en imagen depiendo del “traductor” o “codificador” que se esté usando. El codificador que contiene códigos binarios para todas los caracteres que se usan en el español es UTF-8. Siguiendo con el ejemplo “11000011”, es una cadena de ocho bits --es decir, <strong>ocho</strong> espacios de información-- que en UTF-<strong>8</strong> son interpretados como “É”</p>
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
<p><strong>Para descomprimir en Windows</strong> haz clic derecho en el  archivo comprimido (.<strong>ZIP</strong>). En el menú desplegable, selecciona <strong>7-zip</strong>  y haz clic en "Extraer aquí"<br>
<strong>Para descomprimir en Mac</strong> da doble clic sobre el archivo comprimido<br>
<strong>Para descomprimir en Linux</strong> botón derecho + “Extraer aquí”</p>
</blockquote>
<p>Para cargar los materiales pulsas sobre el icono que dice cargar, abres tu explorador de archivos y, dejando presionada la tecla ‘Shift’ seleccionas todos los archivos que vas a usar. Para esta primera parte del tutorial subiremos todos los archivos de la carpeta <a href="https://github.com/corpusenespanol/discursos-presidenciales/tree/master/corpus-completo">“corpus completo”</a></p>
<p><img src="img/cargar.png" alt="Cargar documentos"></p>
<h2 id="explorando-el-corpus">Explorando el corpus</h2>
<p>Una vez cargados todos los archivos llegará a la ‘interfaz’ (‘skin’) que tiene cinco herramientas por defecto.</p>
<ol>
<li>Cirrus: tipo de nube de palabras que muestra los términos más frecuentes<br>
<img src="img/cirrus.png" alt="Cirrus"></li>
<li>Lector: espacio para la revisión y lectura de los textos completos con una gráfica de barras que indica la cantidad de texto que tiene cada documento<br>
<img src="img/lector.png" alt="Lector"></li>
<li>Tendencias: gráfico de distribución que muestra los términos en todo el corpus (o dentro de un documento cuando sólo se carga uno)<br>
<img src="img/tendencias.png" alt="Lector"></li>
<li>Sumario: proporciona una visión general de ciertas estadísticas textuales del corpus actual<br>
<img src="img/sumario.png" alt="Resumen"></li>
<li>Contextos: concordancia que muestra cada ocurrencia de una palabra clave con un poco de contexto circundante<br>
<img src="img/contextos.png" alt="Contextos"></li>
</ol>
<h3 id="términos-frecuentes">Términos frecuentes</h3>
<p>El primer concepto con el que vamos a trabajar es con el de <strong>frecuencia</strong>. Para esto utilizaremos la ventana de Cirrus.<br>
Actividad:<br>
a) ¿Qué palabras son las más frecuente en el corpus?<br>
b) ¿Qué nos dicen estas palabras del corpus?, ¿son significativas todas?</p>
<blockquote>
<p><strong>Tip</strong> pasa el mouse sobre las palabras para obtener sus frecuencias derecho</p>
</blockquote>
<p>Tal</p>
<p><img src="https://lh5.googleusercontent.com/BbkeB4jyWyNgvybCCSGXcAzFmav-3p9QY-iQzx7JAFKOp31Cw4Cc4yyLt8ZPyie91XrgPI-AltY6vi3zAnpeLvSoyqDLuAXcmPOk92-QHX9MP2rjPLUKX6nBfRuoOHz0Dk9RsJAs" alt=""></p>
<p>Agregar palabras “ruido”, siempre separadas con “enter”</p>
<p><img src="https://lh4.googleusercontent.com/fTmmCqlIGfWAf4HLGSmqwzNFs6bwO8b7qjeeJSJ5HoLZGde8WhMWxUMSlGTXpfov9yn2cyFCZvU6ZOhhlFTQ-vYTaDmqI9za4YYBeflzVEVTA5lAKu3Z494RbLLkYwaSr8Cyv13Z" alt=""></p>
<ol start="3">
<li>Ver palabras en contexto</li>
</ol>
<p>En la barra libre inferior esquina izquierda, escribir palabra que se desea analizar</p>
<p><img src="https://lh3.googleusercontent.com/GSxxs2gtNPI800v_yfoBXoUUCNldLjiuhsO-ViIHOTTU5_vM1cVPAeLWz_yXZNQcTUfZPcwx-LrNETzKNHhlUSd-bgFygt67ConYsVBFmWYOWSwMIrxu9JY1s4ClIi4O0Ku3Al2g" alt=""></p>
<p>Para exportar los datos (la opción te da un txt separado por tabulación) se da clic en el cuadro con flecha y luego en la opción “exportar datos actuales” y se selecciona la última opción</p>
<p><img src="https://lh5.googleusercontent.com/oOAxfmF2GqQPAdoDJu04S-GTXdagRCJWv8dXlECYTzg35mOZR249avA0vYz5dFJDy6xrCneWJgQTr_2D1PHp82ufGRzubhPrIy3H1ZaWGI0B0BUaODvkh_JeouYXP73p3MM2IbFY" alt=""></p>
<p>Normalmente copy paste funciona. Si no lo hace guardar en txt y luego abrir excel y dar clic en datos y después “Desde un archivo de texto”</p>
<p><img src="https://lh4.googleusercontent.com/Et1FZZXYzH37jBv5qYv6LL8TFCjadW-mcHyQFoJQyj2pRYm4B92Q-8E8_h59m4Q8I0d0cjZhMAD-5MensLzs-p-qrCxqtye-7XXJII24bV84qybYG5R6IwTtjjroGkZx1PLCs32B" alt=""></p>
<ol start="4">
<li>Crear árbol de palabras</li>
</ol>
<p>En el icono que parece “ventana windows” dar clic</p>
<ol start="5">
<li>Obtener estadísticas comparadas de los documentos (densidad, palabras diferenciadas, etc)</li>
</ol>
<p><img src="https://lh5.googleusercontent.com/02yX9TWSJVDrlml-T_oS0Zw1ZI9PD1stAyjkYD1YKK50rrR49nhh2mP-SD70X3wNPYDsKZRh80nsGyBpGmkyohsDX-tjM4WZZcZ-SoSuWP_kctOc3b1cbHLloQy2r0Zd55hm8nsC" alt=""></p>
<p><strong>HTML</strong></p>
<p>El Lenguaje para el Marcado de Documentos de Hipertexto (HyperText Markup Language_) es un lenguaje estandarizado para dar formato a documentos que sirvan para crear páginas web y aplicaciones web</p>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-VEVHzkNrmFOlWbEv" height="100%" viewBox="0 0 492.4937515258789 276.171875" style="max-width:492.4937515258789px;"><g><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath" style="opacity: 1;"><path class="path" d="M117.19054015629587,102.79296875L176.609375,59.25L206.1953125,59.25" marker-end="url(#arrowhead48)" style="fill:none"></path><defs><marker id="arrowhead48" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M117.19054015629587,148.79296875L176.609375,192.3359375L201.609375,192.3359375" marker-end="url(#arrowhead49)" style="fill:none"></path><defs><marker id="arrowhead49" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M284.6953125,59.25L314.28125,59.25L365.20661454593557,100.86760344112498" marker-end="url(#arrowhead50)" style="fill:none"></path><defs><marker id="arrowhead50" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M289.28125,192.3359375L314.28125,192.3359375L365.206615386448,151.71833337350853" marker-end="url(#arrowhead51)" style="fill:none"></path><defs><marker id="arrowhead51" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g></g><g class="nodes"><g class="node" id="A" transform="translate(85.8046875,125.79296875)" style="opacity: 1;"><rect rx="0" ry="0" x="-65.8046875" y="-23" width="131.609375" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-55.8046875,-13)"><foreignObject width="111.609375" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Crear un corpus</div></foreignObject></g></g></g><g class="node" id="B" transform="translate(245.4453125,59.25)" style="opacity: 1;"><circle x="-39.25" y="-23" r="39.25"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-29.25,-13)"><foreignObject width="58.5" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Explorar</div></foreignObject></g></g></g><g class="node" id="C" transform="translate(245.4453125,192.3359375)" style="opacity: 1;"><circle x="-43.8359375" y="-23" r="43.8359375"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-33.8359375,-13)"><foreignObject width="67.671875" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Consultar</div></foreignObject></g></g></g><g class="node" id="D" transform="translate(395.88750076293945,125.79296875)" style="opacity: 1;"><polygon points="56.60625,0 113.2125,-56.60625 56.60625,-113.2125 0,-56.60625" rx="5" ry="5" transform="translate(-56.60625,56.60625)"></polygon><g class="label" transform="translate(0,0)"><g transform="translate(-37.7578125,-13)"><foreignObject width="75.515625" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Interpretar</div></foreignObject></g></g></g></g></g></g></svg></div>
<h2 id="bibliografía">Bibliografía</h2>
<p>Sinclair, Stéfan and Geoffrey Rockwell, 2016.  <em>Voyant Tools</em>. Web. <a href="http://voyant-tools.org/">http://voyant-tools.org/</a>.</p>
<h1 id="publication">Publication</h1>
<p>Publishing in StackEdit makes it simple for you to publish online your files. Once you’re happy with a file, you can publish it to different hosting platforms like <strong>Blogger</strong>, <strong>Dropbox</strong>, <strong>Gist</strong>, <strong>GitHub</strong>, <strong>Google Drive</strong>, <strong>WordPress</strong> and <strong>Zendesk</strong>. With <a href="http://handlebarsjs.com/">Handlebars templates</a>, you have full control over what you export.</p>
<blockquote>
<p>Before starting to publish, you must link an account in the <strong>Publish</strong> sub-menu.</p>
</blockquote>
<h2 id="publish-a-file">Publish a File</h2>
<p>You can publish your file by opening the <strong>Publish</strong> sub-menu and by clicking <strong>Publish to</strong>. For some locations, you can choose between the following formats:</p>
<ul>
<li>Markdown: publish the Markdown text on a website that can interpret it (<strong>GitHub</strong> for instance),</li>
<li>HTML: publish the file converted to HTML via a Handlebars template (on a blog for example).</li>
</ul>
<h2 id="update-a-publication">Update a publication</h2>
<p>After publishing, StackEdit keeps your file linked to that publication which makes it easy for you to re-publish it. Once you have modified your file and you want to update your publication, click on the <strong>Publish now</strong> button in the navigation bar.</p>
<blockquote>
<p><strong>Note:</strong> The <strong>Publish now</strong> button is disabled if your file has not been published yet.</p>
</blockquote>
<h2 id="manage-file-publication">Manage file publication</h2>
<p>Since one file can be published to multiple locations, you can list and manage publish locations by clicking <strong>File publication</strong> in the <strong>Publish</strong> sub-menu. This allows you to list and remove publication locations that are linked to your file.</p>
<h1 id="markdown-extensions">Markdown extensions</h1>
<p>StackEdit extends the standard Markdown syntax by adding extra <strong>Markdown extensions</strong>, providing you with some nice features.</p>
<blockquote>
<p><strong>ProTip:</strong> You can disable any <strong>Markdown extension</strong> in the <strong>File properties</strong> dialog.</p>
</blockquote>
<h2 id="smartypants">SmartyPants</h2>
<p>SmartyPants converts ASCII punctuation characters into “smart” typographic punctuation HTML entities. For example:</p>

<table>
<thead>
<tr>
<th></th>
<th>ASCII</th>
<th>HTML</th>
</tr>
</thead>
<tbody>
<tr>
<td>Single backticks</td>
<td><code>'Isn't this fun?'</code></td>
<td>‘Isn’t this fun?’</td>
</tr>
<tr>
<td>Quotes</td>
<td><code>"Isn't this fun?"</code></td>
<td>“Isn’t this fun?”</td>
</tr>
<tr>
<td>Dashes</td>
<td><code>-- is en-dash, --- is em-dash</code></td>
<td>– is en-dash, — is em-dash</td>
</tr>
</tbody>
</table><h2 id="katex">KaTeX</h2>
<p>You can render LaTeX mathematical expressions using <a href="https://khan.github.io/KaTeX/">KaTeX</a>:</p>
<p>The <em>Gamma function</em> satisfying <span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi mathvariant="normal">Γ</mi><mo>(</mo><mi>n</mi><mo>)</mo><mo>=</mo><mo>(</mo><mi>n</mi><mo>−</mo><mn>1</mn><mo>)</mo><mo>!</mo><mspace width="1em"></mspace><mi mathvariant="normal">∀</mi><mi>n</mi><mo>∈</mo><mi mathvariant="double-struck">N</mi></mrow><annotation encoding="application/x-tex">\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="strut" style="height: 0.75em;"></span><span class="strut bottom" style="height: 1em; vertical-align: -0.25em;"></span><span class="base"><span class="mord mathrm">Γ</span><span class="mopen">(</span><span class="mord mathit">n</span><span class="mclose">)</span><span class="mrel">=</span><span class="mopen">(</span><span class="mord mathit">n</span><span class="mbin">−</span><span class="mord mathrm">1</span><span class="mclose">)</span><span class="mclose">!</span><span class="mord mathrm"><span class="mspace quad"></span><span class="mord mathrm">∀</span></span><span class="mord mathit">n</span><span class="mrel">∈</span><span class="mord mathbb">N</span></span></span></span></span> is via the Euler integral</p>
<p><span class="katex--display"><span class="katex-display"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi mathvariant="normal">Γ</mi><mo>(</mo><mi>z</mi><mo>)</mo><mo>=</mo><msubsup><mo>∫</mo><mn>0</mn><mi mathvariant="normal">∞</mi></msubsup><msup><mi>t</mi><mrow><mi>z</mi><mo>−</mo><mn>1</mn></mrow></msup><msup><mi>e</mi><mrow><mo>−</mo><mi>t</mi></mrow></msup><mi>d</mi><mi>t</mi><mspace width="0.16667em"></mspace><mi mathvariant="normal">.</mi></mrow><annotation encoding="application/x-tex">
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="strut" style="height: 1.41429em;"></span><span class="strut bottom" style="height: 2.32624em; vertical-align: -0.91195em;"></span><span class="base"><span class="mord mathrm">Γ</span><span class="mopen">(</span><span class="mord mathit" style="margin-right: 0.04398em;">z</span><span class="mclose">)</span><span class="mrel">=</span><span class="mop"><span class="mop op-symbol large-op" style="margin-right: 0.44445em; position: relative; top: -0.001125em;">∫</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 1.41429em;"><span class="" style="top: -1.78805em; margin-left: -0.44445em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathrm mtight">0</span></span></span><span class="" style="top: -3.8129em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mathrm mtight">∞</span></span></span></span><span class="vlist-s">​</span></span><span class="vlist-r"><span class="vlist" style="height: 0.91195em;"></span></span></span></span></span><span class="mord"><span class="mord mathit">t</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.864108em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathit mtight" style="margin-right: 0.04398em;">z</span><span class="mbin mtight">−</span><span class="mord mathrm mtight">1</span></span></span></span></span></span></span></span></span><span class="mord"><span class="mord mathit">e</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.843556em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">−</span><span class="mord mathit mtight">t</span></span></span></span></span></span></span></span></span><span class="mord mathit">d</span><span class="mord mathit">t</span><span class="mord mathrm"><span class="mspace thinspace"></span><span class="mord mathrm">.</span></span></span></span></span></span></span></p>
<blockquote>
<p>You can find more information about <strong>LaTeX</strong> mathematical expressions <a href="http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference">here</a>.</p>
</blockquote>
<h2 id="uml-diagrams">UML diagrams</h2>
<p>You can render UML diagrams using <a href="https://mermaidjs.github.io/">Mermaid</a>. For example, this will produce a sequence diagram:</p>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-zFZMW0JvZBsK0P9A" height="100%" width="100%" style="max-width:750px;" viewBox="-50 -10 750 484"><g></g><g><line id="actor6" x1="75" y1="5" x2="75" y2="473" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="0" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="75" dy="0">Alice</tspan></text></g><g><line id="actor7" x1="275" y1="5" x2="275" y2="473" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="200" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="275" dy="0">Bob</tspan></text></g><g><line id="actor8" x1="475" y1="5" x2="475" y2="473" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="400" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="475" dy="0">John</tspan></text></g><defs><marker id="arrowhead" refX="5" refY="2" markerWidth="6" markerHeight="4" orient="auto"><path d="M 0,0 V 4 L6,2 Z"></path></marker></defs><defs><marker id="crosshead" markerWidth="15" markerHeight="8" orient="auto" refX="16" refY="4"><path fill="black" stroke="#000000" stroke-width="1px" d="M 9,2 V 6 L16,4 Z" style="stroke-dasharray: 0, 0;"></path><path fill="none" stroke="#000000" stroke-width="1px" d="M 0,1 L 6,7 M 6,1 L 0,7" style="stroke-dasharray: 0, 0;"></path></marker></defs><g><text x="175" y="93" class="messageText" style="text-anchor: middle;">Hello Bob, how are you?</text><line x1="75" y1="100" x2="275" y2="100" class="messageLine0" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="fill: none;"></line></g><g><text x="375" y="128" class="messageText" style="text-anchor: middle;">How about you John?</text><line x1="275" y1="135" x2="475" y2="135" class="messageLine1" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><text x="175" y="163" class="messageText" style="text-anchor: middle;">I am good thanks!</text><line x1="275" y1="170" x2="75" y2="170" class="messageLine1" stroke-width="2" stroke="black" marker-end="url(#crosshead)" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><text x="375" y="198" class="messageText" style="text-anchor: middle;">I am good thanks!</text><line x1="275" y1="205" x2="475" y2="205" class="messageLine0" stroke-width="2" stroke="black" marker-end="url(#crosshead)" style="fill: none;"></line></g><g><rect x="500" y="215" fill="#EDF2AE" stroke="#666" width="150" height="103" rx="0" ry="0" class="note"></rect><text x="516" y="245" fill="black" class="noteText"><tspan x="516">Bob thinks a long</tspan><tspan dy="23" x="516">long time, so long</tspan><tspan dy="23" x="516">that the text does</tspan><tspan dy="23" x="516">not fit on a row.</tspan></text></g><g><text x="175" y="346" class="messageText" style="text-anchor: middle;">Checking with John...</text><line x1="275" y1="353" x2="75" y2="353" class="messageLine1" stroke-width="2" stroke="black" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><text x="275" y="381" class="messageText" style="text-anchor: middle;">Yes... John, how are you?</text><line x1="75" y1="388" x2="475" y2="388" class="messageLine0" stroke-width="2" stroke="black" style="fill: none;"></line></g><g><rect x="0" y="408" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="440.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="75" dy="0">Alice</tspan></text></g><g><rect x="200" y="408" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="440.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="275" dy="0">Bob</tspan></text></g><g><rect x="400" y="408" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="440.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="475" dy="0">John</tspan></text></g></svg></div>
<p>And this will produce a flow chart:</p>
<h2 id="notas-al-pie">Notas al pie</h2>
<p><sup>1</sup> Existen formas más complejas para cargar corpus que <a href="https://voyant-tools.org/docs/#!/guide/corpuscreator">puedes consultar en la documentación en inglés</a></p>

