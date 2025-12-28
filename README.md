# ⚽ Análisis de Talento Futbolístico con Power BI
Scouting, rendimiento y valor de mercado basado en datos

📌 Objetivo del proyecto

El objetivo de este proyecto es analizar la base de datos de jugadores de fútbol profesional en diferentes equipos y ligas europeas combinando:

rendimiento deportivo (overall, habilidades)

potencial futuro

edad

posición

y valor de mercado

para apoyar procesos de scouting, detección de talento y toma de decisiones deportivas mediante visualizaciones claras, interactivas y orientadas al negocio.

🧠 Preguntas clave que responde el dashboard

Este dashboard fue diseñado para responder, entre otras, las siguientes preguntas:

¿Qué jugadores ofrecen mejor relación rendimiento / valor de mercado?

¿Qué categorías de jugadores concentran el mayor potencial de crecimiento?

¿Cómo influye la edad en el rendimiento según posición?

¿Qué habilidades están más desarrolladas (o faltan desarrollar) en jugadores de alto potencial?

¿Un jugador está sobrevalorado o infravalorado respecto al promedio de su categoría?

🗂️ Dataset utilizado

El dataset contiene información detallada de miles de jugadores profesionales, incluyendo:

Nombre del jugador

Edad

Posición

Overall (rendimiento general)

Potencial

Valor de mercado

Atributos técnicos (finalización, defensa, dribbling, velocidad, etc.)

El volumen y variedad de datos permite análisis tanto descriptivos como comparativos y exploratorios.

🔧 Herramientas y tecnologías

Power BI

Power Query para limpieza y transformación de datos

DAX para:

métricas promedio

comparaciones por categoría

agregaciones dinámicas

Modelado de datos orientado a análisis

📊 Estructura del dashboard(🔹) y decisiones de diseño(👉)

🔹 KPIs principales 

En la parte superior se muestran indicadores clave:

Cantidad total de jugadores

Overall promedio

Edad promedio

Valor de mercado promedio

👉 Permiten tener contexto inmediato y sirven como referencia para evaluar si un jugador está por encima o por debajo del promedio.


🔹 Distribución de jugadores por posición

Gráfico de tipo donut que muestra cómo se distribuyen los jugadores según su rol en el campo.

👉 Útil para entender:

abundancia o escasez de talento por posición,

posibles oportunidades de scouting en roles menos saturados.


🔹 Overall vs Valor de mercado por categoría

Este scatter plot, a mi consideración, es el corazón del análisis que realicé.

Eje X: Overall

Eje Y: Valor de mercado

Color: Categoría del jugador (Elite, Potencial Estrella, Rotación, etc.)

👉 Permite identificar rápidamente:

jugadores infravalorados (alto overall, bajo valor),

jugadores sobrevalorados,

diferencias claras entre categorías.


🔹 Edad vs Overall

Este gráfico analiza la relación entre edad y rendimiento según posición.

👉 Facilita el scouting al permitir:

detectar jugadores jóvenes con alto rendimiento,

comparar picos de rendimiento por rol,

evaluar riesgos asociados a la edad.


🔹 Habilidad específica vs Overall (análisis técnico)

Gráfico interactivo que permite seleccionar una habilidad específica (finalización, defensa, velocidad, etc.) y analizar su relación con el overall.

👉 Muy útil para:

detectar fortalezas técnicas,

identificar áreas de desarrollo,

complementar decisiones de scouting con análisis cualitativo.


🔹 Tabla de jugadores

Tabla ordenada por overall que permite:

identificar rápidamente a los mejores jugadores,

cruzar información con los gráficos,

realizar análisis más detallados a nivel individual.


🎯 Enfoque analítico y valor agregado

Este proyecto no se limita a visualización, sino que aplica:

criterio analítico para elegir qué comparar y cómo,

pensamiento de negocio (valor vs rendimiento),

enfoque de scouting real, no teórico.

Cada gráfico fue diseñado para:

responder una pregunta concreta,

evitar redundancia,

aportar contexto a los demás elementos del dashboard.

🚀 Conclusiones principales

El valor de mercado no siempre crece al mismo ritmo que el rendimiento.

Existen jugadores con alto potencial que aún no reflejan su valor en el mercado.

La edad impacta de manera distinta según la posición.

El análisis por habilidades permite detectar perfiles técnicos específicos más allá del overall.
