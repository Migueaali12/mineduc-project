# 📊 Predicción del Rendimiento Académico en Instituciones Educativas de Loja
## Análisis mediante Modelos de Regresión Lineal Múltiple

**Autores:** Miguel Alvarez y Jorge Ayala  
**Fecha:** 2024  
**Tecnologías:** Python, Pandas, Scikit-learn, Matplotlib, Seaborn

---

## 🎯 **Descripción del Proyecto**

### **Objetivo Principal**
Desarrollar un sistema de predicción del rendimiento académico de estudiantes en instituciones educativas de la provincia de Loja, Ecuador, utilizando técnicas avanzadas de regresión lineal múltiple.

### **Contexto y Datos**
- **Fuente de Datos:** Registros oficiales del Ministerio de Educación (Mineduc)
- **Período:** 2009-2024 (datos de inicio y fin de año lectivo)
- **Alcance:** Provincia de Loja, Ecuador
- **Tipo de Análisis:** Predicción de rendimiento académico institucional

### **Problema a Resolver**
Crear un modelo predictivo que permita:
- Evaluar la calidad educativa de instituciones
- Comparar rendimiento entre diferentes centros educativos
- Identificar factores que influyen en el éxito académico
- Proporcionar herramientas para la toma de decisiones educativas

---

## 📋 **Metodología y Proceso**

### **1. Preparación de Datos**
- **Carga de Datasets:**
  - Dataset principal de Loja (características institucionales)
  - Variables de rendimiento académico
  - Características institucionales predictoras

- **Limpieza y Transformación:**
  - Eliminación de valores nulos
  - Normalización de variables numéricas
  - Codificación de variables categóricas
  - Optimización de memoria para datasets grandes

### **2. Análisis Exploratorio**
- **Exploración de Datasets:**
  - Análisis de dimensiones y tipos de datos
  - Estadísticas descriptivas
  - Visualizaciones de distribución

- **Identificación de Variables:**
  - Variables de rendimiento (objetivo)
  - Variables predictoras (características institucionales)
  - Variables categóricas y numéricas

### **3. Desarrollo del Modelo**

#### **Enfoque Seleccionado: Índice Compuesto de Excelencia (ICE)**
Se implementó un **índice compuesto** que combina múltiples métricas de rendimiento académico:

```python
# Variables del índice ICE:
- Tasa de Retención (25%)
- Tasa de Promoción (30%)
- Control de Deserción (20%)
- Control de Abandono (15%)
- Crecimiento Estudiantil (10%)
```

#### **Cálculo de Variables para el ICE**

Las variables utilizadas en el ICE se calcularon a partir de los datos de matrícula de inicio y fin de año lectivo:

**1. Tasa de Retención de Estudiantes:**
```python
tasa_retencion = (Total_Estudiantes_fin / Total_Estudiantes_inicio) × 100
```

**2. Diferencia de Estudiantes (Crecimiento/Deserción):**
```python
diferencia_estudiantes = Total_Estudiantes_inicio - Total_Estudiantes_fin
```

**3. Porcentaje de Deserción:**
```python
porcentaje_desercion = (diferencia_estudiantes / Total_Estudiantes_inicio) × 100
```

**4. Tasa de Promoción:**
```python
tasa_promocion = (Promovidos / Total_Estudiantes_fin) × 100
```

**5. Tasa de Abandono:**
```python
tasa_abandono = (Abandono / Total_Estudiantes_fin) × 100
```

**Nota:** Todas las variables incluyen validaciones para evitar división por cero y manejar casos donde los datos no están disponibles.

#### **Proceso de Modelado:**
1. **Normalización** de variables de rendimiento (0-100)
2. **Creación del índice ICE** mediante ponderación ponderada:
   - Tasa de Retención: 25%
   - Tasa de Promoción: 30%
   - Control de Deserción: 20%
   - Control de Abandono: 15%
   - Crecimiento Estudiantil: 10%
3. **Selección de variables predictoras** más relevantes
4. **Codificación categórica** con LabelEncoder
5. **División train/test** (80%/20%)
6. **Entrenamiento** con regresión lineal múltiple
7. **Evaluación** mediante métricas estándar

### **4. Optimizaciones Implementadas**
- **Manejo de Memoria:** Muestreo estratificado para datasets grandes
- **Codificación Secuencial:** Procesamiento variable por variable
- **Verificación de Variables:** Comprobación de existencia antes del merge
- **Gestión de Errores:** Manejo robusto de valores faltantes

---

## 🎯 **Resultados Alcanzados**

### **Métricas de Rendimiento del Modelo**

| Métrica | Valor | Interpretación |
|---------|-------|----------------|
| **R² Score** | 0.100 | 10% de varianza explicada |
| **MAE** | 4.87 | Error promedio ±4.9 puntos |
| **RMSE** | 7.84 | Error cuadrático medio |

### **Análisis de Importancia de Variables**

**Top 5 Variables Más Importantes:**

