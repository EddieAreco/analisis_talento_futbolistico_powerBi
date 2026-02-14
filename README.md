⚽ Dashboard de Análisis de Scouting de Fútbol - Power BI

<img width="1486" height="817" alt="image" src="https://github.com/user-attachments/assets/9b635fa7-a0ca-4c33-a895-c16a8b7444e1" />

📌 Objetivo del proyecto
Este proyecto nace como un desafío técnico personal para desarrollar habilidades avanzadas en análisis de datos y visualización de información mediante Power BI. El objetivo principal fue trabajar con un dataset de gran volumen (18,278 registros) y alta complejidad dimensional (89 atributos por jugador) para:

Aplicar técnicas avanzadas de modelado dimensional y transformación de datos
Desarrollar métricas derivadas complejas mediante DAX
Crear índices compuestos que sinteticen múltiples variables en indicadores accionables
Diseñar un dashboard interactivo con cross-filtering y drill-down jerárquico
Implementar best practices de visualización de datos y experiencia de usuario

Si bien el proyecto fue concebido como ejercicio de desarrollo de competencias técnicas, el resultado final es un sistema de análisis funcional que puede ser utilizado por evaluadores de talento deportivo (scouts profesionales) para:

Identificar jugadores con alto potencial de crecimiento a bajo costo (oportunidades de inversión)
Comparar perfiles tácticos mediante índices multidimensionales
Analizar distribución geográfica del talento futbolístico
Evaluar relaciones entre calidad, costo de fichaje y salarios
Tomar decisiones basadas en datos para la contratación de jugadores

El enfoque del dashboard no es simplemente mostrar estadísticas FIFA, sino traducir 89 atributos raw en insights estratégicos que faciliten la toma de decisiones en entornos de scouting real.

🧠 Preguntas clave que responde el dashboard
El dashboard fue diseñado para responder, entre otras, las siguientes preguntas:
Análisis de Oportunidades de Inversión:

¿Qué jugadores ofrecen el mejor retorno sobre inversión (ROI) considerando su potencial de mejora?
¿Cuáles son los jóvenes promesas más subevaluados del mercado?
¿Existen jugadores de categorías "Esporádico" o "Rotación" con alto potencial que podrían convertirse en titulares?

Análisis de Perfiles Tácticos:

¿Qué posiciones tienen el mejor balance entre capacidad ofensiva y defensiva?
¿Cómo se distribuyen las habilidades técnicas, físicas y tácticas por posición?
¿Qué jugadores son "completos" (altos índices en múltiples dimensiones)?

Análisis de Mercado:

¿Qué países concentran la mayor cantidad de talento elite?
¿Cuál es la distribución de jugadores por categoría de calidad?
¿Cómo varía el valor de mercado promedio según la edad del jugador?

Análisis Comparativo:

¿Cómo se compara un jugador específico con el promedio de su posición?
¿Qué jugadores están sobrevalorados o subvalorados respecto a sus capacidades?
¿Cuál es la curva de rendimiento típica según la edad?

Estas preguntas guían toda la estructura analítica y visual del dashboard.

🗂️ Dataset utilizado
Fuente: FIFA Players Dataset - Kaggle
El dataset contiene información exhaustiva de 18,278 jugadores de fútbol extraída del videojuego FIFA, desagregada en 89 atributos que incluyen:
Datos de Identificación:

Nombre del jugador
Edad
Nacionalidad
Club actual
Posiciones (hasta 3 posiciones por jugador)

Métricas de Rendimiento:

Overall (habilidad general actual)
Potential (máximo potencial alcanzable)
6 atributos generales (pace, shooting, passing, dribbling, defending, physic)
29 atributos específicos (finishing, positioning, marking, tackling, etc.)
5 atributos de portero
24 ratings por posición (ST, CB, CM, etc.)

Datos Económicos:

Valor de mercado (value_eur)
Salario semanal (wage_eur)

Características Físicas:

Altura
Peso
Pie preferido
Skill moves
Weak foot

