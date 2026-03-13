# kubernetes-wordpress
# Desplegament de WordPress en Kubernetes (K3S)

Aquest repositori conté els fitxers de configuració necessaris per posar en marxa un entorn de WordPress amb base de dades MariaDB utilitzant volums persistents i accés via Ingress.

## Requisits previs

1. Tenir un clúster de Kubernetes o K3S actiu amb un node control-plane i nodes agents.
2. Crear el secret per a la contrasenya de la base de dades a la terminal del servidor:
   `kubectl create secret generic mysql-pass --from-literal=password=la_teva_clau`

## Instruccions d'execució

Executa les següents ordres en aquest ordre per aixecar tot l'entorn:

1. **Crear els volums persistents:**
   `kubectl apply -f wp-db-pvc.yaml`
   `kubectl apply -f wp-site-pvc.yaml`

2. **Desplegar la base de dades MariaDB:**
   `kubectl apply -f mariadb-deployment.yaml`

3. **Desplegar el frontend de WordPress:**
   `kubectl apply -f wordpress-frontend.yaml`

4. **Configurar l'accés exterior (Ingress):**
   `kubectl apply -f wordpress-ingress.yaml`

## Accés a l'aplicació

Afegeix la següent línia al fitxer /etc/hosts de la teva màquina local per accedir amb el nom de domini:
`192.168.69.10 wordpress.local`

Finalment, entra a http://wordpress.local al teu navegador.
