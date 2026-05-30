Desafío Analytics Engineer - Masterplop
Candidato: Javiera Rehbein Fecha: Mayo 2026
Resumen del Proyecto

Este repositorio contiene la solución al desafío de Analytics Engineer para Masterplop. El objetivo fue procesar datos transaccionales crudos, normalizarlos, generar 5 KPIs estratégicos y evaluar el costo real de la campaña de Cashback de mayo 2024, disponibilizando finalmente la información en un Dashboard interactivo para la gerencia.

Entregables incluidos:

- Archivos .sql con las consultas para cada KPI y el reto principal
- Archivo del Dashboard en Power BI.
- Este documento con justificaciones técnicas y de negocio

--------------------------------------------------------------------------------
💼 Justificación de Negocio: Reto Cashback (Mayo 2024)
Para responder a la pregunta central de la gerencia sobre la campaña de mayo de 2024 (7% de cashback para compras internacionales con crédito chileno, tope de $50 USD), se tomó la siguiente decisión arquitectónica y de negocio:

Cálculo del Tope Dinámico: Para garantizar que ninguna tarjeta recibiera más del beneficio máximo estipulado, estructuré el cálculo en dos fases mediante una Common Table Expression (CTE). En la primera fase, se aisló el universo de transacciones válidas y se calculó el beneficio crudo (SUM(amt * 0.07)). Luego, apliqué una sentencia condicional CASE WHEN para limitar ('capping') matemáticamente el premio a 50 USD por usuario antes de realizar la agregación final de la campaña.

Impacto Real: Esta lógica previno una sobreestimación presupuestaria. El costo total real de la campaña auditado fue de $178.470,91 USD, impactando positivamente a un total de 4.029 tarjetas únicas.

--------------------------------------------------------------------------------
🤖 AI Log (Uso de Inteligencia Artificial)
Durante el desarrollo de este desafío, utilicé IA como asistente de ingeniería para acelerar la resolución de problemas y validar mejores prácticas de modelado, cumpliendo con la cultura Data & AI de Artefact:

Manejo de Fechas para Power BI:
Problema: Las fechas venían en formatos no estandarizados (mezclando guiones y barras).
Solución con IA: La IA me ayudó a anidar STRPTIME y REPLACE para que DuckDB leyera correctamente el campo. Además, me recomendó utilizar DATE_TRUNC('year') casteado a DATE puro para entregarle a Power BI un modelo de fechas estándar, delegando correctamente la jerarquía visual a la herramienta de BI.

Resolución de Configuración Regional (Comas vs. Puntos):
Problema: Al importar los CSV a Power BI, el formato regional en español transformaba erróneamente los decimales (puntos) en separadores de miles (ej. mostrando el costo de campaña en billones).
Solución con IA: En lugar de forzar a SQL a devolver strings con comas (lo cual arruinaría el tipo de dato), la IA me guió para aplicar el paso 'Cambiar tipo usando configuración regional (Inglés - EEUU)' en Power Query. Esto corrigió instantáneamente la visualización en el dashboard respetando la integridad numérica de la base de datos.
