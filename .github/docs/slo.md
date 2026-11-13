# Ejercicio 1.1.A — Diagnóstico cultural y flujo de valor de BiciBarrio

## **DEVOLUCION**

Muy Buen trabajo (8/10) comprenden conceptos en general y marca los lineamientos generales y hasta específicos en algunos de ellos. Excelente trabajo en equipo y colaborativo considerando posiciones y roles.

Detalles: el SLI y el presupuesto de errores están correctamente calculados. Revisad la resta de peticiones correctas: son 1.198.860. En el postmortem, diferenciad los errores de toda la semana de los atribuibles al incidente (debemos consultar los registros y las métricas del intervalo 14:10–14:50. Por tanto, no atribuimos automáticamente los 640 errores semanales al incidente) y concretad las acciones con responsable y fecha (cuadro) . Indicad también qué política aplicaríais al haber consumido el 95% del presupuesto, por ejemplo : “Según nuestra política, al superar el umbral del 80%, aplazamos los despliegues no prioritarios y priorizamos la fiabilidad. Solo autorizamos cambios urgentes debidamente revisados, con pruebas y un procedimiento de rollback preparado.

Si alcanzamos el 100% del presupuesto, detenemos los cambios salvo los urgentes, de acuerdo con la política propuesta “

![Imagen del documento original](media/image4.png)

## ![Imagen del documento original](media/image1.png)

## ** 1. Métricas del Flujo de Trabajo **![Imagen del documento original](media/image3.png)

- **Trabajo Activo Total:** $25.5$ horas

- **Tiempo de Espera Total:** $152$ horas

- **Plazo Total:** $177.5$ horas ($25.5h\ activo + 152h\ espera$, equivalente a $7.4$ días continuos)

- **Eficiencia del Flujo:** **14.37%** ($\frac{25.5}{177.5} \times 100$)

**Conclusión del cálculo:** Sólo el **14.37%** del tiempo total del ciclo representa trabajo activo real. El **85.63%** restante corresponde a tiempo de espera.

**2. Identifica los tres mayores cuellos de botella**

1.  **Despliegue manual (sábado por la noche):** 56 horas (36.8% del tiempo total de espera)

2.  **Aprobación del comité de cambios:** 40 horas (26.3% del tiempo total de espera)

3.  **Pruebas manuales de QA:** 32 horas (21.1% del tiempo total de espera)

**3. Relaciona las carencias con los pilares CALMS**

**3. Relaciona las carencias con los pilares CALMS

**![Imagen del documento original](media/image2.png)

**C** Falta “Cultura de colaboración”, se intenta buscar un culpable en vez de responsabilidad compartida.

**A** Falta de automatización de procesos (pruebas QA, Despliegue, PR)

**L** Existen múltiples cuellos de botella.

**M** Con los datos proporcionados se puede medir:

Sólo el **14.37%** del tiempo total del ciclo representa trabajo activo real. El **85.63%** restante corresponde a tiempo de espera.

**S** No hay colaboración ni comunicación como se observa en los tiempos de espera.

4.  **Propón tres mejoras y estima el nuevo plazo total si las aplicas.**

C y S Mejora de la comunicación entre los diferentes departamentos para mejorar los tiempos de espera.

A Implementar herramientas de automatización para Test y Despliegues más agiles.

L y M Despliegues más sencillos y ágiles con procedimientos simples.

1.1.C

1\. Datos del caso

Periodo: 30 días, peticiones 1200000, Errores 5xx, 1º semana 210, 2º 160, 3º 640, 4º 130,

2\. SLO y presupuesto.

210+160+640+130= 1140 total

1200000-1140= 1198160

1.200.000 − 1.140 = 1.198.860

1198160/1200000 \* 100 = 0,99905 \* 100 = 99,905 = 99,91% → SLI

Presupuesto en peticiones 1.200.000 x (1 -0.999)= 1200 errores

Presupuesto en minutos = 30 × 24 × 60 × 0,001 = 43,2 minutos.

Porcentaje del mes seria 95%

Hemos consumido el 95% del presupuesto de errores del mes; quedan 60 peticiones fallidas de margen.

3\. Politicas de errores

\>50% Revisar los cambios más a fondo y hacer más pruebas.

\>=80% Priorizar despliegues urgentes y descartar despliegues no prioritarios y priorizar la fiabilidad.

100% Para los cambios salvo los urgentes

4\. Postmorten

**Plantilla de postmortem**

1.  **Resumen** y gravedad.

2.  **Impacto** (usuarios afectados, duración, presupuesto de errores consumido).

3.  **Cronología** (detección, respuesta, resolución).

4.  **Causas** y factores contribuyentes.

5.  **Qué funcionó** y qué no.

6.  **Acciones** con responsable y fecha.

7.  **Lecciones aprendidas**.

Resumen y gravedad

El martes a las 14:10, un despliegue rutinario provocó que el servicio de reservas devolviera errores 5xx durante unos 40 minutos, afectando a unas 640 peticiones. El equipo restauró el servicio revirtiendo a la versión estable anterior. No hubo pérdida de datos.

SEV1. Servicio caído para la mayoría de usuarios.

Impacto

- Duración 40 min. Parte de las personas no pudieron completar reservas durante la franja de mediodía

- 640 errores durante la semana del incidente, sin que podamos identificar el número de errores causado por ese incidente.

Cronología

- El martes de la semana 3 a las 14:10h hubo un incidente en el despliegue que duro 40 min

- 14:50h se restableció el servicio realizando un “rollback”

Causas y factores

- Despliegue realizado el martes a las 14:10h configuración no cubierta por pruebas y reversión manual.

Que funcionó y qué no

- Rollback funcionó como se esperaba y revirtió los cambios.

Acciones

- Revisar las alertas de errores por parte de Operaciones

Lecciones aprendidas

- Validar la configuración antes de realizar un despliegue

- Realizar pruebas más exhaustivas antes de lanzar los despliegues.

- Mejorar los tiempos de Rollback

- Evitar desplegar en horas críticas

- Despliegues progresivos
