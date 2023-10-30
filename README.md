---------------------------------------Creacion de la imagen de docker-------------------------------------------------

En primer lugar deberas de generar la imagen docker del proyecto, esto se hace atraves del siguiente comando:

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/e54de65a-f2bd-403e-a1eb-c57a992d570e)

Al dirigirte a docker desktop deberias poder ver la imagen creada:

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/6ab800fa-9cad-49c8-9b77-d3e9c2f3d7c1)

Podemos revisar que efectivamente se creo la imagen, atraves del siguiente comando:

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/d2b0ea17-5711-4a40-88fa-2a3f28a0d9e6)


Revisamos que efectivamente se encuentra creada la imagen "awsspak":

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/afb531ab-1ae0-4d8a-a4fb-60ec38be523b)



Creamos un instancia de un contenedor de la imagen "awsspark", con el proposito de verificar que el proyecto funciona correctamente:
Para este caso mapeamos el puerto fisico 3000 al puerto 6000 de docker

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/296d429e-3fbe-4952-9e50-f75fe18334ad)


Al ejecutar el comando, se puede observar como respuesta el id de dicho contenedor

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/e991c86f-e92c-4382-af0b-8f4ae9985e34)


Ahora, revisamos en el aplicativo desktop de docker para comprobar que efectivamente se creo satisfactoriamente la instancia del contenedor:

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/389b4b26-2a6a-4468-87b6-ff82653a4c69)

El contenedor se esta ejecutanto correctamente de forma local, para este caso en particular, revisamos la siguiente direccion: http://localhost:3000/hello

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/0dd74811-d040-4d0c-a297-6a1a6656cd3f)

Como se observa, la ejecucion de la instancia del contenedor esta ejecutandose correctamente.


---------------------------Virtualizacion en AWS---------------------------------------------------------

En este punto podemos subir la imagen a dockerHub y proceder con los servicios de virtualizacion de AWS. 
Por otro lado, en mi caso, ya tengo subida la imagen del proyecto a dockerHub, esta se encuentra en el siguiente enlace: https://hub.docker.com/r/blutlucifugekrieger/sparkprojectcamilocastro

Al acceder al enlace podrias ver lo siguiente: 

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/ecc220df-156e-43f9-96ef-2fea55f9e6b1)


Una vez, se tenga en cuenta ese repositorio de dockerHub, se podra acceder a AWS y crear la maquina virtual junto con la key de acceso,
por otro lado, se tendra que conectar a su maquina virtual, e instalar docker, una vez esto este realizado, solo bastara con crear una instancia del contenedor de la imagen subida al repostorio en dockerHub.

Vista de la maquina virtual creada apartir del servicio EC2 de AWS
![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/c7673493-8496-42a9-8f44-5dd852434989)

Con esto en cuenta, te conectaras a tu maquina virtual, y finalmente, emplearas el comando "docker ps" para revisar la instancia del contenedor que se esta ejecutando:

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/ef7eb828-a642-4625-a68f-a6629c0ebecb)

En mi caso, aun no estoy ejecutando ninguna instancia de un contenedor:

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/680640be-bee4-4920-96c0-fd43afdc5573)

Por ende, debo de crear la instancia, pero dicha instancia ya la cree hace unos dias, entonces para revisar si efectivamente esa instancia fue creada empleo el comando:

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/1921ebde-a1ed-4316-8a98-e08ba5310611)

Despues, al ejecutar este comando, obtengo como resultado todas las instancias que he creado, incluso aquellas que no se esten ejecutando:


![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/45baa345-ed91-46f3-8e84-0b8671aec896)

En mi caso, voy a inicializar la instancia de id "d69653587e36", que es la que tiene mapeado el puerto fisico 42000 al puerto 6000 de docker,
para inicializar la instancia del contenedor, debo de emplear el siguiente comando:

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/9cf336c8-9267-436b-b270-ee46018c2c75)

Al ejecutar el comando "docker ps", obtendremos las instancias que se estan ejecutando, es decir la instancia "d69653587e36":

![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/9308ef75-7dda-4fd3-987e-4b8623230e93)

Finalmente, accedemos a la ejecucion del servicio docker en el navegador de preferencia, esto se realiza atraves de la direccion DNS publica de la maquina virtual:
![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/35145cdb-2eff-431a-84bf-bc2b0dff0d7b)

Pegamos en el navegador la direccion DNS y la decoramos con el puerto en donde la maquina virtual esta escuchando (42000), junto a su vez, con la direccion "/hello" definido en la clase main del proyecto.
Obtendriamos algo como esto:
![image](https://github.com/BlutLucifugeKrieger/spark-aws-camilocastro/assets/130005378/df58b3bb-8721-43a3-8f2f-94a944a76bbe)