Transformaciones aplicadas
A partir de estos datos se realizaron las siguientes transformaciones en Power Query:

Conversión de formatos monetarios:

value_eur y wage_eur parseados desde formato "K" (ej: "450K") a valores numéricos
Estandarización de tipos de datos (String, Int64, Double)


Creación de tabla dimensional "Dimension positions":

Code position (ST, CB, CM, etc.)
Name (nombre completo de la posición)
Field line (Ataque, Mediocampo, Defensa, Portero)
Category (Ofensiva, Defensiva, Mixta)


Creación de tabla dimensional "Age Ranges":

Age (edad numérica)
Phase (Promesa: 16-21, Desarrollo: 22-25, Pico: 26-30, Veterano: 31+)


Creación de tabla dimensional "Investment Ranges":

Value_Min, Value_Max (rangos en euros)
Budget_Tier (Low Cost, Mid Market, High Value, Premium, Elite)



El volumen y granularidad del dataset permiten realizar análisis:

Temporales (evolución por edad)
Comparativos (jugador vs promedio, posición vs posición)
Estructurales (distribución geográfica, composición por categoría)
Exploratorios (descubrimiento de oportunidades)


🔧 Herramientas y tecnologías utilizadas
Power BI Desktop
Plataforma principal de desarrollo del dashboard.
Power Query (M Language)
Utilizado para:

Limpieza de datos: eliminación de valores nulos, estandarización de formatos
Transformación de columnas: conversión de tipos, parsing de strings monetarios
Creación de tablas dimensionales: diseño de tablas de referencia para clasificación

DAX (Data Analysis Expressions)
Utilizado para:
Columnas calculadas (6 índices compuestos):
daxAttacking Index = 
VAR score_finishing = SWITCH(TRUE(), [attacking_finishing] >= 80, 30, ...)
VAR score_positioning = SWITCH(TRUE(), [mentality_positioning] >= 80, 25, ...)
...
RETURN suma_ponderada_0_100
Medidas agregadas (14 medidas):

Contadores: Total players, Elite Players, Young Prospects
Promedios: Average Overall, Average Value
ROI: ROI Value, ROI Wage, ROI Potencial
Comparativos: Overall vs avg, Value vs avg
Lookup helpers: Position Name, Investment Player, Age Phase

Técnicas DAX aplicadas:

SWITCH(TRUE()) para scoring condicional ponderado
CALCULATE() con ALL() para forzar contexto completo
SELECTEDVALUE() para valores únicos en contexto de fila
LOOKUPVALUE() para relaciones calculadas
DIVIDE() con manejo de divisiones por cero
AVERAGEX() para iteradores de fila

Modelado de Datos
Arquitectura dimensional star schema con:

1 tabla de hechos: Players_Data (18,278 filas × 89 columnas)
4 tablas dimensionales: Dimension positions, Age Ranges, Investment Ranges, Index Group
1 tabla de métricas: Calculated metrics (14 medidas DAX)
1 jerarquía: nationality → club (drill-down geográfico)


📊 Metodología de Creación de Índices Compuestos
Concepto
Los índices compuestos son métricas derivadas que sintetizan múltiples atributos raw en un único valor normalizado (escala 0-100). Esta técnica permite:

Reducir complejidad (83 atributos → 6 índices)
Facilitar comparaciones
Ponderar atributos según importancia táctica
Crear perfiles multidimensionales

Índices implementados
1. Attacking Index (0-100)
Mide capacidad ofensiva combinando:

attacking_finishing (30 pts máx) - Definición
mentality_positioning (25 pts máx) - Posicionamiento ofensivo
attacking_volleys (20 pts máx) - Remates de volea
attacking_crossing (15 pts máx) - Centros
attacking_heading_accuracy (10 pts máx) - Cabezazos

Interpretación: >80 = Elite ofensivo | 60-79 = Bueno | <60 = Limitado
2. Defense Index (0-100)
Mide capacidad defensiva combinando:

