# Ejercicio 1.2.C — Decisión de arquitectura cloud de BiciBarrio

## Enunciado del ejercicio

![Enunciado original del ejercicio](imagenes/image1.png)

**Objetivo:** Tomar y justificar decisiones de arquitectura cloud con criterios de responsabilidad, disponibilidad, coste y cumplimiento.

**Duración:** 90 min. **Equipos:** 3 o 4 personas. **Herramientas:** Google Docs o Notion, Google Sheets.

**Proyecto del módulo — parte 2: decisión cloud**

- Usad el SLO de 1.1.C y vuestras condiciones de capa gratuita.
- Se construye en cinco partes: 1.1.C, 1.2.C, 1.3.C, 1.4.C y 1.4.D.

**Actividades:**

1. Componentes (20 min): web, API de reservas, base de datos, pasarela de pagos, correo y monitorización; modelo de servicio de cada uno.
2. Despliegue, región y disponibilidad (25 min): modelo de despliegue, región de la UE, zonas y recuperación (RTO y RPO).
3. Responsabilidad compartida y seguridad (15 min): matriz de quién gestiona y medidas básicas.
4. Costes (20 min): estimación con las capas gratuitas (hipótesis marcadas), presupuestos y alertas.
5. Riesgos y alternativas (10 min): dependencia del proveedor y plan de salida.

**Entregable:** Memorando de decisión cloud con modelos, región, disponibilidad, costes y riesgos (entregable evaluable del portafolio).

## 1. Componentes

| N.º | IaaS | PaaS | SaaS |
|---|---|---|---|
| 1 | Web | | |
| 2 | | API | |
| 3 | | Base de datos | |
| 4 | | Pasarela de pago | Pasarela de pago |
| 5 | | | Correo |
| 6 | | Monitorización | |

> Se conserva la clasificación original, incluida la pasarela de pago en dos columnas.

## 2. Modelo de servicio

El elegido es **Cloud Service con AWS**. Se decide coger las regiones **eu-south-2** (5 ms–25 ms) y **eu-west-3** (25 ms–35 ms).

Objetivos propuestos de recuperación:

- **RTO: 45 min** (máximo tiempo para recuperar).
- **RPO: 10 min** (máxima pérdida de datos en tiempo).

**Propuesta:** aplicación y base de datos distribuidas en dos zonas de disponibilidad de la región principal; copias recuperables y protegidas contra el borrado en producción en una segunda región de la UE, siempre que el proveedor y el presupuesto lo permitan. Contar con dos zonas reduce el riesgo de caída de un centro de datos; disponer de una copia en otra región ayuda ante un desastre regional, aunque por sí sola no basta para recuperar en 45 minutos. En una evaluación real se comprobarán coste, ubicación, permisos, cifrado, servicios y restauración. No conviene confundir zona con región ni asumir que varias VMs equivalen a varias zonas.

## 3. Responsabilidad compartida y seguridad

| Área | Proveedor | Nosotros |
|---|---|---|
| Datos de clientes y reservas | — | Clasificación, cifrado en reposo (RDS/S3), control de acceso |
| Identidades y accesos | Infraestructura | Gestión de usuarios, roles, MFA, principio de mínimo privilegio |
| Configuración de servicios | — | Configuración segura de S3 (bloqueo público), RDS (no acceso público), Lambda (VPC si aplica) |
| Aplicación (API, web) | — | Código seguro, validación de entrada, gestión de secretos (Secrets Manager) |
| Sistema operativo / runtime | Completamente | — |
| Red física y virtualización | Completamente | Configuración de Security Groups y reglas de red |
| Cumplimiento PCI (pagos) | Stripe (SaaS) | Uso correcto de la API de Stripe; no almacenar datos de tarjeta |

![Tabla original de responsabilidad compartida](imagenes/image2.png)

## 4. Costes

La estimación se presenta en una captura de AWS Pricing Calculator incluida en el documento original.

- **Coste mensual mostrado:** 249,66 USD.
- **Coste total de 12 meses mostrado:** 2.995,92 USD.
- Se incluyen en la estimación servicios de Amazon Aurora PostgreSQL, Amazon CloudWatch, Amazon API Gateway y Amazon Simple Email Service (SES).

![Captura original de la estimación de costes](imagenes/image3.png)

> Las cifras y los servicios se transcriben de la captura. Para conocer cada configuración y supuesto de cálculo, consultar la imagen original.

## 5. Riesgos y alternativas

**Dependencia del proveedor:** se propone usar el ecosistema de AWS con BBDD Aurora.

**Plan de salida:** se propone la exportación de bases de datos a formatos estándar y portabilidad del código de la aplicación.

**Alternativa:** bases de datos localizadas en dos regiones diferentes, en caso de pérdida de poder en una de ellas.

## Evaluación y comentarios recibidos

> El trabajo está bien encaminado y organizado. Se tuvo en cuenta la disponibilidad, la recuperación ante fallos y un plan de salida del proveedor. Para mejorarlo, solo justificaría la clasificación de los servicios y explicar cómo cumplirías los tiempos de recuperación propuestos (que no lo pide aca). Y algo que tal vez no entorpece, debido a que, en Europa sobran centros de AWS …es la determinación de las leyes que rigen en protección de datos.

**Nota: 10.**
