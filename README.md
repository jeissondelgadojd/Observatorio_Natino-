# 🇨🇴 Observatorio de Actividad Económica y Social por Departamentos

Aplicación web interactiva construida con **Gradio** que permite consultar, filtrar y visualizar indicadores oficiales de Colombia a nivel departamental.

## Fuentes de datos (datos.gov.co / SODA)

| Indicador | Dataset | Descripción |
|-----------|---------|-------------|
| **PIB** | [kgyi-qc7j](https://www.datos.gov.co/resource/kgyi-qc7j.json) | PIB total por departamento (precios constantes 2015, miles de millones) |
| **Homicidios** | [m8fd-ahd9](https://www.datos.gov.co/resource/m8fd-ahd9.json) | Víctimas de homicidio (MinDefensa) |
| **Recursos DNP** | [wc86-9j4a](https://www.datos.gov.co/resource/wc86-9j4a.json) | Recursos públicos del Departamento Nacional de Planeación (COP) |

> Los datos se descargan en tiempo real desde la API pública de datos.gov.co. **No se inventan ni se modifican valores.**

## Características

- Normalización robusta de nombres de departamentos (sin tildes, mayúsculas/minúsculas, variantes comunes).
- Filtros por departamento(s), indicador y rango de años.
- Estadísticas descriptivas (media, mediana, desviación estándar, min, max, conteo).
- Gráfico de tendencias (líneas con marcadores).
- Barras horizontales comparativas (Top 15 departamentos).
- Tabla de datos filtrados (hasta 400 registros).

## Requisitos

- Python 3.9+
- Dependencias listadas en `requirements.txt`

## Instalación

```bash
# Crear entorno virtual (recomendado)
python -m venv venv
source venv/bin/activate          # Linux / macOS
# o
venv\Scripts\activate             # Windows

# Instalar dependencias
pip install -r requirements.txt
```

## Uso

```bash
python observatorio_nariñoipynb.py
```

La aplicación se abrirá en el navegador (por defecto `http://127.0.0.1:7860`).  
Si se lanza con `share=True` (como en el script original), Gradio generará un enlace público temporal.

### Interfaz

1. Selecciona uno o varios **departamentos** (o “Todos”).
2. Elige el **indicador** (PIB, Homicidios, Recursos DNP o Todos).
3. Ajusta el **rango de años** y el año para el gráfico de barras.
4. Haz clic en **Actualizar análisis**.

## Estructura del código

| Sección | Descripción |
|---------|-------------|
| Normalización | `quitar_tildes()` + diccionario canónico de departamentos |
| Carga de datos | `cargar_pib()`, `cargar_homicidios()`, `cargar_dnp()` → `construir_maestro()` |
| Análisis | `filtrar()`, `stats()`, `tendencia()`, `barras()` |
| Interfaz Gradio | Bloques con dropdowns, sliders, pestañas y botón de actualización |

## Notas importantes

- La primera carga puede tardar 30–90 segundos porque se consultan hasta ~150 000 registros.
- Si alguna fuente falla (timeout, cambio de esquema, etc.), el resto de indicadores sigue funcionando.
- Los nombres de departamentos se unifican (ej.: “Narino” → “Nariño”, “Bogota” → “Bogotá D.C.”).

## Licencia y atribución

Datos oficiales de **datos.gov.co**, Ministerio de Defensa y Departamento Nacional de Planeación.  
Esta aplicación es de uso libre para análisis y visualización.

---

*Generado a partir del notebook Colab original.*
