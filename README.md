# Práctica de Azure Logic Apps para encontrar el sentimiento de Tweets.

![Logic Apps Icon](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/logic-apps.png)

## Breve descripción
Logic Apps es un servicio de tipo [PaaS](https://azure.microsoft.com/es-mx/overview/what-is-paas/) y [Serverless](https://azure.microsoft.com/en-us/solutions/serverless/#overview) que se ejecuta en la [nube](https://azure.microsoft.com/es-mx/overview/what-is-the-cloud/) de Azure y ésta  permite hacer microservicios o API's como [Azure Functions](https://azure.microsoft.com/en-us/services/functions/#features), pero con las diferencias en que no se ejecuta por llamada, sino que este servicio se mantiene siempre activo para realizar la automatización de procesos de negocio gracias a el uso de conectores prestablecidos y/o personalizados, según la problemática lo implique y, tiene una forma *"visual"* para trabajar sobre sus acciones. Se encuentra en el [portal de Azure](https://portal.azure.com/#home). Para más información, se puede consultar los siguientes enlaces:   
- [Documentación de Microsoft](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-overview)
- [Documentación de Azure](https://azure.microsoft.com/en-us/services/logic-apps/) 


-----------
## Requisitos
 - Tener una cuenta de Azure para realizar la práctica en su [Portal](https://portal.azure.com/#home) (si aún no se cuenta con alguna, se puede hacer el registro en el siguiente [enlace](https://azure.microsoft.com/es-mx/free/)). Esto es ya que el recurso de la Azure Logic Apps está hecha para hacerse como pago por uso por evento. Es decir, se paga por lo que se consume.
 - Contar con una suscripción activa de Azure para poder realizar la práctica. 

----------

## Instrucciones

Esta práctica es similar a otra [(Azure Functions)](https://github.com/JohnNadja/Practica-Azure-Functions); sin embargo y, como se menciona anteriormente, tiene unas ligeras diferencias en su creación y ejecución.

1. Entrar a la [página de Azure](https://portal.azure.com/#home) y buscar  la opción **Azure Logic Apps**.

2. En la página de Azure Logic Apps, seleccionar la opción **Crear** y aparecerá un panel de Datos básicos.
![2.1](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/2.1.gif)
    - Nos importarán realizar acciones en los siguientes parámetros:

        | Parámetro | Descripción |
        | ---------- | ----------- |
        |Grupo de recursos|Seleccionar el grupo de recursos al que se le asingnará a nuestro servicio. Si no existe, se puede crear uno. Ejemplo: PrácticaLogics|
        |Nombre|Introducir el nombre de la instancia nueva|
        |Región|Seleccionar la región más cercana que esté disponible|
        |Tipo de Plan|Seleccionar la opción **Consumo** para esta práctica|
    
    - Esperamos a que cree cuando se activa la opción de "Revisar y crear".
    ![2.2](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/2.2.gif)
    ![2.3](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/2.3.png)

3. Una vez creada la función, se ingresa al recurso.
![3.1](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/3.1.gif)
    - Como se puede observar, tiene una interfaz peculiar (nota: sino aparece, simpelemente se vuelve a buscar el recurso que se creó, no el grupo de recursos). Dicha interfaz es la que se había mencionado para visualizar las operaciones de Azure Logic Apps.
    - Se creará una nueva aplicación lógica en blanco. Dicha aplicación, necesita un "Trigger", que será ***Twitter***.
    ![3.2](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/3.2.gif)
    - En el apartado de **Nombre de la conexción**, asignamos un nombre que identifique la conexión e iniciamos la sesión con nuestra cuenta de Twitter pulsando el botón de *Iniciar sesión*.
    - Aparecerá una nueva ventana:
    ![3.3](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/3.3.png)
    
        | Parámetro | Uso |
        | ---------- | ----------- |
        |**Texto de búsqueda**|colocaremos un *Hashtag* para poder tener una base de datos. Para esta ocasión se usará el hashtag: ***#SummerGameFest***|
        |Frecuencia| Usaremos por cada **5** ***segundos***|

4. En una cuenta de Google, se creará dentro de su Drive un archivo de tipo ***Sheets*** (Hojas de cálculo) para poder alamcenar los twwets que se vayan capturando.


    - Debe tener el formato de la siguiente manera para establecer un orden conforme a las columnas:

        | ID Tweet | Tweeteado por | Texto del tweet | Localización | Sentimiento | Fecha |
        | ---------- | ----------- | ----------- | ----------- | ----------- | ----------- |
        
        ![4.1](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/4.1.png)

5. Volviendo a la instancia de la función nueva, buscaremos un nuevo paso, y éste será uno de tipo **Cognitive Services**. Escribimos en el campo de búsqueda *"text"* y seleccionamos las opciones como se muestran a continuación:
![5.1](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/5.1.gif)
*(Por el momento estará en "blanco")*

6. Se creará una nueva instancia de Azure, ésta es de tipo **Coginitive Services**. Se busca en el panel inicial del Portal de Azure. (nos servirá para ***analizar el sentimiento de los tweets***) Para ello, podemo abrir otra ventana del Portal de Azure.
![6.1](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/6.1.png)
    - Nos interesa *"Servicio de Lenguaje"* y hacemos clic en ***Crear***.
    - Seguimos los pasos como se muestra a continuación:
    ![6.2](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/6.2.gif)
        | Parámetro | Descripción |
        | ---------- | ----------- |
        | Grupo de recursos | Seleccionar el grupo de recursos en el que estamos realizando la práctica (PracticaLogics)|
        | Nombre | Introducir el nombre de la instancia nueva|
        | Plan de tarifa | Seleccionamos la opción gratuita (free)|
    - Esperamos a que se cree la instancia.
    - Una vez creada y accediendo a la instancia, nos ingresar al apartado de **Claves y puntos de conexión**. Ahí copiaremos la primera clave de acceso con el URL de la instancia.
    ![6.3](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/6.3.gif)
    - Se deben colocar tal clave y URL al parámetro del paso ***5***. Como se muestra, debemos también colocarle un nombre a ese paso.
    - Se tiene una actualización de panel:
    ![6.4](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/6.4.png)
    - Aquí buscaremos en el primer apartado el *"ID del tweet"* y en el segundo apartado estará la opción *"Texto del tweet"*.
    ![6.5](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/6.5.gif)
    - Se da clic en el botón de *"Nuevo paso"*.
    - En el campo de búsqueda, se escribe *"Sheets"* u *"Hojas de cálculo"* de Google para podeer acceder a la hoja de cálculo. que se creó anteriormente. 
    ![6.6](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/6.6.gif)
    - En los apartados siguientes (*"Archivo"* y *"Hoja de Cálculo*"), seleccionamos el archivo y la hoja de cálculo correspondiente (Nota: a veces no responde correctamente, así que se puede eliminar el paso y volver a crearlo usando los 3 puntos en la esquina superior derecha de dicho paso).
    - Una vez obtenido el archivo, se añaden los parametros que buscamos obtener:
    ![6.7](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/6.7.gif)
    [**EXTRA**] Si queremos que se vea o refleje de forma visual sin tener que revisar la hoja de cálculo, se puede hacer clic en el botón **Agregar una acción** y, por ejemplo, se puede añadir la aplicación Teams de Microsoft para publicar el contenido en un canal sleccionado.
    ![extra](https://github.com/JohnNadja/Practica-Logic-Apps/blob/main/images/extra.gif)

- Una vez creado todo, se pulsa el botón de **"Ejecutar desencadenador"** para que empiece a rastrear los tweets.

### Listo, ya está creado el servicio de Azure Logic Apps.

----
# **⚠Importante⚠**: 
### Recordar eliminar el grupo de recursos que se creó en Azure para evitar costos extras no deseados en caso de no ocupar el servicio.
Se puede hacer desde el panel de Azure en inicio y buscando el tipo de recurso que se llama **Grupo de Recursos**.


## Hasta aquí la finalización de la práctica.