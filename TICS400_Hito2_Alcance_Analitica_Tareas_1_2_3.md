# Hito 2 — Alcance, resultados y especificación de métricas

**Asignatura:** TICS400 — Arquitectura Cloud  
**Proyecto:** Plataforma B2B de procesamiento y analítica post-llamada para call centers  
**Responsable del bloque:** Persona 1 — Negocio, datos y analítica  
**Estado:** Tareas 1 y 2 definidas; Tarea 3 en desarrollo (criterios generales y clasificación de interacciones definidos; temas recurrentes y validación detallada pendientes).

---

# 1. Necesidad de negocio, usuarios y alcance

## 1.1. Necesidad de negocio

Los call centers generan grabaciones de las conversaciones entre sus agentes y clientes, las cuales contienen información potencialmente útil para analizar las interacciones, identificar motivos de contacto y reconocer problemas recurrentes. Sin embargo, esta información se encuentra almacenada principalmente en archivos de audio, por lo que requiere un procesamiento previo para transformarse en datos organizados y consultables.

Para obtener estos resultados, las empresas necesitan contar con mecanismos de almacenamiento, transcripción, procesamiento y análisis de datos, lo que implica disponer de infraestructura tecnológica, capacidad de cómputo y recursos para su operación y mantenimiento. Además, procesar las grabaciones de manera individual dificulta consolidar la información y reconocer patrones presentes en múltiples conversaciones.

En este contexto, se identifica la necesidad de contar con un servicio externo que permita delegar el procesamiento de las grabaciones y obtener transcripciones y métricas analíticas de manera estructurada. Esto permitiría que los supervisores y analistas de cada empresa puedan consultar información sobre los motivos de contacto, reclamos y temas recurrentes, sin necesidad de desarrollar y administrar internamente toda la infraestructura necesaria para generar estos resultados.

Esta necesidad corresponde al escenario de negocio propuesto para el proyecto académico. No se dispone todavía de mediciones de una empresa real que permitan cuantificar el costo o el impacto actual del problema.

## 1.2. Usuarios del sistema

La plataforma está orientada a un modelo de negocio B2B (*Business to Business*), en el cual distintas empresas que operan call centers pueden utilizar un mismo servicio de procesamiento y análisis de grabaciones.

Se identifican los siguientes usuarios:

- **Cliente empresarial:** empresas que operan call centers y requieren procesar las grabaciones de sus llamadas. Son quienes contratan el servicio y proporcionan los archivos de audio.
- **Usuarios principales:** supervisores, analistas de datos y analistas de calidad de las empresas clientes. Utilizan las transcripciones y métricas generadas para consultar información, identificar patrones, comparar períodos y realizar análisis según las necesidades de su organización.
- **Usuarios técnicos:** personal responsable de administrar y supervisar el funcionamiento de la plataforma, incluyendo el seguimiento de trabajos de procesamiento, detección de errores y mantenimiento operacional.

Debido a que la plataforma está diseñada para atender a múltiples empresas, cada cliente deberá acceder únicamente a sus propias grabaciones, transcripciones y resultados. La separación de información entre empresas constituye un requisito fundamental del sistema.

## 1.3. Propuesta de valor

La propuesta consiste en ofrecer una plataforma cloud de procesamiento posterior a las llamadas (*post-call processing*) que permita a las empresas externalizar el almacenamiento, la transcripción y el análisis de sus grabaciones.

A diferencia de un servicio limitado a convertir audio en texto, la plataforma buscará transformar las conversaciones en información estructurada mediante la identificación de tipos de interacción, términos relevantes, temas recurrentes y métricas descriptivas. Los resultados podrán consultarse por empresa y período, proporcionando información que cada cliente podrá utilizar para sus propios análisis y decisiones.

El valor del servicio se encuentra tanto en facilitar el acceso a información obtenida de las conversaciones como en permitir que las empresas deleguen la infraestructura y operación tecnológica necesarias para procesarlas.

## 1.4. Alcance del proyecto

El proyecto contempla el diseño de una plataforma B2B capaz de recibir grabaciones de llamadas finalizadas de distintas empresas, procesarlas de manera asíncrona y generar transcripciones junto con resultados analíticos asociados a su contenido.

