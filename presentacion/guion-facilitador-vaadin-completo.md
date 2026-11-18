# Guion del facilitador: Taller CRM interno con Vaadin Flow

## Cómo usar este documento

Este guion cubre la apertura con diapositivas y las sesiones 0 a 8 de la
guía, en **70 minutos**. El texto fuera de los bloques `> [en vivo]` es
lo que digo en voz alta. Los bloques `> [en vivo]` son indicaciones de
puesta en escena: qué mostrar, qué escribir y cuándo cambiar de pantalla.

Cada sesión del taller sigue el mismo ritmo: **muestro el problema en la
app, escribo la solución, y nombro el concepto que acabamos de usar.**
Si me paso de tiempo en una sesión, lo recupero en la siguiente, no al
final.

| Bloque | Tiempo | Acumulado |
|--------|--------|-----------|
| Apertura (diapositivas + Sesión 0) | 3 min | 3 |
| Sesión 1: primera vista | 6 min | 9 |
| Sesión 2: Grid | 7 min | 16 |
| Sesión 3: Signals | 9 min | 25 |
| Sesión 4: formulario y Binder | 11 min | 36 |
| Sesión 5: guardar, crear, eliminar | 12 min | 48 |
| Sesión 6: base de datos real | 5 min | 53 |
| Sesión 7: navegación | 6 min | 59 |
| Sesión 8: estilos y cierre | 11 min | 70 |

> **Antes de que entre el primer asistente**
>
> - Mi proyecto generado, con el backend de la Sesión 0 copiado,
>   corriendo con *hotswap* y con las dependencias ya descargadas.
> - Un commit por sesión ya hecho en una rama aparte, para saltar a un
>   checkpoint si algo se rompe en vivo.
> - Pedir con anticipación a los asistentes que traigan hecha la
>   Sesión 0. Generar el proyecto en vivo no cabe en 70 minutos.

Al final hay tres anexos: preguntas frecuentes, el orden de las demos y
un plan B.

---

## Parte 1: Apertura (3 min)

La presentación tiene 13 diapositivas, pero en 3 minutos no caben todas
con calma: algunas se pasan sin detenerse, y la de Signals (8) se usa
más tarde, en la Sesión 3.

| Diapositiva | Qué hago | Tiempo |
|-------------|----------|--------|
| 1. Portada | Hablo | 20 s |
| 2. Hola | Hablo | 30 s |
| 3, 4, 5. Trayectoria, eventos, stack | Paso sin detenerme | 0 s |
| 6. ¿Qué es Vaadin? | Hablo | 30 s |
| 7. La UI vive en el servidor | Hablo | 30 s |
| 8. Signals | Paso sin detenerme; vuelvo a ella en la Sesión 3 | 0 s |
| 9. Swing, JavaFX o frontend separado | Hablo | 30 s |
| 10. Qué vamos a construir | Hablo | 20 s |
| 11. La agenda | Hablo | 10 s |
| 12, 13. Redes y empecemos | Hablo | 10 s |

> **Captura de la portada**
>
> La imagen de la portada todavía es una captura de StockPilot, el
> ejemplo de inventario de la versión anterior. Cuando tenga la captura
> del CRM terminado (`docs/images/s8-tema-marca.png`), la reemplazo.

### Diapositiva 1: Portada

Buenos días a todos, bienvenidos. Hoy, en una hora y diez minutos, vamos
a construir un CRM interno: una lista de clientes que se puede buscar,
editar, crear y eliminar, con base de datos real, navegación y tema
propio. Y todo, incluida la interfaz, en Java. Sin HTML, sin un proyecto
de JavaScript aparte y sin una API REST de por medio.

### Diapositiva 2: Hola

Soy Geovanny Mendoza, Senior Backend Engineer en F2X, la empresa detrás
de Flypass. Soy Vaadin Champion y lidero BarranquillaJUG. Lo que vamos a
ver hoy no es un ejemplo de juguete: son los mismos patrones que uso en
sistemas reales.

> [en vivo] Paso las diapositivas 3, 4 y 5 sin detenerme.

### Diapositiva 6: ¿Qué es Vaadin?

Vaadin es un framework de Java de código abierto para construir
interfaces web. Nació en Finlandia en el año 2000, y lo usan en
producción empresas como Lufthansa o HSBC. Hoy usamos su enfoque
principal, Vaadin Flow: la interfaz completa en Java.