| Ranking | Variable | Coeficiente | Impacto |
|---------|----------|-------------|---------|
| 1 | Modalidad_encoded | -2.594 | Negativo |
| 2 | Regimen_Escolar_inicio_encoded | -1.110 | Negativo |
| 3 | Jornada_encoded | -1.094 | Negativo |
| 4 | Jurisdiccion_inicio_encoded | -0.922 | Negativo |
| 5 | Estudiantes_Femenino | -0.906 | Negativo |

### **Funcionalidades Implementadas**

✅ **Sistema de Predicción Funcional**  
✅ **Comparabilidad entre Instituciones**  
✅ **Identificación de Factores Clave**  
✅ **Visualizaciones Avanzadas**  
✅ **Función de Predicción Optimizada**  

---

## 📊 **Análisis de Resultados**

### **Fortalezas del Modelo**

1. **Funcionalidad Robusta:**
   - Sin crashes de memoria
   - Predicciones consistentes
   - Error bajo en términos absolutos

2. **Identificación de Factores:**
   - Modalidad educativa (más importante)
   - Régimen escolar (Costa/Sierra)
   - Jornada de estudio
   - Jurisdicción (urbana/rural)
   - Composición de género

3. **Herramienta Comparativa:**
   - Permite ranking de instituciones
   - Diferenciación clara entre niveles
   - Baseline para evaluaciones

### **Limitaciones Identificadas**

1. **Baja Explicabilidad (R² = 10%):**
   - Solo explica 10% de la varianza
   - Factores complejos no capturados
   - Necesidad de variables adicionales

2. **Sesgo en Variables:**
   - Todas las variables importantes son negativas
   - Posible sesgo en la codificación
   - Necesidad de análisis más profundo

3. **Variables Limitadas:**
   - Falta de datos socioeconómicos
   - Sin información de calidad docente
   - Sin datos de infraestructura

---

## 🚀 **Oportunidades de Mejora**

### **1. Variables Adicionales Sugeridas**
```python
# Variables que podrían mejorar el modelo:
- Ratio estudiante/docente
- Años de experiencia docente promedio
- Infraestructura educativa
- Nivel socioeconómico del sector
- Resultados históricos de la institución
- Indicadores de calidad docente
```

### **2. Modelos Más Sofisticados**
- **Random Forest:** Captura interacciones complejas
- **XGBoost:** Mejor para patrones no lineales
- **Redes Neuronales:** Relaciones no lineales
- **Ensemble Methods:** Combinación de modelos

### **3. Segmentación por Contexto**
- Modelos específicos por cantón
- Análisis por tipo de sostenimiento
- Evaluación por tamaño de institución
- Modelos por nivel educativo

---

## 🎯 **Impacto y Aplicaciones**

### **Para Autoridades Educativas**
- **Herramienta de Monitoreo:** Seguimiento de rendimiento institucional
- **Toma de Decisiones:** Información para políticas educativas
- **Identificación de Necesidades:** Detección de áreas de mejora

### **Para Instituciones Educativas**
- **Benchmark de Rendimiento:** Comparación con otras instituciones
- **Identificación de Fortalezas:** Análisis de factores positivos
- **Planificación Estratégica:** Base para mejoras

### **Para Investigadores**
- **Base de Datos:** Información para análisis más profundos
- **Metodología:** Framework para estudios similares
- **Validación:** Comparación con otros modelos

---

## 💡 **Conclusiones**

### **Logros Principales**
✅ **Sistema Funcional:** Modelo predictivo operativo  
✅ **Comparabilidad:** Índice ICE unificado  
✅ **Identificación de Factores:** Variables más importantes  
✅ **Herramienta Práctica:** Aplicable en contexto real  
✅ **Base Sólida:** Punto de partida para mejoras  

### **Valor del Proyecto**
- **Baseline Establecido:** Primer modelo funcional para Loja
- **Metodología Validada:** Proceso replicable
- **Insights Valiosos:** Factores que influyen en rendimiento
- **Herramienta Comparativa:** Sistema de evaluación institucional

### **Próximos Pasos Sugeridos**
1. **Recolección de Datos Adicionales:** Variables socioeconómicas
2. **Implementación de Modelos Avanzados:** Random Forest, XGBoost
3. **Validación Externa:** Pruebas con datos de otros períodos
4. **Desarrollo de Dashboard:** Interfaz para usuarios finales
5. **Expansión Geográfica:** Aplicación en otras provincias

---

## 📈 **Aspectos Destacables**

### **Innovación del Proyecto**
- **Primer modelo predictivo** para rendimiento educativo en Loja
- **Índice ICE único** que combina múltiples métricas
- **Metodología optimizada** para datasets grandes
- **Sistema comparativo** entre instituciones

### **Contribución al Campo**
- **Metodología replicable** para otras regiones
- **Framework de evaluación** institucional
- **Base de datos procesada** para futuras investigaciones
- **Herramienta de apoyo** para decisiones educativas

---

**🎉 El proyecto cumple exitosamente su objetivo de crear un sistema de predicción de rendimiento académico funcional y aplicable en el contexto educativo de Loja, estableciendo una base sólida para futuras mejoras y expansiones.** 