El alcance inicial considera las siguientes funcionalidades:

1. Recepción y almacenamiento de archivos de audio previamente grabados.
2. Procesamiento asíncrono de las grabaciones.
3. Generación de transcripciones automáticas.
4. Extracción de métricas descriptivas y términos relevantes.
5. Clasificación estimada de las conversaciones según el tipo de interacción: consulta, reclamo o solicitud, incluyendo los resultados mixta e indeterminada.
6. Identificación de temas recurrentes mediante categorías y vocabularios definidos.
7. Consolidación de resultados analíticos por empresa y período.
8. Disponibilidad de transcripciones, métricas y resultados para su consulta.
9. Registro del estado de procesamiento y de posibles errores.
10. Separación de información y accesos entre las distintas empresas clientes.

Se considera un procesamiento por lotes (*batch*), realizado después de que las llamadas hayan finalizado. La plataforma no participa directamente en las conversaciones ni realiza su análisis en tiempo real.

La clasificación del contenido será una estimación automática, por lo que deberá contemplar resultados inciertos y mecanismos de evaluación de su calidad. La técnica específica de clasificación se definirá posteriormente, considerando la viabilidad del proyecto y las pruebas disponibles.

### Funcionalidades fuera del alcance

El proyecto no contempla el desarrollo de una central telefónica, un sistema de grabación de llamadas, un CRM, chatbots, asistentes de atención en tiempo real ni mecanismos para responder automáticamente a los clientes.

Asimismo, se excluye del alcance inicial la evaluación automática de la calidad de atención de los agentes, como el cumplimiento de protocolos, la efectividad de las respuestas o la resolución definitiva de problemas.

La plataforma se enfocará en caracterizar el contenido de las conversaciones y no en evaluar individualmente el desempeño de los trabajadores.

La generación de recomendaciones de negocio también queda fuera del alcance. La plataforma proporcionará información analítica, mientras que cada empresa será responsable de interpretar los resultados y decidir las acciones que considere pertinentes.

---

# 2. Resultados entregados por la plataforma

## 2.1. Descripción general

La plataforma entregará a cada empresa sus transcripciones y un conjunto de métricas obtenidas mediante el procesamiento y consolidación de las llamadas. Los resultados se organizarán en dos niveles: información individual por conversación e indicadores agregados por empresa y período.

El objetivo es que los analistas y supervisores puedan acceder tanto al contenido de una llamada específica como a información que describa patrones presentes en el conjunto de conversaciones procesadas.

Para ello, se consideran tres grupos de resultados: transcripciones individuales, métricas analíticas sobre el contenido y métricas operacionales del procesamiento.

## 2.2. Transcripciones individuales

Cada grabación procesada contará con una transcripción asociada a su identificador de llamada y a la empresa correspondiente.

Junto con la transcripción se conservarán metadatos como fecha, duración y estado de procesamiento, además de los resultados analíticos individuales que puedan obtenerse de la conversación.

Las transcripciones permitirán que los usuarios autorizados consulten el contenido y revisen el contexto de las clasificaciones y términos identificados. Debido a que el reconocimiento automático de voz puede contener errores, estas transcripciones no se considerarán representaciones necesariamente exactas de todo lo expresado durante la llamada.

## 2.3. Métricas analíticas sobre el contenido

Estas métricas constituyen el principal valor analítico de la plataforma, ya que buscan transformar las conversaciones en información que permita comprender qué temas y tipos de interacción aparecen entre los clientes de una empresa.

### A. Clasificación del tipo de interacción

La plataforma buscará clasificar las conversaciones según tres tipos generales: **consulta, reclamo y solicitud**. Además, se contemplan las categorías **mixta** e **indeterminada** para los casos en que no corresponda asignar una de las anteriores.

Estas categorías se proponen como una clasificación general aplicable a distintos tipos de call centers, independientemente del sector al que pertenezcan.

La plataforma permitirá obtener la cantidad y proporción de llamadas asociadas a cada tipo de interacción y comparar su distribución entre diferentes períodos.

