# Descripción de requerimiento "Flujo de proceso Venta directa" SMQ

# Índice

1. [Información general](#información-general)
2. [Descripción del flujo](#descripción-del-flujo)
    - [Compra de producto](#compra-de-producto)
    - [Verificación en Almacen de refacciones](#verificación-en-almacen-de-refacciones)
    - [Compra de artículo](#equipo-no-está-en-almacen-de-refacciones-compra-de-artículo)
    - [Recepción de artículo](#recepción-de-artículo)
    - [Prueba técnica](#prueba-técnica)
    - [Pruebas de calidad](#pruebas-de-calidad)
    - [Entrega de equipo](#entrega-de-equipo)
    - [Visualización](#visualización)
3. [Cotización](#cotización)
    - [Información General](#1-información-general)
    - [Descripción del Requerimiento](#2-descripción-del-requerimiento)
    - [Alcance](#3-alcance)
    - [Arquitectura Propuesta](#4-arquitectura-propuesta)
    - [Componentes del Sistema](#5-componentes-del-sistema)
    - [Estimación de Desarrollo](#6-estimación-de-desarrollo)
    - [Entregables](#7-entregables)
    - [Costo estimado y forma de pago](#8-costo-estimado-y-forma-de-pago)
    - [Garantía y soporte](#9-garantía-y-soporte)
    - [Supuestos y Exclusiones](#10-supuestos-y-exclusiones)

---

# Descripción de requerimiento "Flujo de proceso Venta directa" SMQ

## Información general

Se requiere un nuevo proceso para dar seguimiento a ventas directas.

## Descripción del flujo

### Compra de producto

El usuario "Gerente de ventas" registra la compra de un producto, los campos a solicitar son:

    - Información del cliente
    - Información del equipo a solicitar

![alt text](image.png)

![alt text](image-1.png)



### Verificación en Almacen de refacciones


El usuario "Almacen de refacciones" recibe pedido y verifica existencia, si no existe lo envía a compras para su adquisición.

Los campos a solicitar son:

    - Existencia de equipo 
        - Si
            - Estado del equipo (Bueno / Regular / Malo)
            - Comentario
        - No
            - Comentario

![alt text](image-2.png)

### (Equipo no está en Almacen de refacciones) Compra de artículo

El usuario "Compras" registra la compra del equipo o equipos con los siguientes campos:

    - Cant.
    - Equipo
    - No. de parte
    - Proveedor
    - Costo
    - Moneda
    - OC
    - Fecha de llegada
    - Comentario
    - Estado


![alt text](image-4.png)

![alt text](image-5.png)
Se puede actualizar el estado del equipo o  eqipos a comprar
![alt text](image-6.png)


### Recepción de artículo

El usuario "Gerente Técnico" recibe el artículo y valida que sea el correcto. En caso de ser rechzado regresa a compras / Almacen de refacciones

    - Operación (Aprobar / Rechazar)
        - Aprobar
            - Comentarios
        - Rechazar
            - Area responsable (Compras / Almacen de refacciones)
            - Comentarios


![alt text](image-7.png)
![alt text](image-8.png)



### Prueba técnica

El usuario "Lider de área" realiza las pruebas al equipo y determina si es funcional

- Operación (Aprobar / Rechazar)
    - Aprobar
        - Resultado de las pruebas
        - Comentarios
    
    - Rechazar
        - Comentarios
        - Area responsable (Compras / Almacen de refacciones)

### Pruebas de calidad

El usuario "Calidad" recibe el equipo y realiza pruebas de calidad.

- Operación (Aprobar / Rechazar)
    - Aprobar
        - Comentarios

![alt text](image-9.png)


    - Rechazar
        - Comentarios
        - Area responsable (Compras / Almacen de refacciones)

![alt text](image-10.png)

### Entrega de equipo

El usuario "Almacen de equipos" entrega el equipo y sube factura.

- Operación
    - Entregar
        - Factura
        - Comentarios de entrega

![alt text](image-11.png)


### Visualización

Será necesaria una consola de operacione snueva para la revisión de los tickets correspondientes a venta directa

![alt text](image-12.png)



## Cotización


### 1. Información General

**Proyecto:** Flujo de Proceso Venta Directa
**Cliente:** Servo Motion Querétaro SA de CV
**Fecha:** 2025-07-25
**Versión:** 1.0

---

### 2. Descripción del Requerimiento

Implementación de un nuevo flujo en el sistema SMQ para gestionar ventas directas desde el registro de la compra hasta la entrega final del equipo, integrando validaciones de áreas intermedias (Compras, Almacén de refacciones, Gerente Técnico, Líder de Área y Calidad).

---

### 3. Alcance

* Registro de compra por parte del **Gerente de Ventas**.
* Validación de existencia en **Almacén de refacciones**.
* Gestión de compra en **Compras** (con control de estados y actualizaciones).
* Recepción y validación por parte del **Gerente Técnico**.
* Pruebas funcionales por **Líder de Área**.
* Pruebas de calidad por el área de **Calidad**.
* Entrega final en **Almacén de equipos** con carga de factura.
* Consola de operación para seguimiento de tickets en tiempo real.

---

### 4. Arquitectura Propuesta

**Estructura de Capas:**

* **Modelo:** Entidades JPA.
* **DAO/Repository:** Acceso a BD.
* **Servicios:** Lógica de negocio para cada paso del flujo.
* **Controladores:** Servlets que manejan las solicitudes del usuario.
* **Vistas:** JSP con Bootstrap + DataTables para UI dinámica.

---

### 5. Componentes del Sistema

#### 5.1 Módulos

1. **Registro de Compra (Gerente de Ventas)**

   * Captura de datos del cliente y del equipo.
   * Generación automática de ticket de venta directa.

2. **Verificación en Almacén de Refacciones**

   * Validación de existencia.
   * Envío automático a compras si no hay stock.

3. **Compra de Artículo (Compras)**

   * Registro de orden de compra.
   * Subida de documentos (OC, factura).
   * Actualización de estados.

4. **Recepción y Validación (Gerente Técnico)**

   * Aprobar o rechazar artículo recibido.
   * Definición de área responsable en caso de rechazo.

5. **Pruebas Técnicas (Líder de Área)**

   * Registro de resultados de prueba y comentarios.

6. **Pruebas de Calidad (Calidad)**

   * Validación final de calidad.
   * Registro de comentarios.

7. **Entrega de Equipo (Almacén de Equipos)**

   * Registro de entrega y subida de factura.

8. **Consola de Operación**

   * Panel de seguimiento de tickets.
   * Búsqueda, filtrado y paginación.

---

### 6. Estimación de Desarrollo

| Actividad                                | Tiempo estimado     |
| ---------------------------------------- | ------------------- |
| Análisis detallado y adaptación a sistema actual                       | 3 días              |
| Diseño de base de datos                  | 2 días              |
| Desarrollo de backend (servicios y DAOs) | 8 días              |
| Desarrollo de vistas JSP + Bootstrap     | 8 días              |
| Integración de DataTables y filtros      | 3 días              |
| Pruebas unitarias y de integración       | 4 días              |
| Despliegue  y entrega                    | 3 días              |
| **Total estimado**                       | **31 días hábiles** |

---

### 7. Entregables

* Código fuente completo.
* Manual de despliegue y configuración.
* Manual de usuario para la consola de operación.
* Sistema desplegado en producción.

---

### 8. Costo estimado y forma de pago

|                                   | Costo (MXN)     |
| ------------------------------------------ | --------------- |
| **Total**                                  | **\$18,300.00** |

**Pago:**
El pago se realizará en **dos exhibiciones**:

* **Primer pago:** 50% (\$9,150 MXN) al inicio del proyecto.
* **Segundo pago:** 50% (\$9,150 MXN) a la entrega del proyecto (después del periodo de garantía).

El método de pago será **paypal** o **transferencia bancaria**.

---

### 9. Garantía y soporte

Se brinda un periodo de 15 días para validación del cliente,en caso de defecto se corregirá en este periodo sin costo. 
Cualquier cambio y/o requerimiento extra dentro y fuera del periodo de garantía genera costos adicionales.

### 10. Supuestos y Exclusiones

* Se asume que el sistema SMQ ya cuenta con autenticación básica y manejo de usuarios.
* Se incluirá un log de operaciones para todos los tickets de venta directa donde se almacene cada operación que se haga al ticket

***Esta cotización es válida hasta 30 días después de su generación, para mayor información por favor contactarse al 442-358-8389 o al correo ing.abel.padilla@gmail.com***

---