### Diapositiva 7: La UI vive en el servidor

La idea que quiero que se lleven es esta: en Vaadin Flow, la interfaz
vive en el servidor. Cada botón, cada campo, cada tabla es un objeto Java
normal. Vaadin mantiene una conexión con el navegador y se encarga de
pintar y actualizar lo que se ve. Ustedes programan contra objetos Java;
el navegador se actualiza solo.

> [en vivo] Paso la diapositiva 8 sin detenerme: la retomo en la Sesión 3.

### Diapositiva 9: ¿Por qué no Swing, JavaFX o un frontend separado?

Si vieron Swing o JavaFX en algún curso, ya tienen medio camino: un botón
es un objeto Java. La diferencia es que esto corre en el navegador. Y
frente a un frontend separado en React o Angular, el mismo equipo
backend entrega la interfaz completa, sin un segundo repositorio, un
segundo lenguaje ni un contrato de API que mantener sincronizado.

### Diapositiva 10: Qué vamos a construir

El problema de hoy: un equipo comercial lleva sus clientes en hojas de
cálculo, cada quien con su copia, y nadie sabe cuál es la real. Vamos a
construirles una herramienta interna para tener todo en un solo lugar.
La vista habla directo con el servicio, en el mismo proceso Java, y los
Signals mantienen la pantalla sincronizada.

### Diapositiva 11: La agenda

Son ocho sesiones cortas, cada una termina en un commit que compila y
corre. La Sesión 0 la traen hecha de casa.

### Diapositivas 12 y 13: Redes y empecemos

Les dejo las redes de BarranquillaJUG y el grupo del taller. La guía está
en el código QR, con todo el código, sesión por sesión. Manos a la obra.

> [en vivo] Cambio al IDE con el proyecto abierto y la app corriendo.
> Pregunto en voz alta quién tiene la Sesión 0 lista. Quien no la tenga
> sigue en modo observador y la completa después con la guía.

---

## Parte 2: El taller, sesión por sesión

### Sesión 1: Primera vista, componentes y layouts (6 min)

**El problema.** La app arranca, pero no muestra nada. Queremos una
pantalla con campos y botones, sin escribir HTML.

Abro `HomeView`. Fíjense en `@Route("")`: eso publica esta clase como
la página principal de la app. Y extiende `VerticalLayout`, que apila
los componentes uno debajo del otro.

> [en vivo] Escribo de a un componente y guardo entre cada paso:
> `TextField`, `DatePicker`, botón Guardar sin listener (clic: no pasa
> nada), `addClickListener` con `Notification.show`, botón Descartar
> (queda debajo, se ve raro), `HorizontalLayout` con los dos botones.

Cada componente es una clase: si quiero un botón, hago `new Button`. Y
este listener no corre en el navegador: corre aquí, en el servidor.
El navegador avisa que hubo un clic, se ejecuta mi Java, y Vaadin manda
de vuelta solo lo que cambió. Sin endpoint y sin JavaScript.

**Qué resolvimos:** componentes como objetos, y layouts dentro de
layouts para organizar la pantalla. Así se arma cualquier interfaz en
Vaadin.

### Sesión 2: Mostrar datos en un Grid (7 min)

**El problema.** Un CRM es, antes que nada, una lista de clientes.
Necesitamos una tabla, en su propia pantalla, y todavía sin base de
datos.

> [en vivo] Creo `CustomerListView` con `@Route("customers")`. Primero
> `new Grid<>(Customer.class)` con tres clientes de ejemplo.

Miren: Vaadin generó una columna por propiedad, incluido el `id`, y en
un orden que no elegí. Para un prototipo sirve; para una app real no.
Así que le quito la clase y agrego las columnas a mano.

> [en vivo] Cambio a `new Grid<>()` y `addColumn(Customer::getFirstName)`
> con su encabezado, una columna a la vez.

Esto es una referencia a método. Si mañana alguien renombra `getEmail`,
el código deja de compilar. Prefiero eso a una columna vacía en
producción.

> [en vivo] `grid.setSizeFull()`: no ocupa toda la pantalla. Lo dejo
> notar, y después agrego `setSizeFull()` a la vista.

Este es el error de layout más común al empezar: "tamaño completo"
significa el 100% del padre. Si el padre no ocupa toda la pantalla, el
hijo tampoco.