**Decisión acordada:** cada llamada tendrá **una sola categoría final**. Si presenta motivos independientes de distinto tipo y no se reconoce uno principal, se utilizará *mixta*. Si no existe información suficiente para clasificarla, se utilizará *indeterminada*. Los criterios completos se detallan en la sección 3.5.

### B. Identificación de términos relevantes

Se identificarán palabras y expresiones relevantes presentes en las transcripciones para conocer qué conceptos aparecen con mayor frecuencia en las conversaciones.

El análisis permitirá distinguir entre la cantidad total de apariciones de un término y el número de llamadas diferentes en las que se menciona. Esto evita interpretar la repetición de una palabra dentro de una misma llamada como evidencia de que está presente en muchas conversaciones.

El conjunto de términos relevantes podrá considerar vocabularios configurables según las necesidades de cada empresa. Asimismo, se deberán establecer criterios para excluir palabras de escaso valor analítico y evitar exponer información personal.

### C. Identificación de temas recurrentes

A partir del contenido de las transcripciones, la plataforma buscará identificar temas que aparezcan repetidamente en las conversaciones de una empresa.

A diferencia del tipo de interacción, que describe la naturaleza de la conversación, el tema representa el asunto tratado. Por ejemplo, una llamada puede clasificarse como **reclamo** y estar asociada al tema **facturación**.

Para mantener la plataforma aplicable a diferentes empresas, se propone utilizar categorías temáticas configurables según el contexto de cada cliente. La identificación inicial podrá apoyarse en términos o reglas asociadas a esas categorías, cuya calidad deberá evaluarse.

Se podrán generar indicadores sobre la frecuencia de estos temas, considerando la cantidad de llamadas en las que aparecen. Una llamada podría estar asociada a más de un tema: esto no contradice que tenga una sola **categoría de tipo de interacción**.

**Pendiente de definición:** vocabulario de configuración, reglas exactas para identificar los temas y tratamiento de temas desconocidos.

### D. Evolución de tipos de interacción y temas

Los resultados se consolidarán por empresa y período, permitiendo observar cómo varía la frecuencia de determinadas categorías, términos y temas a lo largo del tiempo.

De esta manera, los analistas podrán comparar la presencia de distintos motivos de contacto entre períodos, sin que la plataforma tenga que interpretar automáticamente las causas de sus variaciones ni recomendar acciones específicas.

## 2.4. Métricas operacionales

De manera complementaria al análisis del contenido, la plataforma proporcionará métricas descriptivas sobre las grabaciones y su procesamiento.

Se consideran inicialmente:

| Métrica | Descripción |
|---|---|
| Cantidad de llamadas procesadas | Número de grabaciones únicas cuyo procesamiento finalizó correctamente durante el período considerado. |
| Horas de audio procesado | Duración total del audio correspondiente a las llamadas procesadas. |
| Duración promedio | Promedio de duración de las grabaciones incluidas en el análisis. |
| Tiempo de procesamiento | Tiempo transcurrido durante el procesamiento de una grabación, según los puntos de inicio y término que se definan. |
| Tasa de trabajos fallidos | Proporción de trabajos cuyo resultado final fue fallido, según los criterios que se establezcan. |

Estas métricas permitirán conocer el volumen de información procesada y el funcionamiento del servicio. No se utilizarán por sí solas como indicadores de la calidad de atención de los agentes.

## 2.5. Consulta y utilización de resultados

Los resultados estarán organizados por empresa, permitiendo realizar consultas sobre llamadas individuales y obtener indicadores agregados correspondientes a períodos específicos.

Los usuarios autorizados podrán consultar las transcripciones y los resultados analíticos de su empresa, manteniendo la separación de información respecto de los demás clientes de la plataforma.

La entrega de información se enfocará inicialmente en disponer de datos estructurados y consultas analíticas. El desarrollo de un dashboard completo no se considera un requisito del alcance inicial.

La plataforma no determinará qué decisiones debe tomar cada empresa a partir de los resultados obtenidos. Su responsabilidad será generar información consultable, trazable y acompañada de las limitaciones correspondientes.

## 2.6. Consideraciones y limitaciones