defending_marking (30 pts máx) - Marcaje
defending_standing_tackle (25 pts máx) - Entrada de pie
mentality_interceptions (20 pts máx) - Interceptaciones
defending_sliding_tackle (15 pts máx) - Barridas
power_strength (10 pts máx) - Fuerza física

Interpretación: >80 = Elite defensivo | 60-79 = Confiable | <60 = Vulnerable
3. Physic Index (0-100)
Mide atributos físicos combinando:

movement_sprint_speed (25 pts máx) - Velocidad punta
movement_acceleration (25 pts máx) - Aceleración
power_stamina (20 pts máx) - Resistencia
power_strength (15 pts máx) - Fuerza
power_jumping (15 pts máx) - Salto

Interpretación: >75 = Atleta de elite | 50-74 = Promedio | <50 = Limitaciones físicas
4. Skill Index (0-100)
Mide habilidad técnica combinando:

skill_dribbling (30 pts máx) - Regate
skill_curve (25 pts máx) - Efecto
skill_ball_control (20 pts máx) - Control
skill_long_passing (15 pts máx) - Pase largo
skill_fk_accuracy (10 pts máx) - Tiros libres

Interpretación: >80 = Técnicamente dotado | 60-79 = Competente | <60 = Básico
5. Technical and Movilitie Index (0-100)
Mide técnica + movilidad combinando:

skill_ball_control (30 pts máx) - Control de balón
skill_dribbling (25 pts máx) - Conducción
attacking_short_passing (20 pts máx) - Pase corto
mentality_vision (15 pts máx) - Visión de juego
mentality_composure (10 pts máx) - Compostura

Interpretación: >80 = Playmaker | 60-79 = Organizador | <60 = Funcional
6. Goalkeeper Index (0-100)
Mide capacidad de portero combinando:

goalkeeping_reflexes (30 pts máx) - Reflejos
goalkeeping_diving (25 pts máx) - Estiradas
goalkeeping_positioning (20 pts máx) - Posicionamiento
goalkeeping_handling (15 pts máx) - Manejo
goalkeeping_kicking (10 pts máx) - Despeje

Interpretación: >85 = Elite | 70-84 = Confiable | <70 = Riesgoso
Validación de Índices
Los índices fueron validados mediante matriz heatmap que confirma coherencia táctica:

ST: Attacking Index alto (61.23) + Defense Index bajo (8.77) ✓
CB: Defense Index alto (67.39) + Attacking Index bajo (4.61) ✓
CM: Balance entre Attack (40.85) y Defense (42.69) ✓


📊 Estructura del dashboard y decisiones de diseño
🔹 KPIs principales (6 cards superiores)
Cards implementadas:

Cantidad de jugadores - Total del dataset contextual
Overall promedio - Nivel de calidad promedio (métrica de referencia)
Valor de mercado promedio - Inversión promedio requerida
ROI Value Promedio - Eficiencia calidad/costo
Jugadores Elite 🏆 - Cantidad con overall ≥85
Jóvenes Prospectos 🌟 - Cantidad en categorías "Fuera de serie" + "Potencial Estrella"

👉 Decisión de diseño:
Estas métricas proporcionan contexto inmediato antes de profundizar en análisis granular. Funcionan como norte estratégico para interpretar el resto del dashboard.

🔹 Tabla detallada con formato condicional
Columnas (14 total):

Identificación: name, Overall, Fase Edad, Tipo inversión, Edad, Posicion
Índices: Ataque, Defensa, Portería, Físico, Habilidad, Técnica
ROI: ROI Potencial, ROI Value, ROI Wage
Contexto: Future Potencial, Categoría

Formato condicional aplicado:

Escalas de color en índices (0-100):

Verde: 80-100 (Elite)
Amarillo: 60-79 (Bueno)
Naranja: 40-59 (Regular)
Rojo: 0-39 (Bajo)


Escala en ROI Potencial:

Verde oscuro: >50 (excelente oportunidad)
Verde claro: 20-50 (razonable)
Gris: <20 (limitado)



👉 Decisión de diseño:
Esta tabla es el núcleo operativo del dashboard. Permite:

