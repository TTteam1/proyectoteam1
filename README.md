# Proyecto Team1

- Manuel Enrique Caita				
- Danny Alexander Riano Gomez				
- Luis Felipe Chacon				
- Carlos Alberto González Cardozo				

Despliegue de una arquitectura en AWS altamente disponible y escalable

## Planificacion

### Identificación de requerimientos.

#### Requerimientos de Negocio

El mundo de las letras

Expandiendo la pasión por la lectura al mundo digital.

La librería El mundo de las Letras es una librería física ubicada en Medellín con más de 20 años,
reconocida en la región por su amplia selección de libros en diferentes géneros y temas. Ha
servido como lugar de encuentro para amantes de la lectura y estudiantes de bachillerato y
universitarios donde además de disfrutar de la lectura o la experiencia de compra de libros,
pueden probar los deliciosos postres que se ofrecen.
El Mundo de las letras con gran experiencia en ventas y asesoría de libros reconociendo el cambio
en los hábitos de compra de los consumidores hacia el comercio electrónico, ha decidido expandir
su presencia en línea para llegar a un público más amplio y mantener su relevancia en un mercado
en constante evolución no solo nacional sino también internacional.

Para respaldar esa plataforma en línea se debe implementar la infraestructura en la nube de AWS
para ofrecer un rendimiento óptimo y una seguridad incomparable.

Dado que en la librería El mundo de las Letras adicionalmente a la expansión en línea
decidieron lanzar una campaña en Instagram para promocionar su vasto catálogo de libros, la
experiencia única de la librería y la variedad de postres. La campaña va a incluir publicaciones
patrocinadas, historias y anuncios dirigidos a usuarios interesados en la lectura y la cultura.
Además de la campaña en Instagram, la librería lanzará una campaña en Facebook para llegar a un
público más amplio y diverso. La campaña incluirá publicaciones en la página de la librería,
anuncio en el feed de noticias y anuncios dirigidos a grupos específicos de usuarios basados en sus
intereses y comportamientos en línea.
Para captar la atención de los usuarios que buscan activamente libros y contenido relacionado en
línea, la librería lanzará también una campaña en Google Ads. La campaña incluirá anuncios de
búsqueda relacionadas con libros y lectura en Google y Youtube.
El éxito de estas campañas de publicidad generará un aumento significativo en la visibilidad y el
interés por parte del público hacia la librería El Mundo de las Letras tanto en su tienda física como
en su plataforma en línea.
Se debe prever que el aumento de tráfico puede afectar la experiencia de usuario de la plataforma
en línea y ha identificado la necesidad de mejorar y escalar la infraestructura tecnológica para
satisfacer la demanda creciente y mantener la experiencia positiva de los clientes en línea.

#### Requerimientos Funcionales:

La infraestructura a implementar debe contar con lo siguiente:
* Desarrollar la plataforma web que permita a los clientes explorar los diferentes libros.
* Implementar la red en la nube de AWS.
* La subred pública actuará como la puerta de entrada a la plataforma en línea, brindando a los
usuarios acceso a internet y una experiencia de navegación fluida.
* Las subredes privadas estarán protegidas contra accesos no autorizados desde internet
garantizando la seguridad de los datos sensibles de la librería.
En una de estas subredes se aprovisionará la base de datos RDS.
* La instancia EC2 debe poder conectarse a la base de datos en la subred
privada.
* Para mantener un nivel óptimo de seguridad, se crearán usuarios IAM
con roles específicos:
  - El primer usuario es el administrador del servidor web por lo tanto
tendrá los siguientes permisos:
    - EC2 Full Access
    - SSM Full Access
    - EC2InstanceConnect
  - El segundo usuario es el administrador de las bases de datos RDS por
lo tanto tendrá los siguientes permisos:

    - RDS Full Access
  - El tercer usuario tendrá permisos de auditoría sobre la base de datos RDS, limitándose a
funciones de lectura para garantizar la integridad de los datos.
  -   El cuarto usuario será responsable de la auditoría de la instancia EC2 y tendrá permisos
de solo lectura, protegiendo así la seguridad de la plataforma web.
* Arquitectura resiliente, altamente escalable, disponible y segura.  
* Implementar la siguiente infraestructura de red:
  - 1 VPC
  - 2 zonas de disponibilidad.
  - 1 Internet Gateway
  - 2 subredes publica en cada zona de disponibilidad.
  - 4 subredes privadas, 2 en cada zona de disponibilidad.
  - 2 Elastic IPs
  - 2 NatGateways
 * Debe configurar un Subnet Group con las dos subredes privadas.  
    (Verificar que cada subred esté en una zona de disponibilidad diferente).
  
* En una de las subredes pública implementar un Bastión Host (Instancia EC2) que sirva para
acceder a las instancias en las subredes privadas. En este Bastión Host se configurará el servidor
web que será lanzado en las instancias en las dos subredes privadas.
* Configurar el servicio RDS en las otras dos subredes privadas.
* 3 EC2 Instances
* 1 S3 bucket
* 1 Relational Database Service (RDS)
* Configurar el servicio de Auto Scaling Group.
* Configurar el Load Balancing.
* Realizar una prueba de estrés para verificar el funcionamiento del Auto Scaling Group.

### Diagrama de arquitectura.
En la siguiente imagen se muestra el diseño de la arquitectura a partir de los requerimientos.
![arquitectura](img/Arquitectura.png)
  
### Identificar Roles.
* Web administrator
* Data Base administrator
* Relational Database Service (RDS) audit
* EC2 audit

### Diagrama de Gantt.
-Imagen

### Determinar presupuesto de acuerdo con los servicios AWS usados.
_AWS Calculator

## Ejecucion
para la creacion de los recursos que satisfagan los requerimientos y recursos que nos hemos plantado lo vamos a divirdir en dos archivos, el primer archivo lo vamos a confgurar con la parametrizaciones de red, como lo es la vpc, las subredes, internet gateway, nat gateway,  routebles y routes, lo llamaremos como network.yaml

> [!IMPORTANT]
> en esta seccion se va a explicar el contenido que los archivos pricipales para configurar nuestra arquitectura dentro de aws.
<p>Primero tenemos la seccion de parametros.<p>
En esta seccion vamos a asociar la vpc a una ip
```
AWSTemplateFormatVersion: "2010-09-09"

Description:
  This template deploys the architecture with one VPC, two public subnets and two private subnets

Parameters:
 
  VpcCIDR:
    Type: String
    Default: 172.16.0.0/16
```

* Documento la implementación a través de capas usando el servicio AWS Cloudformation y AWS Pipeline.
* Describir cada uno de los componentes usados durante la implementación.
* Argumentar de acuerdo con el AWS Well-Architect Framework.


Ejemplo de codigo
```
codigo
```

## Seguimiento y Control
Describir la configuración del servicio de AWS Cloudwatch.