La clasificación automática de las conversaciones y la identificación de temas recurrentes constituyen capacidades propuestas para el sistema, cuya precisión y viabilidad técnica deberán evaluarse durante el desarrollo.

Los resultados podrían verse afectados por errores de transcripción, expresiones ambiguas, diferencias de vocabulario y características particulares de cada empresa.

Por ello, el sistema deberá contemplar categorías indeterminadas, mantener referencias a las transcripciones y permitir que los resultados puedan ser contrastados con su contenido original.

Las definiciones exactas de cálculo, reglas de clasificación, períodos de agregación, tratamiento de duplicados y criterios de evaluación se desarrollarán en la etapa de especificación de métricas. Las primeras decisiones de esa etapa se presentan a continuación.

---

# 3. Especificación de métricas y reglas de análisis

## 3.1. Criterios generales

Las métricas generadas por la plataforma se calcularán a partir de las grabaciones procesadas y sus respectivas transcripciones, manteniendo la identificación de la empresa a la que pertenece cada llamada.

Para evitar duplicidades, cada llamada deberá contar con un identificador único dentro de su empresa. Los reintentos de procesamiento no deberán generar registros adicionales en los resultados analíticos.

Se distinguirán dos grupos de indicadores: métricas relacionadas con el contenido de las conversaciones y métricas operacionales asociadas al volumen de grabaciones y al funcionamiento de la plataforma.

Los indicadores analíticos utilizarán como referencia la **fecha original de cada llamada**, permitiendo comparar los resultados entre períodos. Las métricas de funcionamiento utilizarán los registros de ejecución del procesamiento.

Los resultados agregados del contenido incluirán únicamente llamadas cuyo procesamiento haya finalizado correctamente. Las llamadas con fallos técnicos o pendientes no se clasificarán como indeterminadas: se registrarán por separado como trabajos sin análisis completado.

Las consultas deberán restringirse siempre a la empresa correspondiente. La identificación de la empresa utilizada para separar y autorizar resultados deberá ser confiable; no basta con aceptar sin validación cualquier identificador enviado por el cliente.

## 3.2. Métricas analíticas del contenido

### Distribución de tipos de interacción

Se calculará la cantidad y proporción de llamadas clasificadas según su tipo de interacción. Se consideran las categorías **consulta, reclamo, solicitud, mixta e indeterminada**.

Para una empresa y período dados, se utilizará la cantidad de llamadas **únicas** procesadas correctamente e incluidas en ese período. Cada llamada aportará una sola categoría al resultado, de forma que la suma de los conteos por categoría coincida con el total analizado.

Los criterios para asignar estas categorías se describen en la sección 3.5, evitando asignaciones arbitrarias en conversaciones ambiguas.

### Frecuencia de temas recurrentes

Se calculará la cantidad de llamadas asociadas a cada tema identificado en las transcripciones.

Los temas podrán variar según el contexto de cada empresa. Una conversación podrá asociarse a más de un tema cuando su contenido lo justifique. Su frecuencia considerará la cantidad de llamadas distintas en las que se identifica, evitando que múltiples menciones dentro de una misma conversación se contabilicen como varias llamadas.

Las categorías temáticas y el procedimiento exacto de identificación permanecen pendientes de especificación.

### Frecuencia de términos relevantes

Se identificarán las apariciones de palabras y expresiones relevantes dentro de las transcripciones.

Para cada término se distinguirán dos medidas:

1. **Menciones totales:** número de veces que aparece el término en el conjunto seleccionado.
2. **Llamadas con el término:** número de llamadas distintas en las que aparece al menos una vez.

Se establecerán criterios de normalización y exclusión de palabras comunes, así como protección frente a la exposición de información personal. Estos criterios todavía deben cerrarse antes de implementar el análisis.

### Evolución temporal de indicadores

Los indicadores anteriores podrán agruparse por períodos para analizar sus variaciones. Se podrán comparar cantidades y proporciones de tipos de interacción, frecuencia de temas y presencia de términos relevantes entre períodos.

Estas comparaciones describirán cambios observados en las conversaciones procesadas, sin atribuir automáticamente sus causas ni emitir recomendaciones de negocio.

## 3.3. Métricas operacionales

