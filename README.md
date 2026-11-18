# 🎬 StreamFlix — Análisis de Retención y Efectividad de Catálogo (Power BI)

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![Prompt Engineering](https://img.shields.io/badge/Prompt%20Engineering-RCTF-6E40C9?style=for-the-badge)

![Dashboard Principal](img/dashboard_principal.png)

## 📌 Contexto del Negocio
**StreamFlix** es una plataforma de streaming de series y películas que buscaba evaluar la efectividad real de su catálogo para optimizar futuras inversiones en producción y adquisición de contenidos. 

A partir de un modelo analítico en estrella (*Fact_Visualizaciones* cruzada con dimensiones de *Contenido, Usuario, Plan, Dispositivo y Fecha*)[cite: 3], se desarrolló este tablero ejecutivo para responder preguntas clave del Director de Programación sobre comportamiento de consumo, retención por formato, rendimiento por género y calidad de casas productoras[cite: 3].

---

## 📊 KPIs Principales y Medidas DAX

Sobre un total de **1.000 eventos de visualización** analizados, se construyeron las siguientes métricas clave en DAX:

```dax
// Volumen total de consumo en la plataforma (Resultado: 57.449 min)
Minutos Totales = SUM(Vista_Analisis_Visualizaciones[minutos_visualizados])

// Porcentaje promedio de títulos finalizados (Resultado: 63,80%)
Tasa Completitud = AVERAGE(Vista_Analisis_Visualizaciones[completado_flag])



💡 Insights de Negocio y Recomendaciones1. Películas vs. Series (Volumen vs. Fidelización)Hallazgo: Las Películas concentran el 72,76% del volumen total consumido (41.799 min) debido a su mayor duración individual, pero las Series lideran en eficiencia y retención con un Engagement Rate del 76,02% (vs. 73,92% en películas) y una Tasa de Completitud del 65,68% (vs. 62,12% en películas).   Acción recomendada: Incrementar la participación de series episódicas en el catálogo y configurar recomendaciones algorítmicas al finalizar cada película para redirigir al usuario hacia series del mismo género (binge-watching).2. Rendimiento por Género y ProductorasHallazgo: Thriller lidera en minutos totales (15.616 min), pero registra la tasa de completitud más baja (58,25%), evidenciando abandono temprano. En contraste, Drama alcanza la mayor retención de toda la plataforma (79,28% de Engagement Rate y 72,00% de completitud). A nivel proveedores, Drama Works lidera en calidad con un 72,39% de completitud.   Acción recomendada: Priorizar inversión en producciones de Drama y auditar los guiones/ritmo de los títulos de Thriller antes de renovar contratos con productoras de baja completitud.⚙️ Arquitectura de Automatización e IA AplicadaPropuesta de Automatización (End-to-End)Para eliminar la exportación manual semanal de archivos CSV:Ingesta (ETL): Conexión directa desde Power BI hacia el Data Warehouse / base de datos OLTP mediante vistas SQL.Transformación: Limpieza, tipado de datos y reglas de negocio automatizadas en Power Query.Actualización y Alertas: Publicación en Power BI Service con Scheduled Refresh y alertas basadas en umbrales críticos de caída en el Engagement Rate para evitar fatiga de notificaciones (Alert Fatigue).Prompt Engineering (Metodología RCTF)Se diseñó un prompt estructurado bajo el marco Rol - Contexto - Tarea - Formato para asistir al equipo de programación en la selección de catálogo mediante IA Generativa:[ROL] Actuá como un Director de Programación y Estratega de Contenidos experto en plataformas de streaming de video.[CONTEXTO] Planificamos la estrategia de adquisición de catálogo para StreamFlix contando con métricas históricas de minutos visualizados, tasa de completitud, engagement rate y formato (películas vs. series).[TAREA] Analizá el rendimiento histórico del catálogo para identificar los géneros que mejor combinan volumen y retención, recomendando prioridades de inversión.[FORMATO] Informe ejecutivo con Resumen Ejecutivo, Tabla Comparativa de Géneros, Justificación Estratégica y Recomendaciones Concretas.🛠️ Stack Tecnológico & HabilidadesModelado y BI: Power BI Desktop, DAX, Power Query (ETL), Modelado Dimensional (Esquema Estrella)[cite: 3].Análisis de Datos: KPIs de Retención, Análisis de Cohortes/Segmentación, Data Storytelling.IA Generativa: Diseño de Prompts Estructurados (Metodología RCTF).📂 Estructura del RepositorioStreamFlix_Dashboard.pbix: Archivo fuente completo del tablero interactivo en Power BI.Vista_Analisis_Visualizaciones.csv: Dataset utilizado para el modelado y las visualizaciones[cite: 2]./img: Capturas de pantalla en alta resolución del dashboard.

// Eficiencia real de visualización respecto a la duración total (Resultado: 74,48%)
Engagement Rate = DIVIDE(
    SUM(Vista_Analisis_Visualizaciones[minutos_visualizados]), 
    SUM(Vista_Analisis_Visualizaciones[duracion_total_min])
)
