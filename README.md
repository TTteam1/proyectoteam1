# Proyecto Team1

- Manuel Enrique Caita				
- Danny Alexander Riano Gomez				
- Luis Felipe Chacon				
- Carlos Alberto González Cardozo				

Despliegue de una arquitectura en AWS altamente disponible y escalable

## Planificacion

### Identificación de requerimientos.

La librería El mundo de las Letras es una librería física ubicada en Medellín con más de 20 años, reconocida en la región por su amplia selección de libros en diferentes  géneros y temas. Ha servido como lugar de encuentro para amantes de la lectura y  estudiantes de bachillerato y universitarios donde además de disfrutar de la lectura  o la experiencia de compra de libros, pueden probar los deliciosos postres que se  ofrecen.  
El Mundo de las letras con gran experiencia en ventas y asesoría de libros reconociendo el cambio en los hábitos de compra de los consumidores hacia el  comercio electrónico, ha decidido expandir su presencia en línea para llegar a un  público más amplio y mantener su relevancia en un mercado en constante evolución no solo nacional sino también internacional.  
Para respaldar esa plataforma en línea debe implementar la infraestructura en la  nube de AWS para ofrecer un rendimiento óptimo y una seguridad incomparable.  
La infraestructura debe contar con lo siguiente:  
• Desarrollar la plataforma web que permita a los clientes explorar los  diferentes libros.  
• Implementar la red en la nube de AWS con 3 subredes: una pública y dos  privadas.  
• La subred pública actuará como la puerta de entrada a la plataforma en línea,  brindando a los usuarios acceso a internet y una experiencia de navegación  fluida. En esta subred configurará la instancia AWS EC2.  
• Las subredes privadas estarán protegidas contra accesos no autorizados desde internet garantizando la seguridad de los datos sensibles de la librería. En una de estas subredes se aprovisionará la base de datos RDS.  
• La instancia EC2 debe poder conectarse a la base de datos en la subred  privada. Para facilitar esta conexión se implementarán parámetros de  conexión de la base de datos en el AWS System Manager Parameter Store,  garantizando acceso seguro y eficiente a los datos almacenados.  
• Para mantener un nivel óptimo de seguridad, se crearán cuatro usuarios IAM  con roles específicos: 
o El primer usuario es el administrador del servidor web por lo tanto  tendrá los siguientes permisos: 
▪ EC2 Full Access   
▪ SSM Full Access    
▪ EC2InstanceConnect   
o El segundo usuario es el administrador de las bases de datos RDS por  lo tanto tendrá los siguientes permisos:
▪ RDS Full Access 
o El tercer usuario tendrá permisos de auditoría sobre la base de datos  RDS, limitándose a funciones de lectura para garantizar la integridad  de los datos.  
o El cuarto usuario será responsable de la auditoría de la instancia EC2  y tendrá permisos de solo lectura, protegiendo así la seguridad de la  plataforma web.  



* 1 VPC
* 6 subnets:
  - According to the design we will need two public subnets and four private subnets
* 1 Internet Gateway
* 2 Availability Zones
* 1 Application Load Balancer
* 1 Auto Scaling Group
* 3 EC2 Instances
* 1 Relational Database Service (RDS)
* 2 Elastic IPs
* 2 NatGateways
* 1 S3 bucket
  

### Diagrama de arquitectura.
En la siguiente imagen se muestra el diseño de la arquitectura a partir de los requerimientos.
![arquitectura](img/Arquitectura.png)
  
### Identificar Roles.
* Admin
* Data Base administrator
* Developers
* EC2 instances administrator
* EC2 instances support
* Data Base audit
* EC2 instances audit
* S3 support

### Diagrama de Gantt.
-Imagen

### Determinar presupuesto de acuerdo con los servicios AWS usados.
_AWS Calculator

## Ejecucion
Ejemplo de codigo
```
codigo
```

## Seguimiento y Control




• Planificación.

o Diagrama de arquitectura.
o Identificar Roles.
o Diagrama de Gantt.
o Determinar presupuesto de acuerdo con los servicios AWS usados.
▪ AWS Calculator.

  
* Create a Nat Gateway for both public subnets
  - Create two Elastic IPs
  - Create Route table for each NatGateways
  - Create a Route for both Natgateways
  - Associate the route tables with subnets

* Create the SG for instance
* Create the SG for instance in subnet private
* Create the SG for ALB
* Create the SG for DB
* Create the instance
* Create a launch Template
* Create the Application Load Balancer
* Create the target group
* Create a listener for ALB
* Create the Auto Scaling group
* Create the Scaling policy
* Create the databases
* Create the subnets







#### AWS infrastructure High Availability and High Scaling
##### Network Requirements
* Create a VPC
* Create subnets:
  - According to the design we will need two public subnets and four private subnets
* Create Internet Gateway
  - Attach the Internet Gateway to VPC
  - Create the Route Table
    - Create a route
  - Associate the Public Route Table with both Public Subnets
* Create a Nat Gateway for both public subnets
  - Create two Elastic IPs
  - Create Route table for each NatGateways
  - Create a Route for both Natgateways
  - Associate the route tables with subnets


* Create the SG for instance
* Create the SG for instance in subnet private
* Create the SG for ALB
* Create the SG for DB
* Create the instance
* Create a launch Template
* Create the Application Load Balancer
* Create the target group
* Create a listener for ALB
* Create the Auto Scaling group
* Create the Scaling policy
* Create the databases
* Create the subnets