De forma complementaria, la plataforma calculará indicadores que permitan conocer el volumen de grabaciones procesadas y el funcionamiento del servicio.

| Indicador | Regla de cálculo propuesta | Aclaración |
|---|---|---|
| Llamadas procesadas | Conteo de llamadas únicas con resultado final exitoso. | Un reintento no agrega una llamada adicional. |
| Horas de audio | Suma de la duración, en segundos, de esas llamadas / 3600. | Mide duración del audio, no el tiempo de ejecución del sistema. |
| Duración promedio | Suma de duraciones / número de llamadas incluidas. | No equivale necesariamente al tiempo medio total de atención. |
| Tiempo de procesamiento | Instante de finalización menos instante de inicio del procesamiento. | La definición exacta de inicio, fin y reintentos está pendiente. |
| Tasa de trabajos fallidos | Trabajos que terminan con resultado final fallido / total de trabajos finalizados × 100. | Excluye pendientes; los intentos de reintento no se contarán automáticamente como trabajos independientes. |

Estas reglas son la base funcional propuesta. Antes de calcular costos o desarrollar el ETL habrá que precisar la unidad de observación, especialmente para los trabajos reprocesados, y fijar cómo se tratan duraciones no disponibles o archivos inválidos.

Estos indicadores no se interpretarán como evaluaciones de la calidad de atención de los agentes.

## 3.4. Consideraciones sobre los resultados

Las métricas obtenidas mediante transcripción y clasificación automática estarán sujetas a posibles errores de reconocimiento e interpretación. Por ello, las clasificaciones deberán contemplar resultados inciertos y conservar referencias a las transcripciones para permitir su revisión.

La selección del método de clasificación, la definición de umbrales y los criterios cuantitativos de evaluación se desarrollarán posteriormente, considerando las características de las conversaciones y la viabilidad técnica de la plataforma.

## 3.5. Reglas de clasificación de las conversaciones

La plataforma contempla un mecanismo de clasificación automática orientado a identificar el **tipo principal de interacción** presente en cada conversación. Esta clasificación permitirá obtener métricas sobre la distribución de consultas, reclamos y solicitudes entre las llamadas procesadas por cada empresa.

Para mantener una estructura común aplicable a distintos tipos de call centers, se establece un conjunto de cinco categorías: **consulta, reclamo, solicitud, mixta e indeterminada**.

Cada llamada procesada correctamente recibirá **una única categoría final**, determinada a partir del propósito principal identificado en su transcripción, o quedará en una de las categorías previstas para casos ambiguos o insuficientes.

### 3.5.1. Definición de categorías

**Consulta:** interacción cuyo propósito principal es obtener información, orientación o aclaraciones. El cliente busca resolver una duda sin solicitar directamente una modificación o gestión específica ni manifestar una disconformidad como motivo principal.

**Reclamo:** interacción en la que el cliente manifiesta un problema, incumplimiento o disconformidad respecto de un producto, servicio o situación. La solicitud de una solución al problema no modifica necesariamente esta clasificación, ya que puede formar parte del mismo reclamo.

**Solicitud:** interacción en la que el cliente requiere que la empresa realice una acción, trámite o modificación, sin que la existencia de un problema o disconformidad constituya el motivo principal de la llamada.

**Mixta:** conversación en la que se identifican dos o más motivos **independientes** pertenecientes a diferentes tipos de interacción y no existe evidencia suficiente para determinar cuál predomina. No se utilizará esta categoría cuando una consulta o solicitud forme parte de la resolución de un único motivo principal claramente identificable.

**Indeterminada:** conversación cuyo propósito no puede establecerse con suficiente claridad debido a información insuficiente, ambigüedad o dificultades en la transcripción. Esta categoría evita asignar una clasificación sin evidencia adecuada.

### 3.5.2. Criterios para determinar la categoría principal

La clasificación deberá considerar el contexto de la conversación y no únicamente la presencia de palabras o expresiones aisladas. Se propone aplicar la siguiente política funcional:

