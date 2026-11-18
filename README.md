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

// Eficiencia real de visualización respecto a la duración total (Resultado: 74,48%)
Engagement Rate = DIVIDE(
    SUM(Vista_Analisis_Visualizaciones[minutos_visualizados]), 
    SUM(Vista_Analisis_Visualizaciones[duracion_total_min])
)