> [en vivo] `setSortable(true)` en cada columna y ordeno.

Si `/customers` da error de ruta, reinicio: las rutas nuevas a veces no
se registran con *hotswap*.

### Sesión 3: Filtrar con Signals (9 min)

**El problema.** Con tres clientes se ve todo; con trescientos, no.
Necesitamos un buscador. La forma clásica es escuchar el campo, filtrar y
refrescar la tabla a mano, y cada componente nuevo que dependa de la
búsqueda suma otro listener.

> [en vivo] Vuelvo a la diapositiva 8 (Signals) mientras explico, y
> regreso al IDE para escribir el código.

Vaadin tiene otra forma: los **Signals**. Un signal es un contenedor de
estado reactivo. En vez de escuchar cambios y actualizar la UI a mano,
declaro la relación entre el dato y la UI, y Vaadin la mantiene
sincronizada. Si conocen React: `ValueSignal` es como `useState`, y
`Signal.effect` como `useEffect`. La diferencia es que esto corre en el
servidor.

Si no les hace clic a la primera, tranquilos: vamos a usar el mismo
patrón tres veces más hoy.

> [en vivo] Paso `customers` a campo. Creo
> `ValueSignal<String> searchValue = new ValueSignal<>("")`, el
> `TextField`, `bindValue(searchValue, searchValue::set)` y
> `Signal.effect(search, () -> updateCustomerList(searchValue.get()))`.
> Filtro solo por nombre, escribo "ali" y presiono Enter.

Fíjense que el campo y el Grid no se conocen. El campo escribe en el
signal; el efecto lee el signal y actualiza el Grid.

> [en vivo] Agrego apellido, correo y estado al filtro. Pruebo
> "bluefern" y "prospect". Agrego `ValueChangeMode.LAZY`: ya no hace
> falta Enter.

> [en vivo] Borro el `grid.setItems(...)` del constructor y muestro que
> el Grid se sigue llenando.

¿Por qué sigue funcionando? Porque el efecto se ejecuta apenas la vista
se carga. Ya no necesito llenar el Grid a mano.

Y ahora la única regla que les pido memorizar hoy: **dentro de un
efecto, `get()`; en cualquier otro lugar, `peek()`.** `get()` lee el
valor y además suscribe el efecto a ese signal. Fuera de un efecto, lanza
una excepción.

> [en vivo] Muevo el buscador a `createSearch()` y el Grid a
> `configureGrid()`. Treinta segundos, sin explicarlo de más.

### Sesión 4: Formulario de detalle, Binder y validación (11 min)

**El problema.** Podemos ver y buscar, pero no tocar. Quiero hacer clic
en un cliente y ver sus datos en un formulario.

> [en vivo] Creo `editedCustomer`, un `ValueSignal<Customer>` que arranca
> en `null`. En `configureGrid()`:
> `grid.asSingleSelect().bindValue(editedCustomer, editedCustomer::set)`.
> Agrego un efecto de prueba con una notificación, hago clic en filas y
> lo borro.

Es el mismo patrón de la búsqueda: un signal, un enlace de dos vías y un
efecto. Ahora la selección del Grid vive en un signal.

> [en vivo] Creo `createForm()` con `TextField`, `EmailField`,
> `ComboBox<Status>` y `DatePicker`. Lo pongo al lado del Grid con un
> `HorizontalLayout`. Queda muy ancho: `setWidth("300px")`. Si se pierde
> el alto: `content.setSizeFull()`.

`EmailField` ya valida el formato del correo. `ComboBox` es un
desplegable con filtro, y le paso los valores del enum.

> [en vivo] `form.bindVisible(editedCustomer.map(c -> c != null))`.
> Selecciono y deselecciono.

`map` crea un signal derivado: un booleano que se recalcula solo cada vez
que cambia la selección. Y fíjense que no solo se enlazan valores:
también la visibilidad. Más adelante haremos lo mismo con el texto y
con si un botón está habilitado.

**Segundo problema.** El formulario aparece, pero vacío. Podría hacer
`setValue` en cada campo y leerlos uno por uno al guardar, pero ya son
cinco campos y todavía falta validar.

Para eso está `Binder`: conecta cada campo con un getter y un setter, en
las dos direcciones, y además valida.

