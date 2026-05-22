# Memoria Técnica — Sistemas Informáticos

  

**Alumno/a:** Siarhei Lukashou

**Proyecto:** Bitácora IV — Laboratorio de Teletransportación Digital (SSH y RDP)

**Repositorio:**  `SI-Bitacora3-AccesoRemoto`

  

---

  

## 1. Descripción del sistema

  

El laboratorio despliega dos servicios en contenedores Docker mediante `docker-compose.yml`:

  

| Contenedor | Imagen | Función | Puertos |
| -- | -- | -- | -- |
| `lab_ssh_servidor` | `linuxserver/openssh-server` | Acceso remoto SSH | 2222 |
| `lab_rdp_servidor` | `linuxserver/webtop:ubuntu-xfce` | Escritorio remoto (RDP / web) | 3389, 3000 |

  

En desarrollo local el acceso es `localhost`; en producción/cloud el mismo `docker-compose` se ejecuta en **un único VPS**.

  

---

  

## 2. Estimación de Costes de Infraestructura

  

### 2.1. Supuestos

  

-  **Proveedor:** DigitalOcean (Droplet Basic 2 GB RAM, 1 vCPU, 50 GB SSD, ~2 TB transferencia incluida).

-  **Periodo:** coste **mensual recurrente** + despliegue inicial (solo facturado al cliente).

-  **Tráfico estimado:** 25 GB/mes salientes (sesiones SSH y RDP de práctica), dentro del cupo incluido.

  

### 2.2. Tabla presupuestaria

  

| Concepto | Recurso | Unidad | Cantidad | Coste empresa (€) | Precio cliente (€) |
|----------|---------|--------|----------|--------------------|--------------------|
| **Cómputo** | Droplet 2 GB — host de ambos contenedores[1] | mes | 1 | 12,00 | 15,60 |
| **Almacenamiento** | 50 GB SSD (incluido en Droplet; ~5 GB uso Docker) | GB-mes | 50 | 0,00 | 0,00 |
| **Transferencia de red** | Tráfico saliente SSH/RDP | GB | 25 | 0,00 | 0,00 |
| **Gestión y despliegue**  *(solo mes 1, cliente)* | Instalación `docker-compose`, usuarios, puertos | servicio | 1 | 0,00 | 80,00 |
| | | | **Subtotal** | **12,00** | **15,60** |
| | | | **IVA (21%)** | **2,52** | **3,28** |
| | | | **TOTAL MENSUAL** | **14,52** | **18,88** |

-  **Empresa:** paga al proveedor **14,52 €/mes**

-  **Cliente:** paga **18,88 €/mes** recurrente (margen del 30% sobre cómputo) + **80 €** únicos de puesta en marcha el primer mes.

 
### 2.3. Fórmulas utilizadas
  

- Coste por línea: `Cantidad × Precio unitario`

- Subtotal: `=SUM(rango_costes)`

- IVA: `=Subtotal × 0,21`

- Total mensual: `=Subtotal + IVA`
  

### 2.4. Captura del presupuesto

![Presupuesto Cloud](https://i.ibb.co/DgGSvwQh/image.png)

  

---


## 3. Estrategia de Despliegue y Comunicación  

Para subir mi  `docker-compose`  al Droplet vamos a usar  SFTP  (o  `scp`  por SSH) con clave Ed25519.  No vamos a usar FTP en texto plano: las contraseñas y los ficheros viajan sin cifrar. Con SFTP todo va cifrado y solo nosotros con clave. [2] También se puede hacer un  `git pull`  por SSH desde GitHub si hace falta. [3]

Para avisos, usamos  Microsoft Teams  en un canal de incidencias. Si el VPS o los contenedores caen,  UptimeRobot  o las alertas de DigitalOcean mandan un mensaje al canal y lo vemos rápido.


## 4. Referencias

[1] [DigitalOcean Droplets](https://www.digitalocean.com/pricing/droplets) — plan 2 GB: ~12 USD/mes.
[2] P. Ford-Hutchinson, “Securing FTP with TLS,”  _www.rfc-editor.org_, Oct. 2005, doi: https://doi.org/10.17487/RFC4217.
[3] “How to Connect to Droplets with SSH | DigitalOcean Documentation,”  _DigitalOcean_. https://docs.digitalocean.com/products/droplets/how-to/connect-with-ssh/
 

‌