1. **Identificar el propósito de la conversación:** reconocer qué necesita comunicar o resolver el cliente.
2. **Reconocer la intención:** determinar si se busca información, se manifiesta una disconformidad o se solicita una gestión.
3. **Analizar relaciones entre intenciones:** distinguir expresiones que forman parte del mismo problema de motivos realmente independientes.
4. **Determinar el motivo principal:** cuando haya varias intenciones, identificar si alguna constituye claramente el objetivo central de la conversación, considerando las peticiones explícitas del cliente y su contexto general.
5. **Asignar *mixta* cuando corresponda:** si hay motivos independientes de distintos tipos y ninguno predomina claramente.
6. **Asignar *indeterminada* cuando corresponda:** si el texto no permite reconocer el propósito con suficiente evidencia.

Estas son **reglas funcionales acordadas**, no un algoritmo ya implementado ni una garantía de precisión. La forma concreta de convertirlas en lógica de procesamiento o un modelo se evaluará más adelante.

### 3.5.3. Tratamiento de casos especiales

**Reclamos que incluyen solicitudes.** Si un cliente comunica un problema y pide una acción para resolverlo, la categoría principal será *reclamo* cuando ambas expresiones se refieran al mismo motivo.

**Consultas que incluyen solicitudes.** Pedir información sobre cómo realizar un trámite se interpreta como *consulta*, siempre que no se solicite ejecutar el trámite. Pedir que la empresa lo realice corresponde a *solicitud*, salvo que otro motivo sea claramente predominante.

**Conversaciones con motivos independientes.** Primero se intentará determinar el motivo predominante. Si hay motivos de distinto tipo y ninguno es principal con claridad, se utilizará *mixta*.

**Conversaciones con información insuficiente.** Si existe una transcripción, pero no es posible identificar el propósito, se utilizará *indeterminada*. Si falla completamente el procesamiento técnico del audio, no se genera una clasificación: el fallo se registra aparte.

**Menciones de palabras aisladas.** La aparición de expresiones como “reclamo” o “solicito” no determina por sí sola la categoría; se deberá interpretar el significado de la conversación. Por ejemplo, “No tengo ningún reclamo” no constituye evidencia suficiente para clasificar la llamada como *reclamo*.

### 3.5.4. Ejemplos de clasificación

Los siguientes ejemplos son ilustrativos, no resultados del procesamiento automático.

| Conversación | Clasificación esperada | Justificación |
|---|---|---|
| «Quisiera saber cuándo vence mi próxima factura». | Consulta | El cliente solicita información. |
| «Me cobraron dos veces y quiero que me devuelvan el dinero». | Reclamo | La devolución solicitada surge de un problema reportado. |
| «Necesito cambiar mi dirección de facturación». | Solicitud | Se requiere una modificación sin plantear una disconformidad. |
| «Quiero cancelar mi suscripción porque ya no la utilizo». | Solicitud | Se solicita un trámite sin reportar un incumplimiento. |
| «El servicio lleva dos días sin funcionar y necesito que lo arreglen». | Reclamo | Se reporta una falla y se pide resolverla. |
| «Necesito consultar las condiciones del servicio y además presentar un reclamo por un cobro». | Mixta | Son dos motivos independientes y no se identifica uno claramente principal. |
| «Hola, buenos días, llamaba por un asunto...». | Indeterminada | La información disponible no permite identificar el propósito. |

### 3.5.5. Cálculo de la distribución de categorías

Debido a que cada llamada tendrá una única categoría final, las cinco categorías serán mutuamente excluyentes para efectos de los indicadores agregados.

Para cada empresa y período se calculará la cantidad de llamadas correspondientes a cada categoría y su proporción:

\[
P(c) = \frac{N_c}{N_{\text{total}}}\times 100
\]

Donde:

- **\(P(c)\):** porcentaje de llamadas asignadas a la categoría \(c\).
- **\(N_c\):** cantidad de llamadas clasificadas en la categoría \(c\).
- **\(N_{\text{total}}\):** cantidad de llamadas **únicas y procesadas correctamente** de la empresa, incluidas en el período.

Las categorías *mixta* e *indeterminada* forman parte del denominador. Las llamadas con fallos técnicos, todavía pendientes o sin una transcripción procesada correctamente no forman parte de este universo.

De esta forma, la suma de porcentajes será 100 % del conjunto analizado, salvo pequeñas diferencias por redondeo.

