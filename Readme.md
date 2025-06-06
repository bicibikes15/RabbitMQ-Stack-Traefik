# Stack de RabbitMQ para Traefik by DigitAllFran

Este stack despliega RabbitMQ, un robusto y popular bróker de mensajería, e incluye su panel de gestión (`management`). La configuración está diseñada para ser gestionada y asegurada por un stack de Traefik existente.

## Arquitectura y Dependencias

RabbitMQ es un aliado poderoso en un ecosistema de microservicios. Para funcionar como se ha diseñado en este stack, requiere de:

1.  **El Guardián (Traefik):** Una instancia de Traefik v3 funcionando como proxy inverso.
    * **Stack Recomendado:** [Stack de Traefik de DigitAllFran](https://github.com/bicibikes15/Traefik)

2.  **La Red Compartida:** El estandarte oficial de este ecosistema es `digitallfran_net`. RabbitMQ se unirá a esta red para ser descubierto por Traefik.

## El Ritual de Invocación (Instalación)

**1. Clonar el Repositorio**
```bash
# Reemplaza 'tu-github' con tu nombre de usuario y 'rabbitmq-stack' con el nombre de tu repo
git clone [https://github.com/tu-github/rabbitmq-stack.git](https://github.com/tu-github/rabbitmq-stack.git)
cd rabbitmq-stack

2. Verificar la Red Externa

Asegúrate de que la red digitallfran_net existe. Si no, créala:

Bash

docker network create digitallfran_net

3. Configurar los Secretos

Crea tu archivo de configuración local a partir de la plantilla.

Bash

cp .env.example .env
Ahora, edita el archivo .env (nano .env) y establece tus valores:

RABBITMQ_DOMAIN: El subdominio para el panel de gestión de RabbitMQ.
RABBITMQ_USER: Tu usuario administrador.
RABBITMQ_PASS: Una contraseña fuerte para tu usuario.
RABBITMQ_COOKIE: Una cadena de texto larga y secreta para la comunicación interna de RabbitMQ.

4. Desplegar RabbitMQ

Bash

docker compose up -d
Verificación
Traefik asignará un certificado SSL al dominio y lo expondrá de forma segura. Accede al panel de gestión en https:// seguido de tu RABBITMQ_DOMAIN y usa las credenciales que creaste para iniciar sesión.