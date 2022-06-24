# Práctica 7. Conectar 2 VM con subredes

Es importante que los recursos creados en esta práctica se encuentren en la misma región para que puedan conectarse.

## Crear dos redes virtuales

Buscamos las redes virtuales en la barra de búsqueda y creamo una.

![p7p1](imagenes\p7p1.png)

Configuramos la red virtual con los siguientes parámetros:
- Suscripción
- Grupo de recursos: sesion5
- Nombre: redvirtual1
- Región: Australia Central

![p7p2](imagenes\p7p2.png)

En el apartado de dierección IP eliminamos la red que viene por default y agragamos una subred.

![p7p3](imagenes\p7p3.png)

Para agregar la subred agregamos los parámetros:
- Nombre de la subred: subnet1
- Intervalo: 10.0.0.0/24

![p7p4](imagenes\p7p4.png)

Creamos una segunda red virtual, con los parámetros:
- Suscripción
- Grupo de recursos: sesion5
- Nombre: redvirtual2
- Región: Australia Central

![p7p5](imagenes\p7p5.png)

Nuevamente configuraremos una subnet para la red virtual nueva:
- Nombre de la subred: subnet2
- Intervalo: 10.1.0.0/24

![p7p6](imagenes\p7p6.png)

-------------------------------------------

## Creación de las máquinas virtuales

En la barra de búsqueda de Azure buscamos las máquinas virtuales.

![p7p7](imagenes\p7p7.png)

Creamos la máquina virtual con los siguientes parámetros:
- Grupo de recursos: sesion5
- Nombre: maquinavirtual1
- Región: Australia Central
- Imagen: Ubuntu Gen2
- Tamaño: Standard_DS1_v2
- Contraseña

![p7p8](imagenes\p7p8.png)

Es importanque que configuremos con usuario y contraseña para poder ingresar a las máquinas virtuales. Los demás parámetros los dejaremos como están.

![p7p9](imagenes\p7p9.png)

En el apartado de Redes configuramos la redvirtual1 y la subnet1

![p7p10](imagenes\p7p10.png)

Creamos una segunda red virtual modificando los mismos parámetros:
- Grupo de recursos: sesion5
- Nombre: maquinavirtual2
- Región: Australia Central
- Imagen: Ubuntu Gen2
- Tamaño: Standard_DS1_v2
- Contraseña

![p7p11](imagenes\p7p11.png)

Nuevamente, es importante configurar las máuinas virtuales con usuario y contraseña para poder acceder a ellas.

![p7p12](imagenes\p7p12.png)

En el apartado de redes configuramos la redvirtual2 y la subnet2.

![p7p13](imagenes\p7p13.png)

----------------------------------

## Conexión de las máquinas virtuales

### Iniciar la máquina virtual en Ubuntu

Entramos a la primer máquina virtual y seleccionamos Conectar SSH.

![p7p14](imagenes\p7p14.png)

En el punto número 4 copiamos la ruta de acceso privada, en este caso: karen@20.213.245.134.

![p7p15](imagenes\p7p15.png)

Abrimos la terminal de Cloud Shell, ubicada en la parte superior de Azure.

![p7p16](imagenes\p7p16.png)

Seleccionamos Bash ya que haremos la implementación en Ubuntu.

![p7p17](imagenes\p7p17.png)

Ingresamos el comando _ssh_ seguido de la ruta de acceso privada que copiamos. Escribimos _yes_ e ingresamos la contraseña de nuestra primer máquina virtual.

![p7p18](imagenes\p7p18.png)

Una vez que hemos ingresado a Ubuntu podemos hacer una prueba con el comando _sudo apt-get moo_, nos aparecerá una vaquita. 

![p7p19](imagenes\p7p19.png)

### Emparejamiento de redes
Para poder conectar las máquinas primero iremos a la redvirtual1 y seleccionamos _Emparejamiento_.

![p7p20](imagenes\p7p20.png)

Agregamos un emparejamiento y en el nombre del vínculo de emparejamiento de esta red escribimos: redvirtual1-redvirtual2.

![p7p21](imagenes\p7p21.png)

En el nombre del vínculo de emparejamiento de la red remota escribimos: redvirtual2-redvirtual1.

![p7p22](imagenes\p7p22.png)

Llenamos los otros aspectos que se nos pide:
- Suscripción.
- Red virtual: redvirtual2

![p7p23](imagenes\p7p23.png)

Cuando las redes virtuales se conecten escribimos el comando _ping 10.1.0.4_ (dirección IP de la segunda máquina virtual) y veremos como inicia la transferencia de datos; para detenerla, en mi caso, hice uso de Ctrl+Z.

![p7p25](imagenes\p7p25.png)

------------------------------

## Extra

Recursos que se crearon:
- Máquina virtual: para la VM 1 y 2
- Dirección IP pública: para la VM 1 y 2
- Grupo de seguridad de res: para la VM 1 y 2
- Interfaz de red normal: para la VM 1 y 2
- Disco: ra la VM 1 y 2

![p7p26](imagenes\p7p26.png)

![p7p27](imagenes\p7p27.png)

- Red virtual 1
- Red virtual 2

![p7p28](imagenes\p7p28.png)