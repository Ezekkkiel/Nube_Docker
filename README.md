# Nube_Docker

## Preguntas

1. ¿Por qué el frontend no necesita conectarse a PostgreSQL?
Porque solo habla con el backend mediante su API. Es el backend quien accede a la base de datos, de modo que PostgreSQL queda fuera de su alcance.

2. ¿Por qué el backend pertenece a dos redes?
Porque debe comunicarse con el frontend y con PostgreSQL, actuando de puente entre ambos.

3. ¿Qué servicio necesita publicar un puerto en el anfitrión?
El frontend, porque es el único al que deben acceder los usuarios desde fuera.

4. ¿Por qué publicar PostgreSQL hacia fuera no es la solución adecuada para un fallo de comunicación interno?
Porque el fallo es de comunicación entre contenedores, que se resuelve con redes y nombres de servicio internos, y exponer PostgreSQL añadiría un riesgo de seguridad sin corregir la causa.

5. ¿Qué ventaja ofrece Docker Compose respecto a ejecutar los tres contenedores manualmente?
Permite definir y levantar los tres contenedores, con sus redes, volúmenes y variables, desde un único archivo y con un solo comando, de forma reproducible.

6. ¿Por qué hemos dividido la arquitectura en dos redes?
Para aislar la base de datos: el frontend no comparte red con PostgreSQL, lo que reduce la superficie de ataque y aplica el principio de mínimo privilegio.

7. ¿Por qué el backend utiliza db como dirección de PostgreSQL?
Porque db es el nombre del servicio en Compose y el DNS interno de Docker lo resuelve a la IP del contenedor, sin depender de direcciones IP que pueden cambiar.

8. ¿Qué diferencia existe entre detener un proyecto y eliminar sus volúmenes?
Detener el proyecto (docker compose down) elimina contenedores y redes pero conserva los volúmenes y los datos; eliminar los volúmenes (down -v) borra además los datos de forma permanente.

9. ¿Qué consecuencias tendría para la empresa perder el volumen de PostgreSQL?
Se perderían todos los datos almacenados (clientes, pedidos, etc.), con interrupción del servicio, posibles pérdidas económicas e incumplimientos legales, salvo que existan copias de seguridad.