Ordenamiento dinámico por cualquier métrica
Comparación side-by-side de múltiples jugadores
Identificación visual inmediata de fortalezas/debilidades
Exportabilidad para análisis offline

Casos de uso:

Click en Matrix Heatmap (posición CB) → Ordenar tabla por "Defense Index" → Shortlist de mejores defensas
Click en Donut (categoría "Esporádico") → Ordenar por "ROI Potencial" → Gangas identificadas
Click en Treemap (país "Spain") → Ordenar por "Overall" → Talentos españoles


🔹 Distribución por categoría (Donut Chart)
Categorías (7 niveles):
Segmentación automática basada en overall y potential:

Fuera de serie (overall ≥90)
Elite (85-89)
Potencial Estrella (potential - overall ≥15, age <23)
Titular (70-84)
Esporádico (60-69)
Rotación (50-59)
Jugador de banca (<50)

👉 Decisión de diseño:
Proporciona visión estructural de la distribución del talento. Permite identificar rápidamente qué segmentos tienen mayor representación y facilita análisis de concentración.
Insight clave obtenido:

Esporádico: 51.94% del dataset, ROI Value 35.84
Elite: 0.3%, ROI Value 1.3
Conclusión: Segmento Esporádico ofrece 27x mejor ROI que Elite


🔹 Jugadores con mayor potencial futuro (Column + Line Chart)
Configuración:

Barras: Future Potencial (potential - overall) - TOP 10
Línea: Valor de mercado (eje Y secundario)
Leyenda: Categoría

👉 Decisión de diseño:
Cruza potencial de crecimiento con costo de fichaje para identificar las mejores inversiones. El uso de doble eje permite comparar magnitudes diferentes (puntos vs euros) en un solo gráfico.
Casos de uso:

Identificar jóvenes promesas baratas con alto margen de mejora
Comparar costo vs beneficio potencial
Filtrar por posición y encontrar el mejor prospecto de esa posición


🔹 Perfil multidimensional por posición (Matrix Heatmap)
Configuración:

Filas: Posiciones (ST, CB, CM, etc.) - TOP 10
Columnas: 6 índices compuestos (Attacking, Defense, Physic, Skill, Technical, Goalkeeper)
Valores: AVERAGE de cada índice
Formato: Escala de color rojo-amarillo-verde (0-50-100)

👉 Decisión de diseño:
Este gráfico es la validación de la metodología de índices. Permite:

Verificar coherencia táctica (ST alto en Attack, bajo en Defense)
Identificar perfiles balanceados (CM, CDM)
Comparar requerimientos de cada posición
Tomar decisiones informadas sobre qué índice priorizar por rol

Lectura del heatmap:

Verde intenso = fortaleza de la posición en ese índice
Rojo intenso = debilidad típica de la posición
Amarillo = capacidad intermedia


🔹 Curva de rendimiento por edad (Area Chart)
Configuración:

Eje X: Edad (16-45 años)
Eje Y: Promedio de overall
Área sombreada: Representa volumen de datos

👉 Decisión de diseño:
Muestra la curva natural de rendimiento de jugadores de fútbol:

Crecimiento: 16-26 años
Pico: 27-30 años (overall ~70)
Declive: 31+ años

Utilidad:

Evaluar si un jugador está en su pico o en crecimiento
Decisiones de contratación vs edad (¿pagar premium por pico o invertir en crecimiento?)
Identificar jugadores fuera de la curva (alto rendimiento a edad temprana o tardía)


🔹 Oportunidad de inversión (Horizontal Bar Chart)
Configuración:

Eje Y: Nombre de jugador (TOP 15)
Eje X: ROI Potencial (puntos de mejora por millón invertido)
Color: Categoría

👉 Decisión de diseño:
Ranking directo de mejores oportunidades de inversión. Prioriza jugadores con:

Alto margen de crecimiento (potential - overall)
Bajo costo de fichaje
Resultado: ROI Potencial alto

Casos de uso:

