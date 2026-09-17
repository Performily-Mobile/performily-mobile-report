<p align="center">
  <img src="assets/logo-upc.png" alt="Universidad Peruana de Ciencias Aplicadas" width="80">
</p>

<h3 align="center">Universidad Peruana de Ciencias Aplicadas</h3>
<h4 align="center">Carrera de Ingeniería de Software</h4>

<p align="center">
  <b>1ACC0238</b> · Aplicaciones para Dispositivos Móviles · <b>NRC</b> 4951
</p>

<h2 align="center">Performily · Flowboard</h2>

<p align="center">
  Informe del Trabajo Final · Período 202620
</p>

---

## Sobre este repositorio

Este repositorio contiene el informe del trabajo final del curso Aplicaciones para Dispositivos Móviles. Aquí se versiona el documento del informe, los recursos gráficos que lo acompañan y los artefactos de diseño que sustentan la solución.

El código fuente de los productos digitales se desarrolla en repositorios separados, enlazados más abajo.

## El proyecto

**Performily** es la startup. **Flowboard** es su producto: una solución móvil de gestión del vínculo laboral dirigida a organizaciones formales en crecimiento.

El problema que aborda es la dispersión de la información laboral. Los datos del colaborador viven repartidos entre hojas de cálculo, expedientes físicos y sistemas que no se comunican entre sí, de modo que el área de Recursos Humanos dedica buena parte de su tiempo a responder consultas repetitivas y el colaborador depende de intermediarios para saber algo tan básico como cuántos días de vacaciones le quedan. A esto se suma que las soluciones existentes se diseñan para el escritorio del especialista, cuando en el Perú el 95,4% de los hogares cuenta con telefonía móvil frente al 37,8% que cuenta con computadora.

Flowboard responde con una fuente única de verdad sobre el vínculo laboral, autogestión real del colaborador desde su propio teléfono y aprobaciones ruteadas según la jerarquía organizacional.

### Segmentos objetivo

Personal de Recursos Humanos, que administra el ciclo de vida del colaborador y es la puerta de entrada al sistema, y colaboradores generales, que consultan y gestionan su propia información desde un teléfono Android de gama media o de entrada, con conectividad intermitente. Dentro del segundo segmento existe el subperfil de colaborador con personal a cargo, cuya condición de aprobador se deriva de tener subordinados asignados.

## Productos digitales

| Producto | Tecnología |
| :---- | :---- |
| Aplicación móvil nativa | Kotlin sobre Android, Jetpack Compose |
| Aplicación móvil cross-platform | Flutter con Dart |
| RESTful API interno | Java con Spring Boot y Spring Data JPA |
| Landing Page | HTML5, CSS3, JavaScript |

El lenguaje de diseño es Material Design y el enfoque de diseño de todos los productos es Domain-Driven Design. El idioma por defecto de la interfaz es inglés.

## Alcance del dominio

La solución se organiza en siete bounded contexts sobre un Shared Kernel de identificadores tipados.

| Bounded context | Agregado raíz | Responsabilidad |
| :---- | :---- | :---- |
| IAM | UserAccount | Identidad, credenciales y control de acceso por rol |
| Workspace | Employee | Ficha, áreas, puestos, asignaciones y jerarquía |
| Attendance | AttendanceRecord | Marcaciones, consolidación diaria, tardanzas y sobretiempo |
| Request | Request | Trámites parametrizables con flujo de aprobación |
| Benefits | BenefitAssignment, VacationBalance | Beneficios y saldo de vacaciones con movimientos |
| Payroll | Payslip | Repositorio de boletas y estado del depósito |
| Wellbeing | Office | Lecturas ambientales e indicadores de salud ocupacional |

Un bounded context solo referencia a los agregados de otro mediante un identificador tipado, nunca mediante una referencia directa al objeto.

### Decisiones de alcance

Payroll publica boletas y controla el estado del depósito, no calcula remuneraciones. Attendance registra y consulta asistencia, no deriva descuentos ni pagos. No existe migración ni importación masiva de datos históricos: la carga inicial es manual. La plataforma se distribuye únicamente para Android; iOS queda fuera de alcance por ausencia de hardware y de licencia de distribución.

El control de acceso por rol no es un detalle técnico sino un requisito de la Ley N.° 29733 de Protección de Datos Personales: cada colaborador accede únicamente a su propia información.

## Requisitos técnicos del curso

| Requisito | Implementación |
| :---- | :---- |
| Almacenamiento local en el dispositivo | Room en Kotlin, Drift en Flutter |
| Acceso a un recurso interno del dispositivo | Sensor biométrico y sistema de notificaciones |
| Integración con un servicio RESTful interno | API propio documentado con OpenAPI |
| Acceso a un servicio externo de terceros | Firebase Cloud Messaging y API pública de feriados |
| Feature de aprendizaje autónomo | Autenticación biométrica local |

El feature de aprendizaje autónomo es la verificación biométrica local, con AndroidX Biometric en la aplicación nativa y el paquete `local_auth` en la cross-platform. La plantilla biométrica nunca sale del hardware seguro del dispositivo: no se transmite al API ni se almacena en ninguna base de datos.

## Estructura del repositorio

```
.
├── README.md
├── reporte.md      Informe del trabajo final
└── assets/         Figuras del informe y logotipo
```

## Cómo leer el informe

El informe se lee desde `reporte.md`. Está escrito en Markdown y contiene una tabla de contenido con enlaces a sus secciones. La estructura sigue el enunciado del curso:

Registro de versiones, Project Report Collaboration Insights, Student Outcome, Objetivos SMART, Capítulo I de presentación de la startup y del perfil de la solución, Capítulo II de desarrollo de requisitos y diseño de la solución de software, Conclusiones y recomendaciones, Bibliografía y Anexos.

## Convenciones de trabajo

El control de versiones sigue GitFlow con ramas `main`, `develop` y ramas de feature. Los mensajes de commit siguen Conventional Commits y las versiones del informe siguen Semantic Versioning, registradas en la sección de registro de versiones del propio documento.

Los nombres de los bounded contexts, los agregados y los eventos de dominio son los mismos en el EventStorming, los canvases, el backlog, los diagramas y el código. Si algo se renombra, se renombra en todos.

## Herramientas

Los diagramas C4 se construyen con Structurizr, los diagramas UML de clases y de base de datos con PlantUML, el EventStorming con Miro, los wireframes y prototipos con Figma, y los artefactos de needfinding con UXPressia.

## Equipo

| Código | Apellidos y Nombres |
| :---- | :---- |
| u202412270 | Ávila De La Cruz, Darío Fabián |
| u202412663 | Diaz Villalba, Diego Alonso |
| u202411799 | Esquicha Alcántara, Diego Alonso |
| u202419655 | Galvez Meza, Salym Pool |
| u202410478 | Vasquez Llave, Oscar Lizandro |

Docente: Mayta Guillermo, Jorge Luis

---

<p align="center">
  Universidad Peruana de Ciencias Aplicadas · 2026
</p>