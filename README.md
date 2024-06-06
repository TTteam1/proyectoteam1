# Proyecto Team1

- Manuel Enrique Caita				
- Danny Alexander Riano Gomez				
- Luis Felipe Chacon				
- Carlos Alberto González Cardozo				

Despliegue de una arquitectura en AWS altamente disponible y escalable

## Planificacion

#### AWS infrastructure High Availability and High Scaling
* Create a VPC
* Create subnets:
  - According to the desing we will need two public subnets and four private subnets
* Internet Gateway
* Nat Gateway
* Elastic IP
* Route tables for NatGateway
* Route for the two Natgateway
* Associate the route tables to subnets
>
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
