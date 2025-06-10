# loadBalancer

# 🌐 NGINX Configuration for TuneShuffle Deployment

Este archivo de configuración establece un **proxy inverso NGINX** que gestiona:

- 📦 El servicio del **Frontend** desde una máquina virtual dedicada
- ⚙️ El enrutamiento de solicitudes a los servidores **Backend (FastAPI)**
- 🤖 El balanceo de carga entre instancias de la **API de ML**

---

## 🧾 Overview

Esta configuración permite exponer un único servidor público (puerto 80) que enruta el tráfico entrante a servicios internos según la ruta del URL.

---

## 🧭 Routing Behavior

| Ruta         | Destino IP                                 | Rol                        |
|--------------|---------------------------------------------|----------------------------|
| `/`          | `172.20.100.115:3000`                       | Frontend (Next.js)         |
| `/api/`      | `172.20.100.95:8000` ó `172.20.100.78:8000` | Backend API (FastAPI)      |
| `/ml-api/`   | `172.20.100.95:8000` ó `172.20.100.78:8000` | ML API (con balanceo)      |

✅ **Balanceo round-robin** activado para `/api/` y `/ml-api`  
✅ Todos los servicios se exponen a través del **puerto 80**

---

## 🚀 Cómo usar

1. Guarda la configuración en el archivo:

```bash
/etc/nginx/conf.d/tuneshuffle.conf
```

2. Verifica que la configuración sea válida:

```bash
sudo nginx -t
```

3. Recarga NGINX para aplicar los cambios:

```bash
sudo systemctl reload nginx
```

