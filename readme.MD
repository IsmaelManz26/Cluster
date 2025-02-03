# Tarea

## Pruebas correctas y bien documentadas de despliegue de la aplicación sin cluster

### Prueba 1: Inicio del servidor

- **Descripción**: Iniciar el servidor sin usar clústeres.
- **Comando**:
  ```sh
  node app.js
  ```
- **Resultado esperado**: El servidor debería iniciar y estar disponible en [http://localhost:3000](http://localhost:3000).

### Prueba 2: Solicitud a la ruta raíz

- **Descripción**: Realizar una solicitud GET a la ruta raíz `/`.
- **Comando**:
  ```sh
  curl http://localhost:3000/
  ```
- **Resultado esperado**: La respuesta debería ser `"Hello World!"`.

### Prueba 3: Solicitud a la ruta `/api/:n`

- **Descripción**: Realizar una solicitud GET a la ruta `/api/500000`.
- **Comando**:
  ```sh
  curl http://localhost:3000/api/500000
  ```
- **Resultado esperado**: La respuesta debería ser el resultado de la suma de los números de 0 a 500000.

### Prueba 4: Prueba de carga

- **Descripción**: Realizar una prueba de carga para evaluar el rendimiento sin clústeres.
- **Comando**:
  ```sh
  loadtest http://localhost:3000/api/500000 -n 1000 -c 100
  ```

#### Resultados de las pruebas:
![init](capturas/npminit.png)
![appjs](capturas/appjs.png)
![express](capturas/express.png)
![hello-world](capturas/hello-world.png)
![api-50](capturas/api-50.png)
![api-50-tiempo](capturas/api-50-tiempo.png)
![api-5000000-tiempo](capturas/api-5000000-tiempo.png)
![sin-clusters](capturas/loadtest-sinclusters.png)
![sin-clusters-2](capturas/loadtest-sinclusters-2.png)

---

## Pruebas correctas y bien documentadas de despliegue de la aplicación con cluster

### Prueba 1: Inicio del servidor con clúster

- **Descripción**: Iniciar el servidor utilizando clústeres.
- **Comando**:
  ```sh
  node app2.js
  ```
- **Resultado esperado**: El servidor debería iniciar múltiples procesos y estar disponible en [http://localhost:3000](http://localhost:3000).

### Prueba 2: Solicitud a la ruta raíz

- **Descripción**: Realizar una solicitud GET a la ruta raíz `/` en un entorno con clúster.
- **Comando**:
  ```sh
  curl http://localhost:3000/
  ```
- **Resultado esperado**: La respuesta debería ser `"Hello World!"` y debería ser manejada por uno de los procesos del clúster.

### Prueba 4: Prueba de carga

- **Descripción**: Realizar una prueba de carga para evaluar el rendimiento con clústeres.
- **Comando**:
  ```sh
  loadtest http://localhost:3000/api/500000 -n 1000 -c 100
  ```
- **Resultado esperado**: Evaluar el tiempo de respuesta y el rendimiento del servidor bajo carga, observando mejoras en comparación con la versión sin clústeres.

#### Resultados de las pruebas:
![api-50-tiempo](capturas/con-cluster/api-50-tiempo.png)
![api-5000000-tiempo](capturas/con-cluster/api-500000-tiempo.png)
![consola](capturas/con-cluster/consola1.png)
![habilitar-scripts](capturas/con-cluster/habilitar-scripts-sistema.png)
![loadtest](capturas/con-cluster/loadtest.png)
![loadtest-conclusters](capturas/con-cluster/loadtest-conclusters.png)
![loadtest-conclusters-2](capturas/con-cluster/loadtest-conclusters-2.png)

---

## Pruebas correctas y bien documentadas de todas las opciones con PM2 y cuestiones

### `pm2 ls`:

El comando `pm2 ls` se utiliza para listar todos los procesos gestionados por PM2. 

#### Explicación de las columnas:

- **id**: Identificador del proceso.
- **name**: Nombre de la aplicación.
- **namespace**: Espacio de nombres.
- **version**: Versión de la aplicación.
- **mode**: Modo de ejecución (fork o cluster).
- **pid**: Identificador del proceso en el SO.
- **uptime**: Tiempo en ejecución.
- **↺**: Número de reinicios.
- **status**: Estado del proceso.
- **cpu**: Uso de CPU.
- **mem**: Uso de memoria.
- **user**: Usuario ejecutando el proceso.
- **watching**: Indica si se monitorean cambios.

![pm2 ls](capturas/pm2/pm2-ls.png)

---

### `pm2 logs`:

El comando `pm2 logs` muestra registros en tiempo real de las aplicaciones.

#### Secciones principales:

- **PM2 log**: Eventos del sistema PM2.
- **app-error.log**: Registros de error de la aplicación.
- **app-out.log**: Registros de salida estándar.
- **app-ismael-error-<id>.log**: Errores de instancias específicas.
- **app-ismael-out-<id>.log**: Salida estándar de instancias específicas.

#### Uso del comando:

Útil para depuración y monitoreo de logs en tiempo real.

![pm2 logs](capturas/pm2/pm2-logs.png)

---

### `pm2 monit`:

El comando `pm2 monit` permite monitorear en tiempo real las aplicaciones.

#### Secciones principales:

- **Process List**: Lista de procesos con detalles de ID, nombre, memoria, CPU y estado.
- **App Logs**: Logs en tiempo real.
- **Custom Metrics**: Métricas personalizadas.
- **Metadata**: Información de la aplicación, incluyendo nombre, versión, reinicios y uptime.

#### Uso del comando:

Permite identificar problemas y monitorear el rendimiento.

![pm2 monit](capturas/pm2/pm2-monit.png)