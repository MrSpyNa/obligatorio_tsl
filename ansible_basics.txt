1. ¿Qué es Ansible y por qué es "sin agente" (agentless)? 

Ansible es una herramienta de código abierto que permite automatizar tareas como la gestión de configuraciones, la implementación de aplicaciones y la administración de infraestructura. Permite instalar software, aplicar parches y mejorar la seguridad sin intervención manual.
Es "sin agente" porque no requiere software adicional en los nodos gestionados. Utiliza un archivo de inventario para identificar los servidores y se conecta a ellos mediante SSH, ejecutando tareas con el usuario actual y escalando privilegios en caso de ser necesario. 

2. Explica la diferencia entre un comando ad-hoc y un playbook. 

Los comandos “ad-hoc” son instrucciones que consisten en una sola línea que se ejecuta directamente desde la consola de comandos. Se utilizan para tareas simples y puntuales, como reiniciar un servicio o copiar un archivo. 
Ejemplo de comando para el reinicio de un servicio, en este caso DNS para sistemas Debian/Ubuntu: 

ansible all -m service -a "name=systemd-resolved state=restarted" 

Los “playbooks” son archivos escritos en formato YAML que definen una serie ordenada de tareas, establecidas de antemano, que realizan llamadas a los módulos de Ansible. Estos archivos son reutilizables, útiles para la automatización de tareas reiterativas y tediosas. 

3. ¿Qué es la idempotencia y por qué es importante en Ansible? 

Es una propiedad clave en Ansible que garantiza que la ejecución repetida de una tarea no altere el estado del sistema si este ya coincide con el estado deseado. Esto implica que, al aplicar una tarea “idempotente”, Ansible realizará cambios únicamente si es necesario, evitando modificaciones redundantes. Esta característica es esencial para mantener configuraciones consistentes y predecibles, permitiendo que los playbooks se ejecuten múltiples veces sin causar modificaciones indeseadas. 
No todos los módulos de Ansible son inherentemente idempotentes; a modo de ejemplo, los módulos “command” y “shell” no poseen esta propiedad de forma predeterminada, por lo que se deben utilizar con precaución. 

4. ¿Cómo funcionan los handlers y cuándo deberías usarlos? 

Los “handlers” son tareas que se ejecutan únicamente cuando son notificadas por otras tareas que han realizado cambios en el sistema. Los handlers se definen de manera similar a las tareas regulares, pero se ubican en una sección especial llamada handlers. Se ejecutan al final de la ejecución del playbook y solo una vez, incluso si múltiples tareas los notifican. Es recomendable utilizarlos cuando ciertas acciones, como reiniciar servicios o recargar configuraciones, deben realizarse únicamente tras cambios específicos, evitando operaciones innecesarias. 

5. ¿Cómo verificas errores de sintaxis en un playbook de Ansible? 
 
Para identificar errores de sintaxis en un playbook de Ansible, se puede recurir el comando “ansible-playbook” con la opción “--syntax-check”. Este comando analiza el playbook especificado y reporta cualquier problema de sintaxis sin ejecutarlo, permitiendo la corrección errores previo a la realización de cambios en los sistemas gestionados.  
También es aconsejable utilizar la opción “--check” para realizar una "prueba en seco" (dry run), simulando la ejecución del playbook sin efectuar modificaciones reales, lo que ayuda a prever posibles problemas. 