Filtrar por posición (ej: CB) → Ver mejores defensas subevaluados
Filtrar por país (ej: Brazil) → Mejores gangas brasileñas
Sin filtros → Mejores oportunidades absolutas del mercado


🔹 Treemap jugadores por nacionalidad (con drill-down)
Configuración:

Jerarquía: nationality → club
Tamaño: Cantidad de jugadores
Color: AVERAGE(overall) - escala de verde
Interactividad: Drill-down habilitado

👉 Decisión de diseño:
Aprovecha la jerarquía creada para análisis geográfico en dos niveles:

Nivel país: ¿Qué países tienen más talento?
Nivel club (drill-down): ¿Qué clubes de ese país concentran jugadores?

Utilidad estratégica:

Identificar mercados objetivo para scouting
Descubrir países con talento subevaluado
Analizar distribución de calidad promedio por región
Explorar clubes específicos de un país

Interacción:
Click en país → Drill down → Ver distribución por clubes de ese país

🎯 Decisiones de diseño avanzadas
¿Por qué NO hay slicer de posición?
Evaluación realizada: Consideré incluir un slicer de posición, pero decidí que:

El Matrix Heatmap es clickeable y funciona como filtro visual
Los slicers ocuparían espacio valioso en un dashboard ya denso
La tabla detallada ya permite filtrado interactivo
El cross-filtering desde gráficos es más intuitivo que slicers múltiples

Alternativa: Cross-filtering desde Matrix (click en posición) filtra todos los gráficos.
¿Por qué tabla con 14 columnas y no menos?
Razón: La tabla fue diseñada para ser export-ready y contener toda la información crítica para toma de decisiones en un solo lugar. Cada columna tiene una función:

Identificación (5 cols): ¿Quién es y dónde está?
Índices (6 cols): ¿Cómo juega tácticamente?
ROI (3 cols): ¿Vale la pena la inversión?

Eliminar cualquier columna limitaría la capacidad de análisis offline.
¿Por qué índices compuestos y no atributos raw?
Razón: Los 83 atributos del dataset generan parálisis por análisis. Los índices:

Sintetizan información compleja en métricas accionables
Facilitan comparaciones (¿cuál tiene mejor defense?)
Permiten perfiles multidimensionales (radar de 6 índices)
Reflejan conocimiento del dominio (ponderación táctica)

¿Por qué formato condicional en índices?
Razón: Velocidad de lectura visual. Un scout puede:

Identificar fortalezas (verde) y debilidades (rojo) en 2 segundos
Comparar 10 jugadores simultáneamente sin leer números
Detectar patrones (ej: todos los CB tienen verde en Defense)

Esto transforma la tabla de "datos" a "información visual".

🚀 Conclusiones principales
Insights sobre el mercado de jugadores

Concentración de talento elite es extremadamente baja

Solo 54 jugadores (0.3%) tienen overall ≥85
429 jóvenes prospectos (2.3%) identificados con potencial de crecimiento significativo
Implicación: Talento elite es escaso y caro, estrategia debe enfocarse en desarrollo de prospectos


Segmento "Esporádico" ofrece mejor retorno sobre inversión

ROI Value Esporádico: 35.84 puntos por millón
ROI Value Elite: 1.3 puntos por millón
Ratio: 27.6x mejor eficiencia en jugadores de nivel medio
Implicación: Para equipos con presupuesto limitado, priorizar categoría Esporádico maximiza ROI


Validación de coherencia táctica de índices

ST: Attacking Index 61.23 | Defense Index 8.77 ✓
CB: Defense Index 67.39 | Attacking Index 4.61 ✓
CM: Balance Attack 40.85 | Defense 42.69 ✓
Implicación: Los índices compuestos reflejan correctamente roles tácticos reales


Curva de rendimiento sigue patrón esperado

Pico de rendimiento: 27-30 años (overall ~70)
Crecimiento sostenido: 16-26 años
Declive gradual: 31+ años
Implicación: Timing de contratación afecta ventana de rendimiento útil
