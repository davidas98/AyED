Práctica #1
Matrices, operaciones en punto flotante y abstracción

Objetivo

La práctica persigue que el alumnado desarrolle algoritmos para diversas operaciones con matrices. Algunas de estas operaciones incluyen comparaciones u otras operaciones con números reales o números almacenados en variables de tipo punto flotante. Debido a que los ordenadores disponen de capacidad de almacenamiento finito estas operaciones requerirán del uso de un valor de tolerancia. El alumno debe saber cómo utilizar este valor de tolerancia en las comparaciones.

Por último, se pretende que el alumnado comprenda la característica de la abstracción en la programación orientada a objetos. Con este fin se implementará un procedimiento que haga percibir al usuario de la clase en estudio que trabaja con una matriz traspuesta, aunque la información aparezca almacenada físicamente en su estado original.

Guión
El alumnado dispondrá del siguiente material:

    Tres ficheros correspondientes a un programa en el lenguaje de programación C++. A saber, un fichero de cabeceras matrices_3.hpp conteniendo la definición de la clase matrix_t, un fichero de implementación matrices_3.cpp conteniendo las implementaciones de los métodos definidos en el fichero de cabeceras, y un fichero main_m_3.cpp conteniendo un ejemplo de programa principal.
    Además se incluye un fichero de datos datos_m_3.txt que contiene los datos de entrada para la práctica.
    Adicionalmente, el alumnado dispone de dos manuales generados automáticamente a partir de la documentación del código: un manual en un fichero PDF denominado ManualMatrices.pdf, y un manual en ficheros HTML accesible como el recurso Manual Matrices 3.0.

Desarrollo

Para superar la práctica, el alumnado debe enriquecer el código proporcionado tal y como se indica a continuación, efectuando las siguientes cuatro fases:

FASE I.  COMPRENSIÓN DEL MATERIAL PROPORCIONADO

    Descargar los ficheros fuente.
    Compilarlos y ejecutarlos: 

$ g++ -g main_m_3.cpp matrices_3.cpp -o matriz_3
$ ./matriz_3 < datos_m_3.txt

    Examinar el fichero de cabeceras. Identificar los constructores, el destructor, los métodos para acceder a los elementos de la matriz individualmente, los métodos para lectura y escritura desde fichero, e identificar los elementos privados, tanto atributos como métodos.
    Examinar el fichero de implementación y comprobar las implementaciones de todos los métodos definidos en la clase.
    Identificar los métodos en la documentación HTML o PDF proporcionada.


FASE II. DESARROLLO DE FUNCIONES DE COMPARACIÓN
Dados dos números reales a,b∈R
, y una tolerancia o precisión ϵ
,

    para comprobar que a

y b
son iguales se tiene que verificar que |a−b|<ϵ
 , es decir, que el valor absoluto de la diferencia es menor que cierta precisión;
para comprobar que a
es mayor que b
se tiene que verificar que a−b>ϵ
;
para comprobar que a
es menor que b
se tiene que verificar que a−b<−ϵ⟹b−a>ϵ
;
para comprobar que a
es igual a cero se tiene que verificar que  |a|<ϵ

    .

Constrúyase cuatro funciones booleanas:

bool igual(matrix_item_t a, matrix_item_t b, double precision);
bool mayor(matrix_item_t a, matrix_item_t b, double precision); 
bool menor(matrix_item_t a, matrix_item_t b, double precision);
bool zero(matrix_item_t a, double precision);

como métodos de la clase matriz_t, que efectúen la comparación de números en punto flotante tal y como se ha descrito.
Nota: Se deberá hacer uso de la función fabs(double a), para lo cual se deberá cargar la cabecera #include <cmath>.


FASE III. DESARROLLO DE UN MÉTODO PARA PONER EN PRÁCTICA LA COMPARACIÓN

Constrúyase un procedimiento:

void filtra(matrix_t& M, matrix_item_t it, double precision);

como método de la clase matriz_t, que construya una matriz M, de tamaño igual a la original, que contenga aquellos elementos de la matriz original iguales al elemento it, de acuerdo a una tolerancia dada por precisión. Las celdas de la matriz que difieran de it deberán contener 0.0.
Inclúyase las siguientes líneas en el programa principal a fin efectuar la verificación de este procedimiento.

matrix_t A;
matrix_t B;

