# Proyecto Team1

- Manuel Enrique Caita				
- Danny Alexander Riano Gomez				
- Luis Felipe Chacon				
- Carlos Alberto González Cardozo				

Despliegue de una arquitectura en AWS altamente disponible y escalable

## Planificacion


• Planificación.
o Identificación de requerimientos.
o Diagrama de arquitectura.
o Identificar Roles.
o Diagrama de Gantt.
o Determinar presupuesto de acuerdo con los servicios AWS usados.
▪ AWS Calculator.



### Identificación de requerimientos.

#### AWS infrastructure High Availability and High Scaling
##### Network Requirements
* 1 VPC
* 6 subnets:
  - According to the design we will need two public subnets and four private subnets
* 1 Internet Gateway
* 2 Availability Zones
* 1 Application Load Balancer
* 1 Auto Scaling Group
* 3 EC2 Instances
* 1 Relational Database Service (RDS)

  
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









### Identificación de requerimientos.

### Diagrama de arquitectura.
En la siguiente imagen se muestra el diseño de la arquitectura a partir de los requerimientos.
![arquitectura](img/Arquitectura.png)
  
### Identificar Roles.
### Diagrama de Gantt.
### Determinar presupuesto de acuerdo con los servicios AWS usados.
_AWS Calculator

## Ejecucion
Ejemplo de codigo
```
codigo
```

## Seguimiento y Control
