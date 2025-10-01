# Introducción

El cáncer de próstata es la neoplasia sólida más frecuente en varones y constituye una de las principales causas de morbilidad y mortalidad a nivel mundial [1]. A pesar de los avances en diagnóstico y tratamiento, la **heterogeneidad biológica y clínica** de esta enfermedad continúa siendo un desafío, particularmente al momento de estratificar a los pacientes según su riesgo de progresión y recurrencia. Tradicionalmente, la decisión terapéutica se ha basado en parámetros clínicos y patológicos como el antígeno prostático específico (PSA), el estadio tumoral y el **grado de Gleason**. Este último, representado en la base de datos como `grado_histologico`, es un sistema histológico que evalúa el patrón glandular tumoral y constituye uno de los factores pronósticos más robustos [2]. Sin embargo, incluso pacientes con características clínicas y patológicas similares pueden presentar desenlaces muy distintos, lo que resalta la necesidad de **nuevas herramientas de clasificación y estratificación de riesgo** más precisas.

En los últimos años, el advenimiento de las tecnologías de alto rendimiento ha permitido generar **datasets de expresión génica** a gran escala, obtenidos mediante microarrays o secuenciación de RNA. Una **matriz de expresión** contiene información cuantitativa sobre los niveles de expresión de miles de genes (columnas) en múltiples muestras biológicas o pacientes (filas). Cuando esta información molecular se asocia con **datos clínicos relevantes**, como el grado histológico o el desenlace clínico, se abre la posibilidad de identificar **biomarcadores pronósticos** y construir modelos que integren información molecular y clínica para guiar decisiones médicas [3,4].

En este contexto, un desenlace clínico clave es la **recaída bioquímica**, representada en la tabla como `relapse`. La recaída bioquímica se define como el aumento sostenido de PSA en sangre después de la prostatectomía radical, y constituye un indicador temprano de recurrencia tumoral y progresión de la enfermedad [5]. Identificar precozmente a los pacientes con mayor probabilidad de recaída es esencial para optimizar el seguimiento clínico y definir estrategias terapéuticas personalizadas.

Las herramientas de **inteligencia artificial (IA)** y **aprendizaje automático (machine learning, ML)** han demostrado un enorme potencial para abordar este tipo de problemas. Estas metodologías permiten manejar datasets de alta dimensionalidad —donde el número de variables (genes) supera ampliamente al número de muestras (pacientes)—, seleccionar subconjuntos de características relevantes (*feature selection*) y entrenar modelos predictivos capaces de generalizar a nuevos datos [6]. Aplicar ML a datos transcriptómicos y clínicos integrados no solo facilita la identificación de **firmas moleculares asociadas al riesgo de recaída**, sino que también potencia el desarrollo de herramientas de apoyo a la decisión clínica en escenarios reales.

Este hackatón propone que los participantes trabajen con un dataset compuesto por:  
- **Datos transcriptómicos** obtenidos por microarrays de expresión, organizados en una matriz de genes × pacientes.  
- **Datos clínicos**, incluyendo el `grado_histologico` (sistema de Gleason) y la variable binaria `relapse` (ocurrencia o no de recaída bioquímica en los 3 años posteriores a la prostatectomía).  

El objetivo será desarrollar modelos predictivos capaces de estratificar a los pacientes según su riesgo de recaída, explorando distintas metodologías de machine learning y evaluando su desempeño en un **conjunto de datos de prueba independiente** (*held-out data*).  

Este ejercicio busca no solo familiarizar a los estudiantes con el manejo de datos ómicos y clínicos en oncología, sino también resaltar el papel de la bioinformática y la IA en la medicina de precisión.

---

## Referencias

