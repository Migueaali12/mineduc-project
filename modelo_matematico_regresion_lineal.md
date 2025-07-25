# 🔬 Modelo Matemático de Regresión Lineal Múltiple

## LinearRegression() de Scikit-Learn

Basado en el análisis del código donde se implementa:
```python
modelo_final = LinearRegression()
modelo_final.fit(X_train_scaled, y_train)
```

---

## 📐 Ecuación Fundamental

El modelo implementa la **regresión lineal múltiple** con la siguiente ecuación:

```math
ŷ = β₀ + β₁x₁ + β₂x₂ + ... + βₚxₚ
```

**Donde:**
- `ŷ` = Variable predicha (ICE - Índice de Calidad Educativa)
- `β₀` = Intercepto (constante)
- `β₁, β₂, ..., βₚ` = Coeficientes de regresión
- `x₁, x₂, ..., xₚ` = Variables predictoras (características institucionales)

---

## 🎯 Formulación Matricial

En notación matricial:

```math
𝐲 = 𝐗𝛃 + 𝛆
```

**Componentes:**
- `𝐲` = Vector de valores objetivo (n × 1)
- `𝐗` = Matriz de características (n × p+1, incluye columna de 1s para intercepto)
- `𝛃` = Vector de coeficientes ((p+1) × 1)
- `𝛆` = Vector de errores (n × 1)

---

## ⚡ Método de Optimización: Mínimos Cuadrados Ordinarios (OLS)

### Función de Costo

El algoritmo minimiza la **función de pérdida cuadrática**:

```math
J(𝛃) = (1/2m) Σᵢ₌₁ᵐ (h_𝛃(𝐱⁽ⁱ⁾) - y⁽ⁱ⁾)²
```

En forma matricial:
```math
J(𝛃) = (1/2m) ||𝐗𝛃 - 𝐲||²
```

### Solución Analítica - Ecuación Normal

Los coeficientes se calculan usando:

```math
𝛃 = (𝐗ᵀ𝐗)⁻¹𝐗ᵀ𝐲
```

Esta es la **solución exacta** que minimiza la suma de errores cuadráticos.

---

## 🔮 Predicción para Nuevas Observaciones

Para realizar predicciones:

```math
ŷ_nuevo = 𝐱ᵀ_nuevo 𝛃
```

---

## 📊 Aplicación en tu Contexto Específico

Con las **15 variables predictoras** identificadas en el modelo:

```math
ICE = β₀ + β₁·Año_encoded + β₂·Canton_encoded + β₃·Sostenimiento_encoded 
    + β₄·Tipo_Educacion_encoded + β₅·Regimen_encoded + β₆·Jurisdiccion_encoded
    + β₇·Area_encoded + β₈·Modalidad_encoded + β₉·Jornada_encoded
    + β₁₀·Total_Estudiantes + β₁₁·Total_Docentes + β₁₂·Estudiantes_Femenino
    + β₁₃·Docentes_Femenino + β₁₄·Docentes_Masculino + β₁₅·Estudiantes_Masculino
```

---

## ✅ Suposiciones del Modelo

1. **🔗 Linealidad**: Relación lineal entre predictoras y variable objetivo
2. **🔄 Independencia**: Observaciones independientes entre sí
3. **📏 Homocedasticidad**: Varianza constante de los errores
4. **📈 Normalidad**: Errores siguen distribución normal
5. **❌ No multicolinealidad**: Variables predictoras no perfectamente correlacionadas

---

## 📈 Métricas de Evaluación

### R² (Coeficiente de Determinación)
```math
R² = 1 - (SS_res/SS_tot) = 1 - (Σᵢ(yᵢ - ŷᵢ)²)/(Σᵢ(yᵢ - ȳ)²)
```

### MAE (Error Absoluto Medio)
```math
MAE = (1/n) Σᵢ₌₁ⁿ |yᵢ - ŷᵢ|
```

### RMSE (Raíz del Error Cuadrático Medio)
```math
RMSE = √[(1/n) Σᵢ₌₁ⁿ (yᵢ - ŷᵢ)²]
```

---

## 🎯 Resultados en tu Modelo

| Métrica | Valor | Interpretación |
|---------|-------|----------------|
| **R²** | 0.100 | Explica el 10% de la variabilidad en ICE |
| **MAE** | 4.87 | Error promedio de ±4.9 puntos de ICE |
| **RMSE** | 7.84 | Desviación estándar del error |

---

## 🔧 Proceso de Implementación

### 1. Preprocesamiento
```python
# Normalización de variables numéricas
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train_numeric)

# Codificación de variables categóricas
label_encoders = {}
for col in categorical_cols:
    le = LabelEncoder()
    X_encoded = le.fit_transform(X[col])
```

### 2. Entrenamiento
```python
modelo_final = LinearRegression()
modelo_final.fit(X_train_scaled, y_train)
```

### 3. Predicción
```python
y_pred = modelo_final.predict(X_test_scaled)
```

---

## 💡 Características del Algoritmo

- **Tipo**: Supervisado, Regresión
- **Complejidad**: O(p³) para inversión de matriz + O(np²) para multiplicación
- **Ventajas**: 
  - Solución exacta (no iterativa)
  - Interpretable
  - Rápido para datasets medianos
- **Limitaciones**:
  - Asume relaciones lineales
  - Sensible a outliers
  - Problemas con multicolinealidad alta

---

## 🧮 Detalles Computacionales

Scikit-learn utiliza optimizaciones como:
- **Descomposición SVD** para mayor estabilidad numérica
- **Normalización automática** para evitar problemas de escala
- **Manejo robusto** de matrices singulares

El algoritmo es determinístico y siempre converge a la misma solución óptima global. 