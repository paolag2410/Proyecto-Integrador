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
- Cada vez que el usuario presiona "Agregar":
    - El producto se añade a la lista
    - Se actualiza la interfaz



### Función de actualización

```python
def actualizar():
    contador_text.value = f"🛒 {len(carrito)}"
    total_text.value = f"Total: ${sum(p['precio'] for p in carrito):,.2f}"
    page.update()
```
Responsabilidades:
- Actualizar contador de productos
- Calcular total dinámicamente
- Refrescar la UI

### Componente reutilizable: Card
```python
class Card(ft.Container):
```
Funciones principales:
- Mostrar información del producto
- Renderizar imagen
- Incluir botón de acción
- Manejar eventos de clic

## Interfaz de usuario
### Elementos principales

Header
- Nombre de la tienda
- Contador del carrito

Catálogo
- Scroll horizontal
- Tarjetas de productos

Resumen
- Total de compra en tiempo real

### Diseño visual

- Fondo: BLUE_GREY_50
- Tarjetas con bordes redondeados
- Colores diferenciados para precios
- Diseño limpio y minimalista

Flujo de interacción

1. El usuario abre la aplicación
2. Visualiza los productos disponibles
3. Presiona "Agregar" en un producto
4. El sistema:
   ├── Añade el producto al carrito
   ├── Actualiza contador
   └── Recalcula total
5. La interfaz se actualiza automáticamente

### Rendimiento
- Manejo eficiente en memoria (listas simples)
- No requiere base de datos
- Actualización rápida gracias a page.update()

### Casos de uso
- Prototipo de tienda en línea
- Aplicación educativa para UI en Python
- Base para sistemas más complejos

### Mejoras futuras

Funcionales
- Eliminar productos del carrito
- Incrementar/disminuir cantidad
- Persistencia de datos (base de datos)
- Sistema de usuarios

UI/UX
- Modo oscuro
- Diseño responsive
- Buscador de productos
- Filtros por categoría

Técnicas
- Separación en módulos
- Uso de patrones de diseño (MVC)
- Integración con API REST

### Instalación
```bash
git clone https://github.com/tu-usuario/TechStorePro.git
cd TechStorePro
pip install flet
python main.py
```

### Conclusión
Este proyecto demuestra cómo es posible crear aplicaciones visuales modernas en Python utilizando Flet, sin necesidad de conocimientos avanzados en desarrollo web, ofreciendo una base sólida para aplicaciones más complejas.

## Codigo completo
```python
import flet as ft

productos = [
    {
        "id": 1,
        "nombre": "Laptop Gaming X",
        "descripcion": "Procesador i9, 32GB RAM, RTX 4080.",
        "precio": 2499.99,
        "imagen": "https://images.unsplash.com/photo-1603302576837-37561b2e2302"
    },
    {
        "id": 2,
        "nombre": "Smartphone Ultra",
        "descripcion": "Pantalla OLED 120Hz, Cámara 200MP.",
        "precio": 999.00,
        "imagen": "https://images.unsplash.com/photo-1511707171634-5f897ff02aa9"
    },
    {
        "id": 3,
        "nombre": "Audífonos Pro",
        "descripcion": "Cancelación de ruido activa.",
        "precio": 299.50,
        "imagen": "https://images.unsplash.com/photo-1518444065439-e933c06ce9cd"
    },
    {
        "id": 4,
        "nombre": "Monitor 4K",
        "descripcion": "32 pulgadas, 144Hz.",
        "precio": 550.00,
        "imagen": "https://images.unsplash.com/photo-1587829741301-dc798b83add3"
    },
    {
        "id": 5,
        "nombre": "Teclado RGB",
        "descripcion": "Switches mecánicos.",
        "precio": 120.00,
        "imagen": "https://images.unsplash.com/photo-1517336714731-489689fd1ca8"
    }
]

def main(page: ft.Page):
    page.title = "Tech Store Pro"
    page.bgcolor = ft.Colors.BLUE_GREY_50
    page.padding = 20

    carrito = []

    contador_text = ft.Text("🛒 0", size=20, weight=ft.FontWeight.BOLD)
    total_text = ft.Text("Total: $0.00", size=20, color=ft.Colors.GREEN_700)

    def actualizar():
        contador_text.value = f"🛒 {len(carrito)}"
        total_text.value = f"Total: ${sum(p['precio'] for p in carrito):,.2f}"
        page.update()

    class Card(ft.Container):
        def __init__(self, p):
            super().__init__()

            def agregar(e):
                carrito.append(p)
                actualizar()

            self.width = 260
            self.padding = 15
            self.bgcolor = ft.Colors.WHITE
            self.border_radius = 15

            self.content = ft.Column(
                controls=[
                    ft.Image(src=p["imagen"], height=150, fit="cover"),
                    ft.Text(p["nombre"], size=18, weight=ft.FontWeight.BOLD),
                    ft.Text(p["descripcion"], size=12),
                    ft.Text(f"${p['precio']:,.2f}", color=ft.Colors.GREEN_600),
                    ft.ElevatedButton("Agregar", on_click=agregar)
                ]
            )

    header = ft.Row(
        alignment=ft.MainAxisAlignment.SPACE_BETWEEN,
        controls=[
            ft.Text("🛍️ Tech Store", size=28, weight=ft.FontWeight.BOLD),
            contador_text
        ]
    )

    catalogo = ft.Row(scroll=ft.ScrollMode.AUTO)

    for p in productos:
        catalogo.controls.append(Card(p))

    page.add(header, catalogo, total_text)

ft.app(target=main)
```
<img width="1248" height="426" alt="image" src="https://github.com/user-attachments/assets/4975c095-5f7e-453a-8ca8-9d3e64545654" />
