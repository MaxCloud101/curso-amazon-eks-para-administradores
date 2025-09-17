# Introducción

En AWS una instancia spot es un tipo de instancia que permite a los usuarios ofertar por capacidad no utilizada de Amazon EC2 a un precio reducido, posiblemente ahorrando hasta un 90 % del precio bajo demanda. Nosotros podemos utilizar este tipo de instancias dentro de nuestros nodegroups. Recuerda utilizar estas instancias en cargas de trabajo reanudables que no sean críticas para tus operaciones.

## En acción: Creacion de un cluster managenodegroup con instancias spot

1.- Vamos al servio de AWS CloudShell

2.- Creamos un archivo y lo editamos con nano
```
nano spot-cluster-mng.yaml
```
Colocamos el siguiente contenido en el archivo
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: spot-cluster-mng
  region: us-west-2

managedNodeGroups:
- name: spot
  instanceTypes: ["c3.large","c4.large","c5.large","c5d.large","c5n.large","c5a.large"]
  spot: true
```
3.- Creamos el cluster con eksctl. Asi que lanzamos el siguiente comando:
```
eksctl create cluster -f spot-cluster-mng.yaml
```

![Verificar versiones](/img/4-1.image.jpg)

4.- Revisamos los node groups del cluster
```
eksctl get nodegroups --cluster spot-cluster-mng
```
![Verificar versiones](/img/4-2.image.jpg)

5.- Despues de verificar que todo este correcto eliminamos el cluster.
```
eksctl delete cluster -f selector-cluster.yaml --disable-nodegroup-eviction
```

## En acción: Creacion de un cluster nodegroup con instancias spot

Para crear un nodegroup con instancias spot vamos a utilizar el atributo **instancesDistribution**.

1.- Vamos al servio de AWS CloudShell

2.- Creamos un archivo y lo editamos con nano
```
nano spot-cluster-ng.yaml
```
Colocamos el siguiente contenido en el archivo:
```
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: spot-cluster-ng
  region: us-west-2

nodeGroups:
  - name: ng-1
    minSize: 2
    maxSize: 5
    instancesDistribution:
      maxPrice: 0.017
      instanceTypes: ["t3.small", "t3.medium"] # At least one instance type should be specified
      onDemandBaseCapacity: 0
      onDemandPercentageAboveBaseCapacity: 50
      spotInstancePools: 2
```

3.- Creamos el cluster con eksctl. Asi que lanzamos el siguiente comando:
```
eksctl create cluster -f spot-cluster-ng.yaml
```
4.- Revisamos los node groups del cluster
```
eksctl get nodegroups --cluster spot-cluster-ng
```
5.- Despues de verificar que todo este correcto eliminamos el cluster.
```
eksctl delete cluster -f selector-cluster.yaml --disable-nodegroup-eviction
```







