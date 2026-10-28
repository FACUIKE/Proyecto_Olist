# 📦 Análisis de E-Commerce y Optimización Logística (Olist)

## 📊 Descripción del Proyecto
Este proyecto analiza la base de datos pública de **Olist**, la plataforma de e-commerce más grande de Brasil. El objetivo principal es identificar los cuellos de botella logísticos, entender qué variables impactan más en la satisfacción del cliente y proporcionar un panel de control ejecutivo para la toma de decisiones comerciales.

A través de un enfoque end-to-end (desde la limpieza de datos crudos hasta el despliegue de un dashboard), el proyecto combina **Ingeniería de Datos**, **Machine Learning** y **Business Intelligence**.

---

## 🛠️ Stack Tecnológico
*   **Lenguaje & Entorno:** Python (Jupyter Notebook / Visual Studio Code)
*   **Manipulación de Datos:** Pandas, NumPy
*   **Machine Learning:** Scikit-Learn (Random Forest Classifier)
*   **Business Intelligence & Dataviz:** Power BI (DAX, Data Modeling)

---

## ⚙️ Arquitectura y Metodología del Proyecto

1. **ETL y Limpieza de Datos (Python):** 
   * Integración de múltiples datasets relacionales (Pedidos, Clientes, Productos, Ítems, Reseñas).
   * Tratamiento de valores nulos, estandarización de claves (IDs) y conversión de tipos de datos (DateTime).
   * Filtrado exclusivo de pedidos exitosos (`status == 'delivered'`) para no sesgar las métricas financieras.

2. **Ingeniería de Variables (Feature Engineering):**
   * Creación de variables de negocio críticas: `delivery_time_days` (tiempo real de entrega), `delivery_delay_days` (días de retraso respecto a la estimación), y `freight_ratio` (impacto del costo de envío sobre el precio del producto).

3. **Modelado Predictivo de Satisfacción:**
   * Entrenamiento de un modelo **Random Forest** para predecir si un cliente estará "Satisfecho" (4-5 estrellas) o "Insatisfecho" (1-3 estrellas).
   * **Hallazgo clave del modelo:** La variable `delivery_delay_days` demostró ser el factor con mayor peso y poder predictivo sobre la destrucción de la satisfacción del usuario.

4. **Modelado de Datos (Esquema Estrella):**
   * Ruptura del dataframe consolidado en un esquema relacional optimizado para motores de BI: `Dim_Customers`, `Dim_Products` y `Fact_Sales`.

5. **Visualización y KPIs (Power BI):**
   * Desarrollo de un Dashboard dividido en dos perspectivas: **Visión Comercial** (Ventas, Categorías, Ticket Promedio) y **Rendimiento Logístico** (Tasa de entregas tardías por estado, mapa de calor y análisis de dispersión Tiempo vs. Satisfacción).

---

## 💡 Conclusiones y Decisiones de Negocio (Insights)

*   🏆 **Líderes de Facturación:** La categoría *Health & Beauty* (Salud y Belleza) es el motor principal de ingresos de la plataforma, superando los $49 millones, seguida por *Computers & Accessories*.
*   ⏱️ **El dolor de la Logística:** El tiempo promedio de entrega a nivel nacional se sitúa en **11,96 días**. Sin embargo, existe una correlación negativa perfecta: a medida que este número crece, la tasa de satisfacción (promedio 76.8%) se desploma.
*   🚨 **Zonas Críticas:** El análisis geográfico reveló que el estado de **Alagoas (AL)** presenta una tasa de entregas tardías superior al **20%**, muy por encima de la media nacional (6.48%). Esto requiere una renegociación urgente de SLAs (Service Level Agreements) con los transportistas que operan en la región noreste.

---

## 📂 Estructura del Repositorio
```text
├── .gitignore
├── README.md
├── CSV/
│   ├── (datasets exportados para BI: BI_dim_customers.csv, etc. - Ignorados por Git)
├── poweBI_Olise/
│   └── Dashboard_Olist.pbix   # Archivo final de Power BI
└── limpieza_datos.ipynb       # Notebook con todo el proceso de ETL y ML