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
![aws_calculator](img/estimation.PNG)
El documento PDF con el detalle del pricing esta disponible en el siguiente link [PDF Pricing](source/AWSPricingCalculator.pdf)


## Ejecucion
para la creacion de los recursos que satisfagan los requerimientos y recursos que nos hemos plantado lo vamos a divirdir en dos archivos, el primer archivo lo vamos a confgurar con la parametrizaciones de red, como lo es la vpc, las subredes, internet gateway, nat gateway,  routebles y routes, lo llamaremos como network.yaml

> [!IMPORTANT]
> en esta seccion se va a explicar el contenido que los archivos pricipales para configurar nuestra arquitectura dentro de aws.
<p>Primero tenemos la seccion de parametros.<p>
En esta seccion vamos a asociar la vpc a una ip, esto lo hacemos dentro del bloque de parametros en el yaml.

```
AWSTemplateFormatVersion: "2010-09-09"

Description:
  This template deploys the architecture with one VPC, two public subnets and two private subnets

Parameters:
 
  VpcCIDR:
    Type: String
    Default: 172.16.0.0/16
```
> [!NOTE]
>Vamos a asociar las subnets auna ip por cada subnet, cada rango de ip debe ser diferente para que no se traslapen estas subredes.
```
  PublicSubnetAIP:
    Type: String
    Default: 172.16.1.0/24

  PublicSubnetBIP:
    Type: String
    Default: 172.16.2.0/24
  
  PrivateSubnetAIP:
    Type: String
    Default: 172.16.3.0/24
  
  PrivateSubnetBIP:
    Type: String
    Default: 172.16.4.0/24
    
  PrivateSubnetAAIP:
    Type: String
    Default: 172.16.5.0/24
    
  PrivateSubnetBBIP:
    Type: String
    Default: 172.16.6.0/24
```

> [!NOTE]
>Luego tenemos la seccion de recusos, en la cual vamos a definir los recuros que vamos a crear y que son necesarios para el despliegue.
Vamos a tener la creacion de la vpc, la cual se crea como un recurso de EC2,  la asociamos con el nombre que asociamos  en los recursos y asignamos la ip, esto nos permitira asignarle el rango de ip que se configuro anteriormente a la vpc que estamos creando.
```
Resources:
  VPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 
        Ref: VpcCIDR
      EnableDnsHostnames: true
      Tags:  
        - Key: Name
          Value: VPC-WEB-SERVER-BOOK 
```
> [!NOTE]
>Se realiza la configuracion para la creacion de las subnets, aqui la asociamos a la vpc que creamos, definimos una zona de disponibilidad, la asociamos a los parametros que teniamos anteriormente cuando definimos los parametros y las ip, esto lo debemos hacer para cada subnet, lo que va a cambiar son los nombres y la zona de disponibilidad.
```
  PublicSubnetA:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: 
        Ref: VPC
      AvailabilityZone: us-east-1a
      CidrBlock: 
        Ref: PublicSubnetAIP
      Tags:
        - Key: Name
          Value: PublicSubnetA 

  PublicSubnetB:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: 
        Ref: VPC
      AvailabilityZone: us-east-1b
      CidrBlock: 
        Ref: PublicSubnetBIP
      Tags:
        - Key: Name
          Value: PublicSubnetB 
```
> [!NOTE]
>Vamos a configurar el internet gateway, en la cual creamos el recurso le damos un nombre y tambien lo vamos ascoiar al internet gateway con la vpc.
```
  InternetGateway:
    Type: AWS::EC2::InternetGateway
    Properties:
      Tags:
        - Key: Name
          Value: IG_WSC

  InternetGatewayAttachment:
    Type: AWS::EC2::VPCGatewayAttachment
    Properties:
      InternetGatewayId: 
        Ref: InternetGateway
      VpcId: 
        Ref: VPC 
```
> [!NOTE]
>En esta seccion vamos a crear la route table y sera asociada a la vpc que se creo, esta se encargara de redirigir el trafico.
```
  PublicRouteTable:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: 
        Ref: VPC
      Tags:
        - Key: Name
          Value: Public_Routes

#luego vamos  a crear una route, esta route la tenemos que refenciar  a la route table que creamos, al internet gateway,tambien al attach del internet gateway y la vpc.
  PublicRouteA:
    Type: AWS::EC2::Route
    DependsOn: InternetGatewayAttachment
    Properties:
      RouteTableId:
        Ref: PublicRouteTable
      DestinationCidrBlock: 0.0.0.0/0
      GatewayId: 
        Ref: InternetGateway          
```

