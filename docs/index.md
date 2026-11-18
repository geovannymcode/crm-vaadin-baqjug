# CRM interno en Java puro con Vaadin Flow

Taller de **1 hora y 10 minutos**. Construimos un CRM pequeño (una lista de
clientes que se puede buscar, editar, crear y eliminar, con base de datos
real, navegación y tema propio) escribiendo **solo Java**: sin HTML, sin
un proyecto de JavaScript aparte y sin una API REST de por medio.

## El problema que resolvemos

Un equipo comercial lleva sus clientes en hojas de cálculo. Cada persona
tiene su copia, nadie sabe cuál es la versión real, y cuando alguien
pregunta "¿cuántos clientes activos tenemos?" la respuesta depende de a
quién le preguntes.

Necesitamos una herramienta interna sencilla: ver, buscar, crear, editar
y eliminar clientes desde un solo lugar. Es el tipo de aplicación que un
equipo backend termina construyendo en casi cualquier empresa.

La forma habitual sería un backend con API REST y un frontend aparte en
React o Angular: dos proyectos, dos lenguajes y un contrato que mantener
sincronizado. Con **Vaadin Flow** toda la interfaz se escribe en Java,
en el mismo proyecto que ya tiene la lógica de negocio. Cada componente
(botón, campo, tabla) es un objeto Java que vive en el servidor, y el
framework se encarga de pintarlo y actualizarlo en el navegador.

## Agenda

| Sesión | Qué problema resuelve | Tiempo |
|--------|-----------------------|--------|
| [0](sesion_0.md) | Preparación (se hace **antes** del taller) y apertura | 3 min |
| [1](sesion_1.md) | Primera vista: componentes y layouts | 6 min |
| [2](sesion_2.md) | Mostrar datos en un Grid | 7 min |
| [3](sesion_3.md) | Filtrar con Signals | 9 min |
| [4](sesion_4.md) | Formulario de detalle, Binder y validación | 11 min |
| [5](sesion_5.md) | Guardar, descartar, crear y eliminar | 12 min |
| [6](sesion_6.md) | Conectar la base de datos real | 5 min |
| [7](sesion_7.md) | App shell y navegación | 6 min |
| [8](sesion_8.md) | Estilos, tema Aura y cierre | 11 min |

!!! warning "La agenda está ajustada"
    No hay minutos de sobra. La Sesión 0 tiene que estar hecha antes de
    empezar: generar el proyecto y descargar dependencias en vivo se come
    fácilmente 10 minutos.

## Cómo está escrita cada sesión

Todas siguen el mismo orden:

1. **Resumen**: tiempo en vivo, qué vas a tener al terminar y qué
   conceptos son nuevos.
2. **De dónde partimos** y **el problema**: qué no funciona o qué falta
   en la app en ese momento.
3. **Conceptos**: la explicación de cada idea nueva antes de usarla.
4. **Pasos numerados**: el código de cada paso, qué hace cada línea y
   qué deberías ver en el navegador al guardar.
5. **Código completo al cierre**: la clase entera, con imports, para
   comparar con la tuya.
6. **Verifica** y **errores comunes**: una lista para comprobar que todo
   funciona y una tabla con los síntomas más frecuentes y su solución.
7. **Qué resolvimos**, **captura** (ver
   [`images/README.md`](images/README.md)) y **checkpoint**: un commit
   para poder volver atrás si algo se rompe.

!!! tip "La guía tiene más detalle del que se dice en vivo"
    En el taller se avanza por los pasos numerados. Las explicaciones de
    conceptos, las tablas y las secciones "Para profundizar" están para
    leer con calma después, o si te quedas atrás durante el taller.

## Versiones

Java 25 · Spring Boot 4.1 · Vaadin 25.2 · tema Aura · Maven · H2 en memoria.

!!! note "Si el asistente te ofrece otras versiones"
    Las versiones disponibles en [start.vaadin.com](https://start.vaadin.com)
    cambian con el tiempo. Elige la estable más reciente de la serie
    Vaadin 25.x. Signals, que usamos desde la Sesión 3, necesita Vaadin
    25.1 o superior.

Este taller sigue el orden del tutorial oficial de introducción a Vaadin
Flow de Drew Harvey ([texto](https://drewharvey.github.io/vaadin-intro-tutorial/),
[código](https://github.com/drewharvey/vaadin-intro-tutorial)), adaptado
al español.

Arranca por la [Sesión 0](sesion_0.md).
