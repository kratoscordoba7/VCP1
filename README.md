<h1 align="center">🌟 Práctica 1 - Visión por Computador (Curso 2024/2025)</h1>

<img align="left" width="160" height="160" src="https://i.imgur.com/SckSK0a.png"></a>
Se han completado todas las tareas solicitadas de la **Práctica 1** para la asignatura **Visión por Computador**. Primeros pasos con OpenCV.

*Trabajo realizado por*:

[![GitHub](https://img.shields.io/badge/GitHub-Heliot%20J.%20Segura%20Gonzalez-purple?style=flat-square&logo=github)](https://github.com/kratoscordoba7)

[![GitHub](https://img.shields.io/badge/GitHub-Alejandro%20D.%20Arzola%20Saavedra%20-blue?style=flat-square&logo=github)](https://github.com/AlejandroDavidArzolaSaavedra)

## 🛠️ Librerías Utilizadas

[![NumPy](https://img.shields.io/badge/NumPy-%23013243?style=for-the-badge&logo=numpy)](Link_To_Your_NumPy_Page)
[![OpenCV](https://img.shields.io/badge/OpenCV-%23FD8C00?style=for-the-badge&logo=opencv)](Link_To_Your_OpenCV_Page)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-%43FF6400?style=for-the-badge&logo=matplotlib&logoColor=white)](Link_To_Your_Matplotlib_Page)
[![Pillow](https://img.shields.io/badge/Pillow-%23000000?style=for-the-badge&logo=pillow)](Link_To_Your_Pillow_Page)

---

## 🚀 Cómo empezar

Para comenzar con el proyecto, sigue estos pasos:

> [!NOTE]  
> Debes de situarte en un environment configurado como se definió en el cuaderno de la práctica de [otsedom](https://github.com/otsedom/otsedom.github.io/blob/main/VC/P1/README.md#111-comandos-basicos-de-anaconda).

### Paso 1: Abrir VSCode y situarse en el directorio:
   
   `C:\Users\TuNombreDeUsuario\anaconda3\envs\VCP1`
   
### Paso 2: Clonar y trabajar en el proyecto localmente (VS Code)
1. **Clona el repositorio**: Ejecuta el siguiente comando en tu terminal para clonar el repositorio:
   ```bash
   git clone https://github.com/kratoscordoba7/VCP1.git
   ```
2. Una vez clonado, todos los archivos han de estar situado en el environment del paso 1

### Paso 3: Abrir Anaconda prompt y activar el envioroment:
   ```bash
   conda activate NombreDeTuEnvironment
   ```
Tras estos pasos debería poder ejecutar el proyecto localmente

---

<h2 align="center">📋 Tareas</h2>

### Tarea 1 Tablero de ajedrez

Crear una imagen de 800x800 píxeles con la textura de un tablero de ajedrez utilizando funciones de `numpy` y `matplotlib`. La imagen será en escala de grises (0 negro, 255 blanco). Además, modificar el color de los cuadros para que sean verdes.

Para crear una imagen con un efecto de tablero de ajedrez, es fundamental tener en cuenta dos aspectos clave: la posición de las casillas y su tamaño. La coloración de cada casilla (blanca o negra) se basa en la suma de los índices de las filas (i) y las columnas (j). Por tanto, cuando la suma de los indices sea par se pintará la casilla de blanco (tener en cuenta que partimos de una imagen totalmente negra). El resultado que se obtiene es de un tablero de ajedrez donde las casillas pares son blancas y las impares negras.

<table align="center">
   <td width="50%">
      <h3 align="center">♟️ Tablero de ajedrez</h3>
      <div align="center">
      <img src="https://github.com/user-attachments/assets/3996c73a-4281-4acc-9cc4-7efc2725061a" width="400" height="355" alt="Tablero de ajedrez">
   </td>
   <td width="50%">
      <h3 align="center">♟️ Tablero de ajedrez verde</h3>
      <div align="center">                                       
      <img src="https://github.com/user-attachments/assets/8da19385-fa10-48ab-beb6-154c0a31f192" width="400" height="355"  alt=" Tablero de ajedrez verde"></a>
   <br>                                                 
</table>

A continuación, se muestra un fragmento de código que lo ilustra:

```python
def aplicar_color_casilla(color_img, i, j, tamaño_casilla, color=255):
    if (i + j) % 2 == 0:
        color_img[i * tamaño_casilla:(i + 1) * tamaño_casilla, j * tamaño_casilla:(j + 1) * tamaño_casilla] = color
```

### Tarea 2 Mondrian

Crear una imagen con estilo Mondrian. Para esta tarea se ha realizado un generador aleatorio de cuadros con estilo Mondrian. Para conseguirlo, se ha tomado aleatoriedad en cuanto a el color, alto y ancho de cada rectángulo pintado. Se recorre toda la imagen mediante dos bucles while, hay que tener en cuenta que cuando se pinte un rectángulo de anchura K el indice para el próximo rectángulo debe ser el actual + k. Uno de los mayores problemas que se encontró durante el desarrollo de esta tarea fue la situación de las líneas negras:
         
         - Líneas a la derecha de cada rectángulo: se pinta por dentro del rectángulo, de hacerse por fuera el próximo rectángulo sobreescribiría la línea con otro color
         - Líneas por debajo de cada rectángulo: Esto cubre la posibilidad de que haya rectángulos más pequeños que la altura de la siguiente fila
         - Linéas al final de cada línea: cuando se llega al final, es decir al ancho de la imagen se salta a la próxima fila de ser posible. Antes de hacerlo, se pinta una raya negra y se hace por dentro para que
                                          los rectángulos nuevos no puedan sobreescribirla.

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/7cee482b-4119-4ab1-89db-09c13c095bbd" width="200" height="280" ></td>
</table>

A continuación, se muestra un fragmento de código que lo ilustra:

```python
while posicionY < alto:
    while posicionX < ancho:
        # Se pinta un rectángulo empezando a la derecha del anterior
        color_img[posicionY:posicionY + alto_rect, posicionX:posicionX + ancho_rect, :] = color_rect
        # Se pinta una raya negra de ancho 10 desde la esquina superior derecha del cuadrado hasta la parte inferior de la imagen (por dentro)
        color_img[posicionY:alto, posicionX + ancho_rect - 10:posicionX + ancho_rect, :] = [0,0,0]
        # Se pinta una raya negra del ancho del cuadrado y de altura 10 debajo del cuadrado (por fuera)
        color_img[posicionY + alto_rect:posicionY + alto_rect + 10, posicionX:posicionX + ancho_rect, :] = [0,0,0]
        posicionX += ancho_rect # Se avanza la posición hasta la esquina superior derecha del rectángulo para comenzar en ese punto al crear el siguiente
        # Se escogen nuevos color, alto y ancho para el siguiente rectángulo
        color_rect, alto_rect, ancho_rect = colores[random.randint(0, len(colores)-1)], tamaños[random.randint(0, len(tamaños) - 1)], tamaños[random.randint(0, len(tamaños) - 1)]
```

### Tarea 3 Funciones de dibujo de OpenCV

Recrear una de las tareas anteriores utilizando las funciones de dibujo de OpenCV. En este caso, se optó por recrear lo que realizamos en la tarea uno, es decir, la creación de un tablero de ajedrez, utilizando las funciones de OpenCV. Para ello, se empleó la función `cv2.rectangle`, que permite dibujar los rectángulos que componen el tablero, alternando los colores para representar las casillas. La lógica implícita en esta tarea es la misma vista en la tarea uno pero haciendo uso de una función distinta.

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/dac8c5a2-0fde-4063-acff-81db9015891d" width="300" height="280" ></td>
</table>

A continuación, se muestra un fragmento de código que lo ilustra:

```python
for i in range(alto // tamaño_casilla):
    for j in range(ancho//tamaño_casilla):
        # Dibujar el rectángulo blanco si la suma de i + j es par (para alternar)
        if (i+ j) % 2 == 0:
            cv2.rectangle(color_img,
                          (j * tamaño_casilla, i * tamaño_casilla),
                          ((j + 1) * tamaño_casilla, (i + 1) * tamaño_casilla),
                          (255, 255, 255), -1
```


### Tarea 4 Modificar valores de un plano de la imagen

Primero, hemos realizado modificaciones en el plano de diversas imágenes utilizando las bibliotecas Matplotlib, NumPy y OpenCV. Tomamos una imagen en color e invertimos sus colores. Es importante convertir la imagen de BGR a RGB antes de realizar la inversión.

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/28b5a22b-467e-499a-8853-7f6d17ebb6c3" width="600" height="280" ></td>
</table>
   
A continuación, se muestra un fragmento de código que ilustra este proceso:

```python
# Convertir la imagen de BGR a RGB (OpenCV usa BGR por defecto, matplotlib usa RGB)
color_img_rgb = cv2.cvtColor(color_img, cv2.COLOR_BGR2RGB)

# Invertir los colores
inver_img_rgb = 255 - color_img_rgb 
```


La siguiente modificación que realizaremos será aplicar un desenfoque gaussiano al plano. Para desenfocar la imagen utilizando OpenCV, simplemente empleamos el método `cv2.GaussianBlur`. 

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/f3c16946-1179-4c31-a8b1-a3d00169292a" width="700" height="280" ></td>
</table>

A continuación se muestra un ejemplo de cómo aplicar este desenfoque gaussiano a una imagen:

```python
# Aplicar un desenfoque Gaussiano a la imagen en escala de grises
blurred_image = cv2.GaussianBlur(color_img, (5, 5), 0)
```

La siguiente modificación consiste en aumentar el contraste de la imagen y detectar sus bordes. Es importante tener en cuenta que para detectar los bordes en la imagen utilizamos el método `cv2.Canny`, proporcionado por OpenCV. Además, para asegurarnos de que los valores de los píxeles se encuentren en el rango adecuado después de aumentar el contraste, debemos utilizar los métodos `np.clip()` y `astype(np.uint8)`.

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/2f19d6eb-9bfd-4f57-bf5c-20ee4aed3df0" width="700" height="280" ></td>
</table>

A continuación, se muestra cómo puedes llevar a cabo estos ajustes en la imagen:

```python
# Ajustar el contraste de la imagen
alpha = 2.5  # Factor de contraste
contrast_image = np.clip(alpha * color_img, 0, 255).astype(np.uint8)

# Aplicar la detección de bordes usando el filtro Canny
edges = cv2.Canny(color_img, 140, 180) 
```

Como podemos observar, al dividir los valores de la imagen por un factor, la imagen se oscurece. En este caso, hemos dividido todos los valores por cuatro, y cuanto mayor sea el valor por el que dividimos, más oscura se vuelve la imagen. 

Para asegurarnos de que los valores resultantes se mantengan dentro del rango válido de 0 a 255 y evitar posibles errores, hemos utilizado el método `np.clip`. También realizamos una inversión de colores. Para ello, hemos manipulado los valores RGB de la imagen sumando o restando los componentes de color para invertir la imagen. 

Por último, hemos aplicado la operación del módulo a la imagen. Como podemos observar, cuanto mayor sea el valor del módulo, más intensamente se representará el color en la imagen. Esto se debe a que el módulo permite ajustar la amplitud de los valores de los píxeles, haciendo que las diferencias de color sean más notables.

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/70b6c91e-274d-446a-95ea-5c7652686590" width="600" height="280" ></td>
</table>

Aquí tienes un ejemplo de cómo hacerlo:

```python
# Separar los canales
red = color_img_rgb[:,:,0]
green = color_img_rgb[:,:,1]
blue = color_img_rgb[:,:,2]

# División
r_div = np.clip(red / 4, 0, 255)
g_div = np.clip(green  / 4, 0, 255)  
b_div = np.clip(blue / 4, 0, 255) 

# Se crea una imagen con los planos divididos
div_img = cv2.merge((r_div.astype(np.uint8), g_div.astype(np.uint8), b_div.astype(np.uint8)))
```

A continuación, se muestra un ejemplo de cómo llevar a cabo la inversión de colores en una imagen RGB:

```python
# Inversión de color
red_inverted = np.clip(red + green, 0, 255)
green_inverted = np.clip(green - blue, 0, 255)
blue_inverted = np.clip(blue + red, 0, 255)

# Se crea una imagen con los planos invertidos
inverted_img = cv2.merge((red_inverted.astype(np.uint8), green_inverted.astype(np.uint8), blue_inverted.astype(np.uint8)))

```
Ejemplo de cómo aplicar la operación del módulo en una imagen:

```python
# Módulo
r_mod = np.clip(red % 256, 0, 255)
g_mod = np.clip(green % 128, 0, 255)
b_mod = np.clip(blue % 64, 0, 255)

# Se crea una imagen con los planos módulo
mod_img = cv2.merge((r_mod.astype(np.uint8), g_mod.astype(np.uint8), b_mod.astype(np.uint8)))
```

También aplicamos los cambios de valor de los planos en tiempo real utilizando la webcam. Esto nos permite ver cómo se modifican las imágenes directamente desde la cámara, aplicando las técnicas de procesamiento de imagen que mencionamos anteriormente.

```python
r = r + g
g = g - b
b = b + r

# Ajustamos los valores a un rango válido [0, 255]
r = np.clip(r, 0, 255)
g = np.clip(g, 0, 255)
b = np.clip(b, 0, 255)   
```

Aqui un ejemplo con la camara web cam:

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/c090a18a-e45d-4166-bd30-f684abf65c00" width="650" height="180" ></td>
</table>

### Tarea 5 Pixel más claro y oscuro de la imagen

Dibujar círculos en las posiciones del píxel más claro y oscuro de la imagen. Si se quiere hacer sobre la zona 8x8 más clara/oscura, ¿cómo se haría?

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/8048d6b1-07c2-4cbe-89a5-eede2b2110f8" width="600" height="280" ></td>
</table>

```python
# Encontrar los píxeles más claro y más oscuro
min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(gray_img)

# Dibujar círculos y una línea entre los puntos
cv2.circle(color_img, max_loc, 10, (255, 255, 0), -1)  
cv2.circle(color_img, min_loc, 10, (0, 255, 255), -1)  
cv2.line(color_img, min_loc, max_loc, (255, 255, 0), 2)
```

Para aplicar el mismo proceso de detección de los píxeles más claros y oscuros en una transmisión en vivo desde la cámara web, y luego visualizar los resultados en una ventana en tiempo real, puedes seguir el siguiente enfoque. 

```python
if ret:
   # Convertir el fotograma a gris
   gray_vid = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
        
   # Encontrar los píxeles más claro y más oscuro
   min_val, max_val, min_loc, max_loc = cv2.minMaxLoc(gray_vid)
        
   # Dibujar
   cv2.circle(frame, max_loc, 10, (255, 255, 0), -1)
   cv2.circle(frame, min_loc, 10, (0, 255, 255), -1)
   cv2.line(frame, min_loc, max_loc, (255, 255, 0), 2)
        
   cv2.imshow('Detectar zona oscura y clara', frame)
```

Aqui un ejemplo con la camara web cam:

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/22c64516-5066-4289-a8ab-d32537606586" width="350" height="280" ></td>
</table>

Para detectar las zonas más claras y oscuras en un bloque de 8x8 píxeles dentro de un vídeo en tiempo real, puedes seguir una metodología similar a la que ya hemos utilizado con imágenes estáticas, pero aplicándola a cada fotograma del vídeo.

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/a39a13c2-0cc2-48df-8f3d-9339fceebe2a" width="400" height="290" ></td>
</table>

Ejemplo para detectar la región de 8x8 píxeles más clara y más oscura en cada fotograma de un vídeo:

```python
def find_clear_and_darkest_regions(gray_img, block_size=8):
    h, w = gray_img.shape

    # almacenar la suma máxima y mínima de intensidades
    min_sum = 255 * block_size * block_size  # Valor máximo posible para una región de 8x8
    max_sum = 0

    # Buscando la región de 8x8 píxeles con la suma máxima y mínima
    for y in range(0, h - block_size + 1):
        for x in range(0, w - block_size + 1):
            region = gray_img[y:y+block_size, x:x+block_size]
            region_sum = np.sum(region)
                    
            if region_sum > max_sum:
                max_sum = region_sum
                max_loc = (x + block_size // 2, y + block_size // 2)
                
            if region_sum < min_sum:
                min_sum = region_sum
                min_loc = (x + block_size // 2, y + block_size // 2)

    return min_loc, max_loc
```

Al final del proceso, tanto en el video como en la imagen final, deberemos invocar el método creado para  detectar la región de 8x8 píxeles más clara/oscura y dibujar los círculos/líneas.

```python
# Encontrar las regiones más clara y más oscura
min_loc, max_loc = find_clear_and_darkest_regions(gray_img_mondrian, block_size=8)

# Dibujar círculos y una línea entre los puntos
cv2.circle(color_img_mondrian, max_loc, 4, (255, 255, 0), -1)  # Región más clara en amarillo
cv2.circle(color_img_mondrian, min_loc, 4, (0, 255, 255), -1)  # Región más oscura en cyan
cv2.line(color_img_mondrian, min_loc, max_loc, (255, 255, 0), 1)  # Línea entre las regiones
```

Aqui un ejemplo con la camara web cam:

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/13d3849b-b00a-4a58-83b0-a45184302482" width="250" height="180" ></td>
</table>


### Tarea 6 Pop Art

Realizar una propuesta propia de estilo Pop Art. En nuestro caso, decidimos recrear la obra "Marilyn Pop Art" de Andy Warhol, donde partimos de una imagen original y generamos nueve versiones con diferentes variaciones de color. Esto le da un aspecto muy similar a la obra original, capturando la esencia del estilo característico de Warhol, con sus icónicas repeticiones y cambios de color.

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/e946bf1c-8a7e-4355-8873-4419463ff575" width="290" height="290" ></td>
</table>

Esta función toma una imagen, la convierte a HSV, ajusta el tono (hue) según el valor hue_shift, y luego la convierte nuevamente a RGB. Esto permite cambiar el color percibido sin alterar la saturación o el brillo.

```python
# Función para ajustar el tono (hue) de la imagen
def change_hue(image, hue_shift):
    # Convertir la imagen a modo HSV para modificar el hue
    img_hsv = image.convert('HSV')
    np_img = np.array(img_hsv)

    # Cambiar el hue (primer canal en HSV) agregando un valor de cambio
    np_img[:, :, 0] = (np_img[:, :, 0].astype(int) + hue_shift) % 255  # Cambio de hue
    img_hue_shifted = Image.fromarray(np_img, 'HSV')

    # Volver a convertir la imagen a modo RGB
    return img_hue_shifted.convert('RGB')
```

Aqui un ejemplo con la camara web cam:

<table align="center">
   <td><img src="https://github.com/user-attachments/assets/d992d0be-825d-4cb4-ab89-c952256ef5d8" width="350" height="280" ></td>
</table>


---

> [!IMPORTANT]  
> Los archivos presentados aquí son una modificación de los archivos originales de [otsedom](https://github.com/otsedom/otsedom.github.io/tree/main/VC).



---

## 📚 Bibliografía

1. [Opencv](https://docs.opencv.org/4.x/dc/da5/tutorial_py_drawing_functions.html)
2. [Mondrian](https://www3.gobiernodecanarias.org/medusa/ecoescuela/sa/2017/04/17/descubriendo-a-mondrian/)
3. [Marilyn POP ART](https://temasycomentariosartepaeg.blogspot.com/p/autor-andy-warhol-1928-1987-titulo.html)
4. [Online OpenCV Compiler](https://python-fiddle.com/examples/opencv)
5. [Stackoverflow type np uint8](https://stackoverflow.com/questions/64314899/how-does-numpy-astypenp-uint8-convert-a-float-array-1-2997805-became-255)
6. [Stackoverflow how to change hue](https://stackoverflow.com/questions/67448555/python-opencv-how-to-change-hue-in-hsv-channels)
7. [Stackoverflow how to cv2 minmaxloc](https://stackoverflow.com/questions/53292170/how-to-use-the-cv2-minmaxloc-in-template-matching)
8. [GeeksforGeeks splitting and merging channels](https://www.geeksforgeeks.org/splitting-and-merging-channels-with-python-opencv/)

---

**Universidad de Las Palmas de Gran Canaria**  

EII - Grado de Ingeniería Informática  
Obra bajo licencia de Creative Commons Reconocimiento - No Comercial 4.0 Internacional

---