cout << endl;
A.read(cin);
cout << "---  MATRIZ ORIGINAL  ---" << endl;
A.write();

cout << "---  PRECISIÓN 0.0001 ---" << endl;
A.filtra(B,5.254,1E-4);
B.write();

cout << "---  PRECISIÓN 0.001  ---" << endl;
A.filtra(B,5.254,1E-3);
B.write();

cout << "---  PRECISIÓN 0.01   ---" << endl;
A.filtra(B,5.254,1E-2);
B.write();

cout << "---  PRECISIÓN 0.1    ---" << endl;
A.filtra(B,5.254,1E-1);
B.write();

cout << "---  PRECISIÓN 1.0    ---" << endl;
A.filtra(B,5.254,1.0);
B.write();


El resultado por pantalla debe ser el siguiente:


---  MATRIZ ORIGINAL  ---
|   5.254560    5.254570    5.254580  |
|   5.354560    5.254000    5.254100  |
|   5.654560    5.354570    5.255560  |
|   5.754560    6.000000    5.354580  |
|   5.254580    5.300000    5.254590  |
 
---  PRECISIÓN 0.0001 ---
|   0.000000    0.000000    0.000000  |
|   0.000000    5.254000    0.000000  |
|   0.000000    0.000000    0.000000  |
|   0.000000    0.000000    0.000000  |
|   0.000000    0.000000    0.000000  |
 
---  PRECISIÓN 0.001  ---
|   5.254560    5.254570    5.254580  |
|   0.000000    5.254000    5.254100  |
|   0.000000    0.000000    0.000000  |
|   0.000000    0.000000    0.000000  |
|   5.254580    0.000000    5.254590  |
 
---  PRECISIÓN 0.01   ---
|   5.254560    5.254570    5.254580  |
|   0.000000    5.254000    5.254100  |
|   0.000000    0.000000    5.255560  |
|   0.000000    0.000000    0.000000  |
|   5.254580    0.000000    5.254590  |
 
---  PRECISIÓN 0.1    ---
|   5.254560    5.254570    5.254580  |
|   0.000000    5.254000    5.254100  |
|   0.000000    0.000000    5.255560  |
|   0.000000    0.000000    0.000000  |
|   5.254580    5.300000    5.254590  |
 
---  PRECISIÓN 1.0    ---
|   5.254560    5.254570    5.254580  |
|   5.354560    5.254000    5.254100  |
|   5.654560    5.354570    5.255560  |
|   5.754560    6.000000    5.354580  |
|   5.254580    5.300000    5.254590  |

 

FASE IV. TRASPUESTA DE UNA MATRIZ GENERAL

Constrúyase un procedimiento:

void trasponer(void);

como método de la clase matriz_t, que, una  vez invocado, permita al usuario operar con la matriz original en formato traspuesto, independientemente de su dimensión.

Es importante notar que no se debe alterar en absoluto la ubicación física de los datos. Únicamente  debe incluirse como atributo una variable booleana denominada traspuesta_, alterar los métodos :

get_m(),
get_n(),
pos(matrix_inx_t i, matrix_inx_t j),

y alterar todas aquellos métodos en los que se acceda a algún elemento y se haga referencia a la dimensión de la matriz. Inclúyase en un programa principal las siguientes líneas:

matrix_t A;
 
cout << endl;
A.read(cin);
cout << "---  MATRIZ ORIGINAL  ---" << endl;
A.write();
 
cout << "---  MATRIZ ORIGINAL TRASPUESTA---" << endl;
A.trasponer();
A.write();

y cuya salida debe ser:

---  MATRIZ ORIGINAL  ---
|   5.254560    5.254570    5.254580  |
|   5.354560    5.254000    5.254100  |
|   5.654560    5.354570    5.255560  |
|   5.754560    6.000000    5.354580  |
|   5.254580    5.300000    5.254590  |
 
---  MATRIZ ORIGINAL TRASPUESTA---
|   5.254560    5.354560    5.654560    5.754560    5.254580  |
|   5.254570    5.254000    5.354570    6.000000    5.300000  |
|   5.254580    5.254100    5.255560    5.354580    5.254590  |

MODIFICACIN: Crear una función que sume la matriz original con su traspuesta solo en los casos en los que el elemento de la matriz 
original sean inferiores a los de la traspuesta. La función solo recibirá como parámetro la precisin y devolverá una matriz con el 
resultado de la suma.
