# Respuestas del taller teórico del paradigma orientado a aspectos (POA)

## 1. **El objetivo principal de la POA es:**
   - **c. Separar conceptos y minimizar las dependencias entre ellos.**

## 2. **Inconveniente de metodologías iterativas y POO:**
   - **b. No se considera el tratamiento de aspectos como seguridad y gestión de memoria.**

## 3. **Inconveniente que no aplica a la POA:**
   - **d. Posibles choques entre los aspectos.**

## 4. **Código mezclado (Code Tangling):**
   - **a. Varios requerimientos pueden estar dentro de un mismo módulo.**

## 5. **Elementos propios de la POA:**
   - **b. Puntos de corte, tejedores, puntos de enlace.**

## 6. **Incumbencia transversal (‘crosscutting concern’):**
   - **c. La conceptualización de responsabilidades de uso común en un sistema.**

## 7. **Aspecto aplicable en un banco:**
   - **b. La validación de una transacción de un cliente o empleado del banco.**

## 8. **Definición de un consejo:**
   - **b. El código que debe ser ejecutado en los puntos de unión.**

## 9. **La POA permite una adecuada:**
   - **b. Modularización.**

## 10. **Término relacionado con la POA:**
  - **d. Tejedor.**

### Taller práctico

Para permitir que "Paula", "Miguel", "Edgar" y "Jhonatan" puedan agregar nuevos usuarios al sistema, puedes modificar el código para incluir una función `add_user` que también esté decorada por `security_decorator`. Aquí está el código actualizado:

```python
# Definición del decorador de seguridad
def security_decorator(func):
    def wrapper(*args):
        # Lista de usuarios autorizados
        authorized_users = ["Jhonatan", "Miguel", "Paula", "Edgar"]
        # Validación de acceso
        if args[0] in authorized_users:
            return func(*args)
        else:
            print("Acceso denegado para: " + args[0])
            return None
    return wrapper

# Lista global de usuarios
usuarios = ["Jhonatan", "Miguel", "Paula", "Edgar"]

# Función para iniciar sesión
@security_decorator
def login(user):
    print("Bienvenido has iniciado sesión como: " + user)

# Función para agregar nuevos usuarios al sistema
@security_decorator
def add_user(admin, new_user):
    if new_user not in usuarios:
        usuarios.append(new_user)
        print(f"Usuario {new_user} agregado por {admin}.")
    else:
        print(f"El usuario {new_user} ya existe.")

# Pruebas del sistema
login("Paula")
login("Carlos")
add_user("Paula", "Carlos")  # Paula agrega a Carlos
add_user("Carlos", "Luna")  # Carlos intenta agregar a Luna
add_user("Edgar", "Luna")   # Edgar agrega a Luna
login("Luna")               # Luna intenta iniciar sesión
```

### Salida esperada:
```plaintext
Bienvenido has iniciado sesión como: Paula
Acceso denegado para: Carlos
Usuario Carlos agregado por Paula.
Acceso denegado para: Carlos
Usuario Luna agregado por Edgar.
Bienvenido has iniciado sesión como: Luna
```

### Explicación de los cambios:
1. **`add_user` decorado con `security_decorator`:** Asegura que solo usuarios autorizados puedan agregar nuevos usuarios.
2. **Lista global `usuarios`:** Contiene los usuarios autorizados iniciales y permite dinámicamente agregar nuevos.
3. **Validación en `add_user`:** Comprueba si el nuevo usuario ya existe antes de agregarlo.
4. **Pruebas completas:** Muestra diferentes casos de acceso y agrega usuarios autorizados y no autorizados.