1. Sung H, et al. *Global Cancer Statistics 2020: GLOBOCAN Estimates of Incidence and Mortality Worldwide for 36 Cancers in 185 Countries*. **CA Cancer J Clin.** 2021;71(3):209–249.  
2. Epstein JI, et al. *The 2014 International Society of Urological Pathology (ISUP) Consensus Conference on Gleason Grading of Prostatic Carcinoma*. **Am J Surg Pathol.** 2016;40(2):244–252.  
3. Lapointe J, et al. *Gene expression profiling identifies clinically relevant subtypes of prostate cancer*. **Proc Natl Acad Sci USA.** 2004;101(3):811–816.  
4. Taylor BS, et al. *Integrative genomic profiling of human prostate cancer*. **Cancer Cell.** 2010;18(1):11–22.  
5. Cookson MS, et al. *Variation in the definition of biochemical recurrence in patients treated for localized prostate cancer: The American Urological Association Prostate Guidelines for Localized Prostate Cancer Update Panel report and recommendations for a standard in the reporting of surgical outcomes*. **J Urol.** 2007;177(2):540–545.  
6. Kourou K, et al. *Machine learning applications in cancer prognosis and prediction*. **Comput Struct Biotechnol J.** 2015;13:8–17.  

---

# Hackatón de bioinformática: predicción de recaída en cáncer de próstata

## datos
Se pueden descargar como `.csv` del siguiente link:
https://1drv.ms/x/c/d446169bfe3b3704/Eag4c4RqyTFDqSkTM3F2nn4BR3mRusJi8rmDt5LIUmWVWw?e=lkk5U3


## Contexto
El cáncer de próstata presenta una marcada heterogeneidad biológica y clínica, lo que dificulta la correcta estratificación de pacientes y la predicción de desenlaces posteriores al tratamiento. En este hackatón, los participantes trabajarán con un **dataset real** de pacientes de cancer de prostata sometidos a prostatectomía radical, sin tratamiento previo, en los que se cuenta con datos de:  

- **Expresión génica** obtenida por microarrays de expresión (matriz de genes (columnas) × pacientes (filas)).  
- **Datos clínicos** asociados, incluyendo:  
  - `grado_histologico`: sistema de **Gleason**, indicador histopatológico de agresividad tumoral.  
  - `relapse`: variable binaria que indica la **recaída bioquímica** (sí/no) en los 3 años posteriores a la cirugía.  