> [en vivo] `binder.bind(firstName, Customer::getFirstName, Customer::setFirstName)`
> y `Signal.effect(form, () -> binder.setBean(editedCustomer.get()))`.
> Hago clic en filas: se llena el nombre. Enlazo el resto.

El efecto es el puente: cambia la selección y el Binder recibe el nuevo
cliente.

> [en vivo] Cambio a `forField(firstName).asRequired("El nombre es obligatorio")`.
> Borro el nombre: borde rojo y mensaje. Hago lo mismo con apellido,
> correo y estado.

`customerSince` no es obligatorio a propósito: un prospecto todavía no
tiene fecha de alta. Y algo importante: mientras un campo es inválido, el
Binder no escribe ese valor en el cliente.

### Sesión 5: Guardar, descartar, crear y eliminar (12 min)

**El problema.** Miren esto.

> [en vivo] Edito el nombre de un cliente, hago clic en otra fila y
> muestro que el Grid ya tiene el cambio.

Nadie apretó guardar, pero el cambio ya está aplicado. Con `setBean`, el
Binder trabaja en modo *write-through*: cada cambio se escribe de
inmediato en el objeto. Si el usuario se equivoca, no hay vuelta atrás.

La solución es el modo *buffered*: los cambios se quedan en el formulario
hasta que el usuario los confirma. Y el cambio es una sola palabra:
`setBean` pasa a ser `readBean`.

> [en vivo] Cambio a `readBean`. Agrego Guardar y Descartar. Descartar:
> `binder.readBean(editedCustomer.peek())`. Escribo `save()` con
> `writeBean` y el `catch` vacío, y la sobrecarga
> `updateCustomerList()`. Pruebo descartar y guardar.

Tres métodos, tres trabajos: `readBean` copia del objeto al formulario,
`writeBean` valida y copia del formulario al objeto, y descartar es
volver a hacer `readBean`.

Fíjense en `peek()` dentro de los listeners: el clic decide cuándo se
ejecuta este código. No quiero que se vuelva a ejecutar solo cada vez
que cambie el signal. Confundir `get()` con `peek()` es el error más
común con Signals.

El `catch` vacío es intencional: si `writeBean` falla, cada campo ya
muestra su error. No lancen una excepción ahí; romperían la pantalla por
algo que el usuario ya está viendo.

**Problema dos:** no hay forma de crear un cliente.

> [en vivo] Renombro `createSearch()` a `createToolbar()`: `H3`,
> buscador y botón con `VaadinIcon.PLUS`. Le pongo
> `setFlexGrow(1, title)` al título. `addCustomer()` hace
> `editedCustomer.set(new Customer())`. En `save()`, agrego el cliente a
> la lista si no está. Creo uno en vivo.

Crear es una línea: pongo un cliente vacío en el signal. El formulario
se abre porque su visibilidad depende del signal, y se carga vacío
porque el Binder escucha el mismo signal. No hay una bandera de "modo
creación".

**Problema tres:** falta eliminar, y eliminar es destructivo.

> [en vivo] Botón Eliminar y `confirmDelete()` con `ConfirmDialog`:
> primero solo texto y `open()`, después `setCancelable(true)`, el
> listener que elimina, el encabezado, el nombre del cliente y el texto
> "Eliminar". `bindEnabled` con `c -> c != null`. Elimino un cliente.

Nada se borra hasta que el usuario confirma. Y el botón se deshabilita
solo cuando no hay selección: otra vez un `map` sobre el mismo signal.

### Sesión 6: Conectar la base de datos real (5 min)

**El problema.** Todo vive en una lista en memoria: reinicio y se pierde.
Y como los clientes nuevos no tienen `id`, no puedo distinguir uno nuevo
de uno existente. Fíjense que Eliminar está habilitado para un cliente
que nunca se guardó.

`CustomerService` está en el proyecto desde la preparación. Es Spring
Data JPA normal. La vista lo pide en el constructor y Spring lo inyecta.

> [en vivo] Agrego `CustomerService` al constructor. Borro `customers` y
> `getSampleCustomers()`, y sigo los errores del compilador: `findAll()`
> en `updateCustomerList`, `customerService.save` en `save()` (y
> desaparece el `contains`), y `customerService.delete` en el diálogo.
> Reinicio el servidor.

