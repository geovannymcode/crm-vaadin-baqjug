# Referencias

## Vaadin Flow

- **Documentación general**: <https://vaadin.com/docs>
- **Signals (estado reactivo)**: <https://vaadin.com/docs/latest/flow/ui-state>, la guía oficial de cómo manejar estado de UI con Signals.
- **Effects y Signals computados**: <https://vaadin.com/docs/latest/flow/ui-state/effects-computed>
- **Component Bindings con Signals** (`bindValue`, `bindText`, `bindVisible`, `bindEnabled`): <https://vaadin.com/docs/latest/flow/ui-state/building-ui>
- **Binder** (validación y binding de formularios): <https://vaadin.com/docs/latest/flow/binding-data/binder>
- **Grid**: <https://vaadin.com/docs/latest/components/grid>
- **Theming y variantes**: <https://vaadin.com/docs/latest/styling>
- **Tema Aura y su editor de temas**: <https://vaadin.com/docs/latest/styling/themes/aura>
- **Directorio de add-ons**: <https://vaadin.com/directory>

!!! note "Signals es una API relativamente nueva"
    Se volvió production-ready recién en Vaadin 25.1. Los nombres de clases
    y métodos de esta guía (`ValueSignal`, `Signal.effect`, `bindValue`/`bindText`/`bindVisible`/`bindEnabled`)
    están confirmados contra la documentación oficial al momento de
    escribir esto. Si algo no compila tal cual en tu versión de Vaadin,
    revisa el changelog de Signals en la documentación: lo más probable es
    un cambio menor de nombre de método, no un cambio de concepto.

## Spring

- **Spring Boot**: <https://docs.spring.io/spring-boot/>
- **Spring Data JPA**: <https://docs.spring.io/spring-data/jpa/reference/>

## El repo de esta guía

Si publicas tu propio avance como repo, este es un buen punto de partida
para el README:

- Cada sesión termina con un commit (checkpoint). El último es la versión
  final, con tema propio.
- `docs/` es esta guía, pensada para servirse con MkDocs Material
  (`pip install mkdocs-material && mkdocs serve`).

---

¿Dudas o ideas? Escribime por [GitHub](https://github.com/geovannymcode) o
[LinkedIn](https://www.linkedin.com/in/geovannycode/).
