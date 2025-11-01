# Introducción

Si eres alguien que se dedica a trabajar principalmente en el laboratorio,
lo más probable es que la idea de programar sea algo que puede ser apetecible,
pero no algo necesario para el día a día. Sin embargo Python realmente nos puede
hacer la vida más fácil y, sobre todo, es libre y gratis.

Cuando hablo de usar Python no me refiero a programar: en inglés hay una distinción muy clara entre *programming* o *coding* y *scripting*. Mientras que 
la programación típicamente involucra crear aplicaciones más o menos complejas, el concepto
de *scripting* se puede resumir en escribir una lista de instrucciones que se le pasa
a un programa y que puede reutilizarse. En su acepción literal, scripting es escribir un guión, una receta que te permite hacer cosas de manera más eficiente y reproducible. 

En ese segundo sentido, Python es una herramienta superútil, con innumerables librerías para
tareas tan variadas como correr simulaciones, procesar datos, crear gráficas, o aplicar modelos de inteligencia artificial. Como dice [xkcd](https://xkcd.com/353/):

:::{figure} https://imgs.xkcd.com/comics/python.png
:align: center

xkcd: Python
:::

Usar estas herramientas no require explorar los rincones más recónditos
de un lenguaje de programación o crear aplicaciones con múltiples ficheros. La idea es poder reutilizar
software en muchos casos puntero en scripts de una complejidad mínima. 
Por ejemplo:

```python
from ase import Atoms
from gpaw import GPAW
d = 0.74
a = 6.0

atoms = Atoms('H2',
              positions=[(0, 0, 0),
                         (0, 0, d)],
              cell=(a, a, a))
atoms.center()
calc = GPAW(mode='fd', nbands=2, txt='h2.txt')
atoms.calc = calc
print(atoms.get_potential_energy())
```
calcula la energía potencial de una molécula de hidrógeno usando DFT usando
la librería [gpaw](https://gpaw.readthedocs.io).

Otra ventaja es que todas estas herramientas son software libre con cero coste. La percepción de
que hay que tener mucha financiación para poder hacer investigación de primera línea es en buena parte cierta, sobre todo
desde el punto de vista experimental. Sin embargo, hoy en día en muchas disciplinas es posible realizar
contribuciones significativas en teoría, computación/modelos, e inteligencia artificial usando sólamente
software libre y tu portátil. En muchas áreas estamos limitados más por la habilidad de identificar los problemas relevantes o nuestra capacidad para diseminar los resultados que por los
medios.

Qué lenguaje usar depende de tu disciplina: [R](https://www.r-project.org) domina en las ciencia sociales y ecología, [Julia](https://julialang.org) se está abriendo camino en el análisis de datos, pero Python es el
lenguaje de programación más extendido en la física, la química, y la ciencia de materiales. Es cierto
que las simulaciones más complejas siguen usando lenguajes como Fortran o C, pero la mayoría de ellas tienen una
interfaz que permite utilizarlas desde Python. Eso convierte a Python en el lenguaje ideal para el usuario
casual, el científico que no quiere ser un *coder*, pero que quiere usar herramientas de software libre
que están a su alcance.

¿Cómo aprender Python si tu objectivo no es programar? Mi aproximación sería centrarse en las herramientas que quieres usar en lugar de empezar con tutoriales genéricos y aprender las sutilezas conforme
las vayas necesitando. Los large language models suelen ser buenos para solucionar problemas de programación, y
muchos directamente generan el código necesario. Si los AI summaries de Google están disponibles donde
vives, muchas veces puedes generar un ejemplo completamente gratis desde el navegador. Los AI chatbots tienen fama de ser poco fiables, pero la generación de pequeños programas en Python es
una de las cosas que saben hacer bien.

No todo es perfecto: el lenguaje por defecto en el mundo del software libre y Python es el inglés,
lo cual puede ser una barrera de entrada. Parte de mi motivación para colgar tutoriales de las
herramientas que uso a menudo en este sitio web es contribuir a generar más contenido directamente
en español (aparte de ayudarme a recordar cómo usar herramientas que necesito de higo a breva y
recuperar un poco de soltura escribiendo).

El segundo problema, más específico de Python, es la variedad de formas en la que puedes instalar o usarlo.
A diferencia de lenguajes como R, donde RStudio es la plataforma mayoritaria, no hay un workflow único para
trabajar con Python (de nuevo [xkcd obligatorio](https://xkcd.com/1987/)). Una vez que lo tienes instalado encuentras que la comunidad se ha
centrado en unas pocas herramientas que prácticamente todo el mundo usa y puedes recoger los frutos,
pero primero tienes que llegar ahí.





