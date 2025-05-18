## Descripcion General del Sistema
Este proyecto corresponde a el diagramado de un programa para la digitalizacion de turnos en entornos de atencion al publico, optimizando flujos operativos mediante automatizacion de asignacion y notificacion de turnos y escalabilidad para multiples sucursales y servicios
---
## Objtivos del Modelado
- Demostrar transición desde requisitos funcionles hasta arquitectura fisica
- Aplicar patrones de siseño para resolver problemas especificos del dominio
- Garantizar modularidad, mantenibilidad y extensibilidad

---

## Diagrama de Caso de Uso UML

![Diagrama de Caso de Uso](https://github.com/user-attachments/assets/2b27a74b-42ea-4d60-9cbd-88161c3afbe3)

#### Actoras identificados
**Cliente**: solicita, consulta o cancela turnos
**Administrador**: configura servicios, genera reportes y gestiona parametros globales
**Sistema Externo** sincroniza datos con sistemas externos

####Casos de uso destacado####
- **Sacar turno**: `<<extend>> Promocion especial` las promociones son opcionales y con condicioneles a fechas/campañas
- **Consultar Turno**: `<<inclide>> autenticar usuario` la autenticacion es obligatoria para acceder a datos privados
- **Generar reportes**: `<<include>> exporter PDF` todo reporte requiere conversion a fromato PDF
- **Sincronizar datos**: `<<SistemaExterno --> Sincronizar datos>>`  comunicacion directa con sistemas externos

####Justificacion Relaciones####
- `<<include>>` para flujos obligatorios en este caso autenticar usuario ya que es obligatorio para la seguridad del sistema
-  `<<extend>>` para funcionelidades condicioneles en este caso para promociones en fechas especiales

---

##Diagrama de clase UML con patrones aplicados

![Diagrama de clases](https://github.com/user-attachments/assets/4de6d2f3-182d-4e42-910d-810677837169)

- **Singleton** FabricaTurnos : garantiza una unica instancia global para evitar inconsistencia y centralizar control de creacion de turnos
- **Prototype** Turno : clonar turnos base para agilizar creacion de turnos en horarios pico
- **Adapter** AdaptadorExterno traducir formatos entre el sistema nuevo y aislar cambios en sistemas externos
- **Bridge** InterfazUsuario + DisplayModule separa logica de UI de implementacion para facilitar soporte multi-dispositivo

---

### Diagrama de implementacion UML

![Diagrama de Implementacion](https://github.com/user-attachments/assets/9d492a49-d078-49bf-b37f-7af9abd934d1)


- Nodos fisicos:
- - Servicio Central: hostea `FabricaTurnos` (Singleton) y CoordinadorTurnos
  - Dispositivos Cliente: interfaz adapter (Bridge) para movil/web/pantallas fisicas
  - Servidor de integracion: aisla conexiones con sistemas externos
- Seguridad:
- - Autenticacion obligatoria en la consulta de datos

---

## Reflexion final del modelo
este modelo demuestra como los patrones de diseño resuelven problemas concretos en sistemas de gestion de turnos
- **singleton** evita colisiones en la generacion de turnos
- **protorype** optimiza recursos en contextos de alta demanda
- **adapter/bridger** facilita la evolucion tecnologica sin impactar el codigo original. la arquitectura refleja buenas practicas, equilibrando flexibilidad, ejecucion y mantenibilidad
