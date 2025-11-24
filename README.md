# PROYECTO POO - EQUIPO ROCKET

## Sistema de gestión de inventario
Este proyecto es una aplicación en Python que simula un sistema de gestión de inventario para la bodega de una farmacia. Permite registrar productos, controlar entradas y salidas, generar reportes y mantener un historial organizado de todos los movimientos.
El sistema está diseñado para manejar diferentes tipos de productos, registrar los movimientos del inventario y generar reportes.

## Diagrama de clases

.

```mermaid
classDiagram
direction TB
    class Inventory {
	    - products: dict[id : str]
	    - movements: list
	    + add_product() :
	    + delete_product() :
	    + register_entry() :
	    + check_out() :
	    + show_inventory() :
	    + search_product() :
	    + generate_report() :
	    + product_category() :
    }

    class Movement {
	    - id: int
	    - id_product: int
	    - type: str
	    - lot: int
	    - date: datetime
	    + __str__() :
    }

    class Product {
	    - __id: int
	    - name: str
	    - category: str
	    - cost: float
	    - lot: int
	    - registration_date: datetime
	    - date_expiration: datetime | None
	    - supplier: str
	    + __str()__:
	    + update_lot(lot:int) :
	    + total_cost() : -> float
    }

    class Medicine {
	    - __id: str
	    - name: str
	    - category: str
	    - cost: float
	    - lot: int
	    - registration_date: datetime
	    - date_expiration: datetime
	    - supplier: str
	    - route_of_administration: str
	    - dosage: float
	    - type: str
	    - invima: str
	    - prescription: bool
	    + __str()__:
	    + update_lot(lot:int) :
	    + total_cost() : -> float
    }

    class Medical_Device {
	    - __id: int
	    - name: str
	    - category: str
	    - cost: float
	    - lot: int
	    - registration_date: datetime
	    - date_expiration: datetime | None
	    - supplier: str
	    - type: str
	    - material: str
	    - single_use: bool
	    + __str() __:
	    + update_lot(lot:int) :
	    + total_cost() : -> float
    }

    class Care_Product {
	    - __id: int
	    - name: str
	    - category: str
	    - cost: float
	    - lot: int
	    - registration_date: datetime
	    - date_expiration: datetime | None
	    - supplier: str
	    - brand: str
	    - dosage: float
	    + __str() __:
	    + update_lot(lot:int) :
	    + total_cost() : -> float
    }

    class Archive {
	    - data_path: str
	    + save_inventory() :
	    + load_inventory() :
    }

    class Reports {
	    + general_report() :
	    + movement_report() :
	    + category_report() :
    }

    Product <|-- Medicine
    Product <|-- Medical_Device
    Product <|-- Care_Product
    Inventory *-- Movement
    Inventory <-- Reports
    Inventory <-- Archive
```

## ¿Cómo funciona?
Nuestro diagrama esta compuestos por distintas clases:


### Product (Clase base)
Es la clase principal de donde salen los demás productos. Sus atributos son:
- __id
- nombre
- categoría
- costo
- lote
- proveedor
- fecha de registro
- fecha de vencimiento

Sus metodos son:
- update_lot(): para actualizar el lote
- total_cost(): precio total del stock
- str(): mostrarlo como texto

Y sus tres clases hijas **(Herencia)*: 
- Medicine
- Medical_Device
- Care_Product


### Inventory (Clase base)
Es la clase más importante porque maneja todo el sistema. Aquí se guardan:
- Los productos (en un diccionario)
- La lista de movimientos

Sus metodos son:
- **add_product()** = Agregar productos
- **delete_product()** = Eliminar productos
- **register_entry()** = Registrar entrada
- **check_out()** = Registrar salida
- **show_inventory()** = Mostrar inventario
- **earch_product()** = Buscar producto
- **generate_report()** = Genrar reporte
- **product_category()** = Categoria de producto


### Movement
Guarda los cambios que le pasan a los productos. 
Sus métodos son:
- id
- id del producto
- tipo (entrada o salida)
- lote afectado
- fecha del movimiento


### Archive and Reports
Archive se encarga de guardar y cargar los datos del inventario. Mientras que Reports genera reportes con base en la información del inventario.
Ambas depenten de la clase "Inventory"

## Organización de Modulos y Paquetes:
Así mismo, se espera al momento de programar el código, este se organice de la siguiente manera:
```csv
Sistema de Inventario de Farmacia
│
├── Product (clase base)
│   ├── Medicine
│   ├── Medical_Device
│   ├── Care_Product
│
├── Inventory
│   ├── Manages products and transactions
│   ├── Calculates values, expiration dates, and low stock levels
│   └── Generates reports
│
├── Movement
├── Archive
└── Reports
```