> [!NOTE]
>En esta seccion vamos asociar la route table a cada una de las redes publicas que creamos, hacemos relacion a que route table vamos asociar y a que subnet la queremos asociar.
```
  PublicSubnet1RouteTableAssociation:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      RouteTableId: 
        Ref: PublicRouteTable
      SubnetId: 
        Ref: PublicSubnetA

  PublicSubnet2RouteTableAssociation:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      RouteTableId: 
        Ref: PublicRouteTable
      SubnetId: 
        Ref: PublicSubnetB
```
> [!NOTE]
>Vamos a crear el recurso de la nat gateway, esto nos permitira que nos podamos conectar a intenet, como tenemos dos subredes publicas debemos crear dos nat gateway, cada una la vamos a asociar a un subred y le vamos a asociar un ip elastica, esta asociasion la vamos a realizar por medio del nombre de la ip elastica.
```
  NatGatewayA:
    Type: AWS::EC2::NatGateway
    Properties:
      AllocationId: !GetAtt AipELASTIC.AllocationId
      SubnetId:
        Ref: PublicSubnetA
      Tags:
        - Key: Name
          Value: NatGatewayA-subnetPublicA

  NatGatewayB:
    Type: AWS::EC2::NatGateway
    Properties:
      AllocationId: !GetAtt BipELASTIC.AllocationId
      SubnetId:
        Ref: PublicSubnetB
      Tags:
        - Key: Name
          Value: NatGatewayA-subnetPublicB
```
> [!NOTE]
>En esta seccion vamos a crear la configuracion para las ip elasticas, debemos tener dos ip elasticas estas son apra cada nat gateway y las asociamos a la vpc que creamos
```
  ##Elastic IP
  AipELASTIC:
    Type: AWS::EC2::EIP
    Properties:
      Domain:
        Ref: VPC
      Tags: 
        - Key: Name
          Value: EIP-nwA
  
  BipELASTIC:
    Type: AWS::EC2::EIP
    Properties:
      Domain:
        Ref: VPC
      Tags: 
        - Key: Name
          Value: EIP-nwB
```
> [!NOTE]
>En esta seccion vamos a crear 2 route tables asociadas a la vpc y estas las asociaremos a las nat gateway
```
  RouteTableNatGatewayA:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: 
        Ref: VPC
      Tags:
        - Key: Name
          Value: Route-NW-A
  
  RouteTableNatGatewayB:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: 
        Ref: VPC
      Tags:
        - Key: Name
          Value: Route-NW-B
```
> [!NOTE]
>Debemos crear una route para cada una de las route table que creamos, le definimos quien puede conectarse, lo asociamos a cada nat gateway
```
  PublicRouteNgA:
    Type: AWS::EC2::Route
    Properties:
      RouteTableId:
        Ref: RouteTableNatGatewayA
      DestinationCidrBlock: 0.0.0.0/0
      NatGatewayId: 
        Ref: NatGatewayA

  PublicRouteNgAB:
    Type: AWS::EC2::Route
    Properties:
      RouteTableId:
        Ref: RouteTableNatGatewayB
      DestinationCidrBlock: 0.0.0.0/0
      NatGatewayId: 
        Ref: NatGatewayB          
```
> [!NOTE]
>Vamos asociar nuestra route table cpn el natgateway y con la subneta la que deseamos asociar
```
  NWARouteAssociation:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      RouteTableId: 
        Ref: RouteTableNatGatewayA
      SubnetId: 
        Ref: PrivateSubnetA

  NWBRouteAssociation:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      RouteTableId: 
        Ref: RouteTableNatGatewayB
      SubnetId: 
        Ref: PrivateSubnetB
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