Tambien se destaca que el datast contiene informacion de **diferentes cohortes de pacientes** (columna `cohorte` pooleadas para aumentar el numero de observaciones. 
nota: la primer columna corresponde al identificador único del paciente 

El desafío consiste en **desarrollar modelos predictivos** capaces de anticipar el riesgo de recaída en pacientes, integrando datos transcriptómicos y clínicos mediante herramientas de **machine learning**.

### El grado histológico (Gleason score)

El grado histológico, registrado en la tabla como grado_histologico, hace referencia al Gleason score, que constituye el sistema de clasificación histopatológica estándar en cáncer de próstata. Este grado se determina evaluando, bajo el microscopio, el patrón de crecimiento glandular tumoral en muestras obtenidas por biopsia o prostatectomía. El sistema fue propuesto por Donald Gleason en los años 60 y, desde entonces, ha demostrado un alto valor pronóstico. El puntaje se obtiene sumando los dos patrones histológicos más frecuentes observados (primario y secundario), cada uno valorado en una escala de 1 a 5, donde los números más bajos reflejan un tejido más diferenciado y los más altos un patrón más indiferenciado y agresivo. En la práctica clínica, los puntajes suelen agruparse en rangos de riesgo:

- ≤6: bajo riesgo (tumores bien diferenciados).
- 7: riesgo intermedio (moderadamente diferenciados).
- 8–10: alto riesgo (pobremente diferenciados, de mayor agresividad).

El Gleason score es, por lo tanto, un parámetro clave en la estratificación pronóstica y en la toma de decisiones terapéuticas, ya que orienta tanto la indicación de prostatectomía, radioterapia o vigilancia activa, como la intensidad del seguimiento clínico posterior.

### La recaída bioquímica (relapse)

La recaída bioquímica, indicada en la tabla como relapse, se define como la elevación persistente del antígeno prostático específico (PSA) en sangre tras la prostatectomía radical. Dado que la próstata es extirpada quirúrgicamente, se espera que los niveles de PSA desciendan a valores indetectables en pocas semanas. Un aumento sostenido posterior constituye un marcador indirecto de la presencia de células tumorales residuales o recurrentes, aun en ausencia de hallazgos radiológicos o clínicos. Este evento tiene gran relevancia porque anticipa el riesgo de progresión clínica y metastásica, y se emplea como criterio de eficacia en numerosos estudios clínicos y de validación de biomarcadores.

## Estrategias de modelado en bioinformática y predicción clínica

Existen múltiples estrategias de análisis que los participantes podrán explorar en este hackatón. Entre las más utilizadas en bioinformática se destacan los métodos de reducción de dimensionalidad, como el principal component analysis (PCA), que permiten explorar patrones globales en los datos de expresión génica. También son frecuentes los enfoques de selección de variables, como el uso de limma para detectar genes diferencialmente expresados, o algoritmos de feature selection integrados en modelos de machine learning (ej. regularización LASSO, recursive feature elimination). Finalmente, se emplean algoritmos supervisados de predicción como regresión logística, máquinas de soporte vectorial (SVM), random forests y redes neuronales, cada uno con ventajas y limitaciones en términos de interpretabilidad, robustez y capacidad de generalización.

Otra estrategia común es la integración de datos moleculares con variables clínicas. Modelos híbridos que combinan la información transcriptómica con factores clásicos (como el grado histológico) suelen mejorar el desempeño predictivo. Este enfoque refleja la práctica clínica real, en la que las decisiones se basan en la integración de múltiples fuentes de información. Asimismo, los participantes pueden explorar la generación de firmas génicas compactas, que son subconjuntos de genes con alto poder predictivo y mayor potencial de validación en estudios independientes.

## Overfitting y generalización

Un concepto central en el entrenamiento de modelos predictivos es el sobreajuste (overfitting). Este fenómeno ocurre cuando un modelo se ajusta demasiado a los datos de entrenamiento, capturando ruido o particularidades específicas de la muestra en lugar de patrones generales. Como consecuencia, el modelo muestra un desempeño muy alto en el conjunto de entrenamiento, pero pobre en datos nuevos o independientes. La capacidad opuesta, llamada generalización, es la habilidad del modelo para mantener un buen desempeño en datos no vistos previamente. Para mitigar el sobreajuste, se emplean estrategias como la validación cruzada (k-fold cross-validation), el uso de conjuntos independientes de prueba (held-out datasets), la regularización de modelos (ej. LASSO, ridge regression) y el control del número de variables incluidas en el análisis.

## Número de variables y aplicabilidad clínica

Un aspecto fundamental a considerar es la simplicidad y parsimonia del modelo. Si bien los datos transcriptómicos incluyen miles de genes, en la práctica clínica resulta inviable implementar modelos que requieran medir una gran cantidad de marcadores. Por ello, se deben priorizar modelos que utilicen un número reducido de features, siempre que mantengan un buen desempeño predictivo. Modelos basados en un conjunto limitado de genes tienen mayor probabilidad de ser trasladados a la práctica, por ejemplo mediante ensayos clínicos o paneles de PCR dirigidos, lo cual los hace más útiles como herramientas de apoyo a la decisión médica.

## Métricas sugeridas para evaluar modelos
estas son algunas de las metricas básicas que se pueden utilizar, pero los aprticipantes podrán proponer otra

- **AUC-ROC (Área bajo la curva ROC)**: mide la capacidad global de discriminación.  
- **Sensibilidad y especificidad**: identifican la proporción de verdaderos positivos y verdaderos negativos.  
- **Precisión y recall**: útiles en escenarios de clases desbalanceadas.  

## Presentación de modelos y validación final

Al finalizar el hackatón, cada grupo presentará el o los modelos predictivos desarrollados durante la jornada, describiendo brevemente la estrategia utilizada, las variables seleccionadas y los resultados obtenidos en el proceso de validación interna. Una vez completada esta instancia, se entregará a los participantes un conjunto de datos independiente y oculto (held-out dataset), que no estuvo disponible durante el entrenamiento. Este paso permitirá evaluar de manera objetiva la capacidad de generalización de los modelos, comparando su desempeño en datos nuevos y reproduciendo el desafío real de trasladar una herramienta bioinformática a un escenario clínico.

## Al final del hackatón, cada equipo habrá:  

- Diseñado un **pipeline de análisis bioinformático** aplicado a datos ómicos reales.  
- Experimentado con técnicas de **machine learning** para predicción clínica.  
- Discutido cómo este tipo de herramientas pueden **aportar a la medicina de precisión** en cáncer de próstata.  
