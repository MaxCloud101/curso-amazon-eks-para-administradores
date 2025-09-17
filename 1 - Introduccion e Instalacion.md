# 1 Introducción e instalación
## Introducción
Kubernetes es un orquestador de contedores, es decir que te va a permitir crear, administrar, y eliminar contenedores, este fue desarrollado por Google en 2014, luego fue donado y es mantenido por la CNCF (Cloud Native Compute Foundation).

Amazon EKS (Amazon Elastic Kubernetes Service) es un servicio de AWS que te ofrece Kubernetes de forma administrada. Esto te permitira lanzar rapidamente clusters de kubernetes sin la necesidad de instalar componentes en máquinas virtuales como Amazon EC2.

Eksctl es una herramienta de líneas de comando que te va a permitir administrar clústeres de Amazon EKS.

## Requerimientos para este curso

- Conocimientos básicos sobre programación
- Conocimientos básicos sobre Linux
- Conocimientos básicos en AWS
- Conocimientos intermedios en Docker

# Arquitectura de un cluster de kubernetes

Kubernetes está compuesto por un conjunto de recursos de cómputo, memoria ram y disco, en AWS seria utilizar instancias EC2. A este conjunto de instancias lo llamaremos "clúster". En un clúster de kubernetes van a correr diferentes componentes.

A continuación vamos a explicar como es la arquitectura de un clúster de Kubernetes y la función de cada uno de los componentes.
