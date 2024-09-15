<h1 align="center">🌟 Práctica 1 - Visión por Computador (Curso 2024/2025)</h1>

<img align="left" width="160" height="160" src="https://github.com/user-attachments/assets/b279b85c-7ae5-4f07-bc42-ec238591eaf0"></a>
Se han completado todas las tareas solicitadas de la **Práctica 1** para la asignatura **Visión por Computador**. Primeros pasos con OpenCV.

*Trabajo realizado por*:

[![GitHub](https://img.shields.io/badge/GitHub-Heliot%20J.%20Segura%20Gonzalez-purple?style=flat-square&logo=github)](https://github.com/kratoscordoba7)

[![GitHub](https://img.shields.io/badge/GitHub-Alejandro%20David%20Arzola%20Saavedra%20-blue?style=flat-square&logo=github)](https://github.com/AlejandroDavidArzolaSaavedra)

## 🛠️ Librerías Utilizadas

[![NumPy](https://img.shields.io/badge/NumPy-%23013243?style=for-the-badge&logo=numpy)](Link_To_Your_NumPy_Page)
[![OpenCV](https://img.shields.io/badge/OpenCV-%23FD8C00?style=for-the-badge&logo=opencv)](Link_To_Your_OpenCV_Page)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-%43FF6400?style=for-the-badge&logo=matplotlib&logoColor=white)](Link_To_Your_Matplotlib_Page)


---

<h2 align="center">📋 Tareas</h2>

### Tarea 1 Tablero de ajedrez

Crear una imagen de 800x800 píxeles con la textura de un tablero de ajedrez utilizando funciones de `numpy` y `matplotlib`. La imagen será en escala de grises (0 negro, 255 blanco). Además, modificar el color de los cuadros para que sean verdes.

Para crear una imagen con un efecto de tablero de ajedrez, es fundamental tener en cuenta dos aspectos clave: la posición de las casillas y su tamaño. La coloración de cada casilla (blanca o negra) se basa en la suma de los índices de las filas (i) y las columnas (j).

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
Crear una imagen con estilo Mondrian.

### Tarea 3 Funciones de dibujo de OpenCV
Recrear una de las tareas anteriores utilizando las funciones de dibujo de OpenCV.

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

### Tarea 6
Realizar una propuesta propia de estilo Pop Art.

---

## 🚀 Cómo empezar

Para comenzar con el proyecto, sigue estos pasos:

1. Clona el repositorio:
   ```bash
   git clone https://github.com/kratoscordoba7/VCP1.git
   ```
2. Abre el proyecto en VS Code.
3. Navegar por las tareas e ir siguiendo las instrucciones.

---

## 🤝 Contribuciones

Si deseas contribuir a este repositorio, por favor sigue estos pasos:

<img align="left" width="200" height="180" src="https://github.com/AlejandroDavidArzolaSaavedra/CNN-CT-BRAIN/assets/90756437/3bf833fa-828e-467c-89b8-0ea4a077d3ea">

1. Haz un fork del repositorio.
2. Crea una nueva rama para tus cambios: `git checkout -b feature/nueva-caracteristica`.
3. Realiza tus cambios y haz un commit: `git commit -m "Añadir nueva característica"`.
4. Envía tus cambios a tu repositorio forked: `git push origin feature/nueva-caracteristica`.
5. Crea un pull request explicando tus cambios.


---

## ⚠️ Aviso

Los archivos presentados aquí son una modificación de los archivos originales de [otsedom](https://github.com/otsedom/otsedom.github.io/tree/main/VC).

---

## 📚 Bibliografía

1. [Opencv](https://docs.opencv.org/4.x/dc/da5/tutorial_py_drawing_functions.html)
2. [Mondrian](https://www3.gobiernodecanarias.org/medusa/ecoescuela/sa/2017/04/17/descubriendo-a-mondrian/)
3. [Marilyn POP ART](https://temasycomentariosartepaeg.blogspot.com/p/autor-andy-warhol-1928-1987-titulo.html)
4. [Online OpenCV Compiler](https://python-fiddle.com/examples/opencv)
5. [Stackoverflow](https://stackoverflow.com/questions/64314899/how-does-numpy-astypenp-uint8-convert-a-float-array-1-2997805-became-255)


---

**Universidad de Las Palmas de Gran Canaria**  

EII - Grado de Ingeniería Informática  
Obra bajo licencia de Creative Commons Reconocimiento - No Comercial 4.0 Internacional

---
