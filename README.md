# IDLSA PyPI Server

Servidor de aplicaciones privada para IDLSA. Para más info ingresar al [link](https://testdriven.io/blog/private-pypi/#pypi-setup)

### Requisitos

- Instalar [docker](https://docs.docker.com/desktop/)
- Copiar .env.example y renombrar la copia como .env (Cambiar la variable `PORT` en caso de ser conflicto)
- Instalar htpasswd

```bash
# para debian o deribados
sudo apt-get install -y apache2-utils
# para centos o deribados
sudo yum install -y httpd-tools
```

### Configurar usuario y contraseña

- Crear usuario para subir dependencias al servidor

```bash
htpasswd -sc .htpasswd <SOME-USERNAME>
```

- **Ejemplo**:

```bash
htpasswd -sc .htpasswd pypi-admin
```

### Levantar el servidor

```bash
docker-compose up -d --build
```

---

## Como subir dependencias al PyPI Server

### Requisitos

Instalar twine y paslib

```bash
pip install twine
pip install passlib
```

### Subir dependencia

- Ingresar a la carpeta de la dependencia
- Construir la dependencia

```bash
python -m build
```

- Subir la dependencia al servidor privado

```bash
twine upload --repository-url http://<PUBLIC-IP-ADDRESS>:$PORT dist/*
```

- Usando **HTTPS**, para más info ingresar al siguiente [link](https://testdriven.io/blog/private-pypi/#supporting-https):

```bash
twine upload --repository-url https://<PUBLIC-IP-ADDRESS>:$PORT dist/*
```

- **Ejemplo**:

```bash
twine upload --repository-url http://10.10.10.10:8080 dist/*
```