Hay que reiniciar porque cambió el constructor: *hotswap* no lo detecta.
Y fíjense: la vista llama al servicio directamente. Es un objeto Java,
en el mismo proceso. No hay REST, no hay JSON, no hay DTOs de
transporte.

> [en vivo] Agrego `isNew(customer)`. `saveBtn.bindText(...)` con "Crear"
> o "Guardar", y cambio el `bindEnabled` de Eliminar a `!isNew(c)`.
> Muestro un cliente existente y luego uno nuevo.

Con base de datos hay una regla clara: un cliente guardado tiene `id`.
Un solo método me da dos comportamientos, los dos derivados del mismo
signal.

### Sesión 7: App shell y navegación (6 min)

**El problema.** Tengo dos pantallas, y la única forma de cambiar entre
ellas es escribir la URL a mano.

> [en vivo] Creo `MainLayout extends AppLayout` con `@Layout`, vacío.
> Guardo y muestro el marco alrededor de todas las vistas.

Una anotación, y esta clase envuelve todas las rutas. No toqué ningún
`@Route`.

> [en vivo] `setPrimarySection(Section.DRAWER)`, `SideNav` con Inicio,
> lo agrego al drawer y navego. Agrego Clientes. Agrego logo y nombre en
> un `HorizontalLayout`, y `setPadding(true)` porque queda pegado al
> borde.

`SideNavItem` recibe la clase de la vista, no la URL como texto. Si la
ruta cambia, el menú la sigue sola, y un error de tipeo es un error de
compilación. Y el ítem activo se resalta solo.

### Sesión 8: Estilos, tema Aura y cierre (11 min)

**El problema.** Todos los botones se ven iguales. Guardar debería
destacar, y Eliminar debería verse peligroso.

Antes de escribir CSS, uso lo que ya traen los componentes.

> [en vivo] `ButtonVariant.PRIMARY` en Guardar y en +.
> `ERROR` + `TERTIARY` en Eliminar. `setConfirmButtonTheme("primary error")`
> en el diálogo. `form.getStyle().setPaddingTop("30px")`.

Las variantes se combinan: rojo y sin borde da un Eliminar discreto pero
claramente peligroso. `getStyle()` es para casos puntuales; lo que se
reutiliza va en la hoja de estilos. Si vienen de Vaadin 24: ya no lleva
el prefijo `LUMO_`.

**Problema dos:** no hay variante para poner en negrita el nombre de la
app, y la app ignora el modo oscuro del sistema.

> [en vivo] `appName.addClassNames("app-name")` y `.app-name { font-weight: bold; }`
> en `styles.css`: se ve sin reiniciar. Agrego
> `@ColorScheme(ColorScheme.Value.LIGHT_DARK)` en `AppShell` y
> reinicio.

Es CSS normal, sin lenguaje propietario. Vaadin trae dos temas, Aura y
Lumo, y los dos soportan modo claro y oscuro.

**Problema tres:** quiero los colores de mi marca sin diseñar un sistema
visual entero.

> [en vivo] Abro el editor de temas de Aura, elijo un acento, copio el
> bloque de variables y lo pego en `styles.css`. Cambio a
> `ColorScheme.Value.DARK` y reinicio.

No toqué ni un componente. Botones, campos, diálogos y el Grid cambiaron
juntos, porque todos leen las mismas variables CSS.

**Cierre (3 min).** Construimos un CRM con Grid ordenable y filtrable,
formulario validado con guardar y descartar, alta y baja contra una base
de datos real, navegación y tema propio. Todo en Java, en tres clases de
UI.

Para seguir: el directorio de add-ons de Vaadin, con componentes como
calendarios y gráficos que se instalan como una dependencia Maven más.
Vaadin Copilot, que con la app en modo desarrollo permite editar la UI
desde el navegador y escribe el cambio en el código Java. Y la
documentación de Signals, que tiene más de lo que vimos hoy, como
`ListSignal` y los signals computados.

> [en vivo] Si queda un minuto, abro Copilot y cambio el placeholder del
> buscador desde el navegador, mostrando que el código cambia en el IDE.

Muchas gracias. La guía queda publicada para que cada quien termine a su
ritmo, y seguimos en contacto por el grupo del taller.

---

## Anexo A: Preguntas frecuentes

**¿Por qué Vaadin y no React o Angular con una API REST?**
Para herramientas internas construidas por un equipo backend, un solo
lenguaje y un solo repositorio reducen mucho el mantenimiento. Para un
producto público con muchos clientes distintos, un frontend separado
sigue siendo válido.

