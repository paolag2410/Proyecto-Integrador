# Tech Store Pro
Aplicación desarrollada en Python utilizando el framework Flet, que simula una tienda en línea de productos tecnológicos con carrito de compras.

### Descripción general
Tech Store Pro es una aplicación interactiva que implementa una interfaz gráfica moderna para la gestión de productos tecnológicos. Permite al usuario explorar un catálogo visual, agregar productos a un carrito y visualizar el total acumulado en tiempo real.

El proyecto está diseñado con fines educativos para demostrar:

- Creación de interfaces gráficas en Python
- Manejo de eventos
- Actualización reactiva de la UI
- Organización modular del código

### Objetivos del proyecto
- Implementar una interfaz visual atractiva sin usar frameworks web tradicionales
- Simular el comportamiento básico de un e-commerce
- Aplicar conceptos de programación estructurada y orientada a objetos
- Practicar el uso de componentes visuales y eventos en Flet

### Tecnologías utilizadas

| Tecnología | Descripción |
|------------|------------|
| Python 3 | Lenguaje principal |
| Flet | Framework para crear interfaces gráficas modernas |

### Arquitectura del sistema

El proyecto sigue una estructura simple basada en funciones y clases:

```plaintext
main.py
│
├── productos (lista de diccionarios)
├── main(page)
│   ├── variables de estado (carrito)
│   ├── función actualizar()
│   ├── clase Card (componente reutilizable)
│   ├── header (encabezado)
│   ├── catalogo (contenedor de productos)
│   └── renderizado final
```
### Modelo de datos

Los productos se almacenan en una lista de diccionarios con la siguiente estructura:

```python
{
    "id": int,
    "nombre": str,
    "descripcion": str,
    "precio": float,
    "imagen": str  # URL
}
```
Ejemplo:

```python
{
    "id": 1,
    "nombre": "Laptop Gaming X",
    "descripcion": "Procesador i9, 32GB RAM, RTX 4080.",
    "precio": 2499.99,
    "imagen": "URL"
}

```
### Lógica de funcionamiento

###  Carrito de compras

Se maneja mediante una lista en memoria:

```python
carrito = []
```