### 3.5.6. Limitaciones de la clasificación

Las categorías representan una **estimación automática del propósito** de las conversaciones. Su calidad puede verse afectada por errores de transcripción, expresiones ambiguas, diferencias lingüísticas y conversaciones con múltiples necesidades.

El sistema deberá conservar una referencia a la transcripción y la versión del método de clasificación utilizado, para que un analista autorizado pueda revisar y contrastar los resultados.

La clasificación tampoco constituye una evaluación de la calidad de atención del agente ni confirma que la consulta, reclamo o solicitud haya sido resuelta.

La selección de tecnología y la definición de criterios cuantitativos para evaluar la precisión se realizarán posteriormente, utilizando conversaciones de referencia revisadas manualmente.

## 3.6. Plan preliminar de evaluación de la clasificación

Antes de aceptar los resultados del mecanismo de clasificación se propone:

1. Preparar un conjunto de conversaciones ficticias o autorizadas que represente las cinco categorías y casos ambiguos.
2. Etiquetar manualmente cada ejemplo según las definiciones anteriores, registrando los criterios empleados.
3. Ejecutar el mecanismo automático que finalmente se seleccione.
4. Comparar las etiquetas automáticas con las etiquetas de referencia e identificar en qué categorías se producen errores.

Esta evaluación se plantea como **trabajo futuro**, no como prueba ya realizada. No se fija aún un porcentaje mínimo de precisión, porque primero debe conocerse la calidad y dificultad del conjunto de prueba.

---

# 4. Decisiones acordadas y trabajo pendiente

## 4.1. Decisiones acordadas hasta este punto

- El servicio será una **plataforma B2B para múltiples call centers** y no estará especializado en una única empresa o sector.
- Las empresas **externalizarán el procesamiento** de sus grabaciones y recibirán **transcripciones y métricas consultables**, no únicamente texto transcrito.
- Se procesarán **llamadas finalizadas por lotes**, no audio en tiempo real.
- El valor analítico principal será **comprender tipos de interacción, términos y temas recurrentes**. Las métricas de volumen y funcionamiento son complementarias.
- Se excluye del MVP la **evaluación de calidad de atención de los agentes** y la generación de recomendaciones de gestión.
- Cada llamada tendrá una única etiqueta de tipo: **consulta, reclamo, solicitud, mixta o indeterminada**.
- Los **temas** y los **tipos de interacción** son conceptos distintos; una llamada podrá tener varios temas, pero un único tipo final.
- Los resultados y accesos de una empresa deberán permanecer separados de los de las demás.
- Se considera acceso a resultados estructurados y consultas; un **dashboard completo no es un requisito del MVP**.

## 4.2. Pendientes para terminar la Tarea 3

- Definir **cómo funcionará la configuración de temas por empresa**, cuáles serán sus categorías iniciales y qué ocurre si una conversación no coincide con los temas disponibles.
- Precisar reglas de extracción y normalización de **términos relevantes**, así como exclusión de información personal.
- Acordar **medición y evaluación** del mecanismo de clasificación: conjunto de referencia, errores aceptables y tratamiento de incertidumbre.
- Precisar los **períodos y fórmulas operacionales** cuando existen reintentos, fallos o duraciones no disponibles.

## 4.3. Siguientes tareas de la Persona 1

Una vez cerrada la Tarea 3, el trabajo continuará con:

1. Definir los **campos y contratos de entrada/salida** por empresa y llamada.
2. Preparar **ejemplos ficticios verificables** de al menos dos empresas, con llamadas exitosas, fallidas y repetidas.
3. Especificar qué **extrae, transforma y consolida el ETL**, además de consultas y resultados esperados.
4. Definir **escenarios de carga normal y pico**, retención y frecuencia de consultas como supuestos de negocio.
5. Publicar el **paquete base común** para que las Personas 2 y 3 trabajen de forma independiente, cada una desde la misma versión.

**Nota de alcance:** Este archivo consolida el trabajo funcional realizado hasta ahora. No documenta pruebas ejecutadas de AWS, Ministack, modelos de clasificación, exactitud ni presupuestos calculados.