**¿Aguanta muchos usuarios concurrentes?**
Sí, hay empresas grandes usándolo en producción. El estado de cada sesión
vive en el servidor, así que se dimensiona distinto a un frontend
estático, pero es un patrón conocido.

**¿Qué es un Signal, en una frase?**
Un contenedor de estado que avisa solo a todo lo que depende de él
cuando su valor cambia.

**¿Cuándo `get()` y cuándo `peek()`?**
`get()` dentro de un efecto, porque además suscribe el efecto al signal.
`peek()` en listeners y métodos auxiliares, porque solo interesa el valor
en ese instante. `get()` fuera de un efecto lanza
`IllegalStateException`.

**¿Qué hace `map` sobre un Signal?**
Crea un signal derivado, de solo lectura, calculado a partir del
original. No es el `map` de un stream.

**¿Qué es el modo buffered?**
Los cambios quedan en el formulario hasta que se llama a `writeBean`. Lo
contrario, *write-through* con `setBean`, escribe cada cambio de
inmediato en el objeto.

**¿Signals y Binder compiten?**
No. Signals decide qué se muestra y cuándo; Binder lee, escribe y valida
un formulario contra un objeto.

**¿Por qué Aura y no Lumo?**
Aura es el tema más reciente de Vaadin y trae un editor visual para
generar la paleta. Lumo sigue soportado: se cambia en una línea en
`AppShell`.

**¿Se puede usar en el celular?**
Los componentes son responsivos y con `@PWA` la app se puede instalar en
la pantalla de inicio. No genera apps nativas de iOS o Android.

**¿Es gratis?**
Vaadin Flow y todos los componentes que usamos hoy son de código
abierto. Vaadin también vende productos comerciales, pero ninguno hace
falta para el taller.

**¿Qué pasa si no termino hoy?**
Cada sesión termina en un commit que compila y corre. La guía queda
publicada para continuar desde donde cada uno se quedó.

## Anexo B: Orden de las demos

1. Sesión 1: componentes apareciendo uno a uno; el botón sin listener no
   hace nada; los botones pasan de apilados a lado a lado.
2. Sesión 2: columnas automáticas (con `id`) contra columnas manuales;
   Grid que no ocupa la pantalla hasta que la vista también es
   `setSizeFull()`.
3. Sesión 3: filtrar con "ali", "bluefern" y "prospect"; pasar de Enter
   a `LAZY`.
4. Sesión 4: notificación de selección; formulario que aparece y
   desaparece; campos que se llenan solos; error de campo obligatorio.
5. Sesión 5: el problema de *write-through* (cambio aplicado sin
   guardar), luego descartar y guardar; crear con +; eliminar con el
   diálogo.
6. Sesión 6: los clientes de `data.sql`; "Crear" contra "Guardar";
   Eliminar deshabilitado para un cliente nuevo.
7. Sesión 7: el marco apareciendo al guardar `@Layout`; navegación con
   ítem activo resaltado.
8. Sesión 8: variantes, negrita con CSS, modo oscuro, tema de marca
   pegado desde el editor de Aura. Opcional: Copilot.

## Anexo C: Plan B

**Si voy atrasado:** recorto los "recorridos" de a un componente y pego
el bloque completo de la guía explicándolo. Si a los 53 minutos no
terminé la Sesión 6, la Sesión 8 queda solo con variantes y cierre, y el
resto se lo dejo a la guía.

**Si algo se rompe en vivo y no lo encuentro en un minuto:** salto al
commit de checkpoint de esa sesión en mi rama de respaldo y sigo.

**Si *hotswap* no toma un cambio:** reinicio. Rutas nuevas, cambios de
constructor y cambios en `Application` o `AppShell` siempre lo necesitan.

**Si varios asistentes no traen la Sesión 0:** siguen en modo
observador. No intento generar proyectos en grupo durante el taller.

**Si el editor de temas de Aura no carga:** pego el bloque de variables
que está en la Sesión 8 de la guía.

**Si falla el proyector:** sigo narrando con la guía abierta en el
computador de cada asistente.

**Si preguntan algo fuera del alcance** (Hilla, despliegue, otro
framework): respondo en una frase y ofrezco seguir por el grupo del
taller.
