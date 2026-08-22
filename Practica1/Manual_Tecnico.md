<div align="center">

## UNIVERSIDAD SAN CARLOS DE GUATEMALA
## FACULTAD DE INGENIERÍA
## INGENIERÍA EN CIENCIAS Y SISTEMAS


#### Redes de Computadoras 1
#### Segundo Semestre 2026

<br><br><br>
<br><br><br>

# Práctica 1
### QuetzalDev S.A.

<br><br><br>
<br><br><br>

</div>

**Estudiante:** Manuel Alejandro López Canel
**Carnet:** 202302035

**Auxiliar:** César Fernando Sazo Quisquinay

<br>

<div align="center">

**Guatemala, agosto de 2026**

</div>

---

<div align="justify">

## 1. Inventario de Equipos

A continuación, se detalla el equipo activo y pasivo seleccionado para la red:

| Cantidad | Equipo | Descripción |
| :--- | :--- | :--- |
| 1 | Switch Principal | 48 puertos SFP/RJ45 (Cisco Catalyst serie 9300 o equivalente). |
| 8 | Switch de Acceso | 16/24 puertos Gigabit Ethernet, PoE+ (para cada departamento). |
| 1 | Patch Panel Principal | 48 puertos, Categoría 6, montaje en rack de 19". |
| 8 | Patch Panel Secundario | 24 puertos, Categoría 6, montaje en pared. |
| 1 | Rack de Piso | 42U, puertas perforadas, organizadores de cables verticales y horizontales. |
| 8 | Gabinete de Pared | 9U, con puerta de vidrio y ventilación activa. |
| 48 | Tomas de Red | Combinación de placas unitarias, dobles y triples (dependiendo de la distribución por área). |
| 4 | Bobinas de Cable UTP | Categoría 6, LSZH, 305 metros cada una (color azul). |
| 1 | Bobina Fibra Óptica | Multimodo OM4, 4 hilos, uso interior (color aqua), para cableado troncal. |
| 2 | UPS | 3kVA para el Data Center y MDF. UPS menores de 1kVA para switches de distribución. |

## 2. Justificación de la Ubicación del Cuarto de Telecomunicaciones (MDF)

El MDF se ubicó en el **Data Center**. 
**Justificación:** Cumple con los requerimientos de aislamiento acústico, térmico y de seguridad física indispensables para equipos críticos de red y servidores. Al ubicarse en el extremo derecho del plano (que tiene una longitud total de 28 metros), la distancia al punto de red más lejano en el Departamento de Recepción ronda los 30-35 metros considerando canalización aérea y caídas. Esta métrica garantiza que ninguna conexión horizontal supere el límite normativo de 90 metros del estándar TIA/EIA-568.

## 3. Topología Física

| Segmento | Tipo de Topología | Justificación |
| :--- | :--- | :--- |
| **Por Departamento** | Estrella | Alta tolerancia a fallos: la desconexión de un host no afecta al resto. Permite escalar fácilmente añadiendo nodos al switch local. Centraliza el tráfico de hosts en un solo equipo activo por área. |
| **Edificio** | Árbol | El Switch Principal en el MDF actúa como nodo raíz, conectando mediante enlaces troncales a los switches de cada departamento. Aísla el dominio de colisiones y broadcast de cada área, optimizando el rendimiento general. |

## 4. Medios de Transmisión

| Segmento | Tipo de Medio y Categoría | Justificación |
| :--- | :--- | :--- |
| **Troncal (MDF - Deptos)** | Fibra Óptica Multimodo (OM4) | Garantiza enlaces de alto rendimiento (10 Gbps o más) para manejar el tráfico agregado de múltiples computadoras y servidores hacia el Core, evitando cuellos de botella. Inmune a interferencias electromagnéticas. |
| **Horizontal (Switch - Hosts)** | UTP Categoría 6 | Soporta anchos de banda de 1 Gbps (hasta 10 Gbps en distancias cortas). Costo-efectivo para conectar PCs, laptops y servidores a nivel de escritorio dentro del margen de los 90 metros permitidos. |

## 5. Distancias de Cableado Horizontal y Cálculo de Bobinas

Todas las distancias son estimaciones proyectadas sobre el plano de 28x21m, asumiendo recorridos ortogonales y caídas de 3 metros.

| Departamento | Dispositivos | Distancia Promedio (m) | Total de Cable Estimado (m) |
| :--- | :--- | :--- | :--- |
| Recepción | 2 | 35 | 70 |
| Recursos Humanos | 5 | 22 | 110 |
| Legal | 3 | 18 | 54 |
| Capacitación | 12 | 12 | 144 |
| Diseño e Innovación | 8 | 25 | 200 |
| Dirección General | 5 | 16 | 80 |
| Backend | 7 | 8 | 56 |
| Data Center | 6 | 4 | 24 |
| **TOTAL** | **48 hosts** | | **~738 metros + 20% holgura = 885 metros** |

**Cálculo de Bobinas:**
* Requerimiento total estimado: 885 metros.
* Longitud estándar de bobina UTP: 305 metros.
* 885 m / 305 m = 2.9 bobinas.
* **Cantidad requerida:** Se estipula la compra de **4 bobinas completas** para tener margen de error y mantenimiento futuro.

## 6. Equipo Activo y Dimensionamiento

* **Dimensionamiento del Patch Panel y Switch Principal:** La red exige soportar un total de 48 hosts distribuidos en el edificio. Para el MDF, se seleccionó un Switch Core de 48 puertos y un Patch Panel central de 48 puertos. Aunque el cableado horizontal se gestiona en los switches de cada departamento, esta decisión garantiza que la capacidad instalada central tiene equivalencia directa en número de puertos respecto al volumen total de dispositivos de la empresa, asegurando redundancia, capacidad de enrutamiento y puertos suficientes para los servidores locales del Data Center y enlaces troncales.
* **Switches de Distribución:** Equipos de 16/24 puertos en cada departamento para manejar el tráfico local y proveer puertos disponibles para el crecimiento interanual proyectado.

## 7. Canalización y Rack

* **Canalización Troncal y Horizontal Superior:** Escalerilla metálica abierta instalada en el cielo falso. Garantiza ventilación adecuada para la fibra y el UTP, facilidad para añadir nuevos cables y cumplimiento de radio de curvatura.
* **Canalización Horizontal Inferior (Bajadas):** Tubería conduit metálica o canaleta de PVC de alto impacto para proteger el cableado UTP desde el cielo falso hasta las placas de pared.
* **Rack/Gabinete:** Para el MDF en el Data Center se propuso un **Rack de Piso cerrado de 42U**. Se justifica por la necesidad de centralizar switches principales, UPS de gran tamaño, patch panels de alta densidad, fibra óptica y los 3 servidores principales de la empresa. Para los departamentos, gabinetes de pared de 9U por eficiencia de espacio.

## 8. Estimación de Consumo Eléctrico y UPS

* **Estimación:** Un switch de 48 puertos consume aproximadamente entre 50W y 100W (sin PoE masivo). Los 8 switches de departamento sumarán alrededor de 400W. Los servidores de rack consumen aproximadamente entre 300W a 500W cada uno (6 servidores = 3000W). Total estimado de equipo crítico = 3500W.
* **Respaldo:** Se propone una UPS Central de **5kVA a 6kVA** para el Rack del Data Center (respaldando Core y servidores), y micro-UPS de 750VA-1kVA para los gabinetes de pared de los switches departamentales, garantizando estabilidad ante fluctuaciones y autonomía temporal.

## 9. Disposición de Pines y Tipo de Conexión (T568A/T568B)

Dado que la red conecta equipos heterogéneos modernos, la tarjeta de red (NIC) de los hosts negocia automáticamente mediante Auto-MDIX. Sin embargo, por normativas de estructuración, toda la instalación horizontal se basará en la norma **T568B**.

| Enlace | Medio | Tipo de Cable | Justificación |
| :--- | :--- | :--- | :--- |
| **PC/Laptop a Toma (Switch)** | UTP | Straight-through | Conexión de dispositivos de distinta capa OSI. |
| **Switch Depto a Switch Core** | Fibra Óptica | Patch cord dúplex | La interconexión troncal óptica requiere un par TX/RX cruzado intrínsecamente en el patch cord. (Si fuera UTP, requeriría un cable crossover en hardware antiguo sin Auto-MDIX al conectar equipos de misma capa). |

**Documentación de Disposición de Pines (T568B - Straight-Through):**
Ambos extremos del cable (A y B) utilizan el mismo orden:
1. Blanco-Naranja
2. Naranja
3. Blanco-Verde
4. Azul
5. Blanco-Azul
6. Verde
7. Blanco-Marrón
8. Marrón

**Documentación de Disposición de Pines (Crossover - Extremo 1 T568A / Extremo 2 T568B):**
Extremo T568A:
1. Blanco-Verde | 2. Verde | 3. Blanco-Naranja | 4. Azul | 5. Blanco-Azul | 6. Naranja | 7. Blanco-Marrón | 8. Marrón

## 10. Etiquetado de Cables y Normativa TIA/EIA-606

**Formato utilizado en esta práctica:**
* Cableado Horizontal: `[Área]-[Número de Punto de Red]`
* Cableado Troncal: `MDF-[Área]`

**Comparación con Estándar TIA/EIA-606:**

| Aspecto | Práctica Actual | Estándar TIA/EIA-606 Completo |
| :--- | :--- | :--- |
| **Complejidad del Identificador** | Usa nombres descriptivos simples. | Exige códigos alfanuméricos únicos que denotan piso, cuarto, rack, panel y puerto (Ej. `1A-B01-05`). |
| **Codificación por Colores** | No especificada. | Asigna colores estrictos por subsistema (Ej. Naranja = Demarcación, Azul = Horizontal). |

**Justificación de su uso en entorno real:**
En un Data Center o entorno corporativo real, se exige aplicar el estándar 606 completo porque la infraestructura escalará a miles de puertos. Los nombres descriptivos de la práctica ("Diseño") quedan obsoletos si el departamento se muda de oficina. El estándar 606 utiliza identificadores geográficos inmutables (Piso 1, Cuarto A, Rack 2), lo que reduce drásticamente el tiempo de resolución de fallas independientemente de qué departamento ocupe el espacio físico.

## 11. Flujo de Conexión End-to-End

El flujo para un equipo es el siguiente:
1. El dispositivo se conecta vía patch cord UTP Cat 6 hacia la toma de red en la pared/escritorio.
2. Desde la parte posterior de la toma, el cableado horizontal UTP Cat 6 viaja por tubería conduit a la escalerilla en cielo falso hasta el Patch Panel en el Gabinete de Pared del departamento.
3. Mediante un patch cord corto, la conexión pasa del Patch Panel al Switch de Acceso del departamento.
4. El Switch de Acceso empaqueta la trama y la envía a través de su transceptor (SFP) por el cableado troncal de Fibra Óptica.
5. La luz viaja por la escalerilla principal hasta el ODF en el Rack del Data Center.
6. Desde el ODF, un patch cord de fibra conecta al Switch Core.
7. El Switch Core enruta el tráfico hacia su destino final.

## 12. Presupuesto Estimado

| Ítem | Cantidad | Precio Unitario Estimado (USD) | Total Estimado (USD) |
| :--- | :--- | :--- | :--- |
| Nexxt Bobina de Cable Cat.6 F/UTP con Revestimiento para Exteriores - 4 Pares, 305m | 1 | Q2,934.00 | Q2,934.00 |
| Cisco Catalyst 1200-48P-4G Smart Switch, 48 Port GE, PoE, 4x1GE SFP, Limited Lifetime Protection (C1200-48P-4G) | 1 | Q11,714.00 | Q11,714.00 |
| Switch Intellinet 560559 De 24 Puertos Gigabit Ethernet Administrable PoE | 8 | Q2,624.00 | Q20,992.00 |
| EPA171 Gabinete de Piso 600X800X42U | 1 | Q12,300.00 | Q12,300.00 |
| Gabinete De Pared, 9U 19 Pulgadas, Color Negro Epoxy | 8 | Q1,589.00 | Q12,712.00 |
| UPS APC Smart RT 5000VA 208V 4 Salidas | 1 | Q17,745.00 | Q17,745.00 |
| Placas, Jacks, Patch Cords | 48 (Lotes) | Q95.00 | Q4,560.00 |
| Fibra Óptica y ODFs | 1 (Kit) | Q1,364.65 | Q1,364.65 |
| **Presupuesto Total** | | | **Q84,321.65** |

Links de referencia:

Nexxt Bobina de Cable Cat.6 F/UTP con Revestimiento para Exteriores - 4 Pares, 305m: https://www.kemik.gt/nexxt-bobina-de-cable-cat_6-f_utp-con-revestimiento-para-exteriores-4-pares-305m

Cisco Catalyst 1200-48P-4G Smart Switch, 48 Port GE, PoE, 4x1GE SFP, Limited Lifetime Protection (C1200-48P-4G): https://www.pacifiko.com/compras-en-linea/cisco-catalyst-1200-48p-4g-smart-switch-48-port-ge-poe-4x1ge-sfp-limited-lifetime-protection-c1200-48p-4g-nombre-de-estilo-cisco-catalyst-1200-switch-48-port-ge-poe-375w-4-x-ge-uplinks&pid=MTY3YzQ3Nj

Switch Intellinet 560559 De 24 Puertos Gigabit Ethernet Administrable PoE: https://www.intelaf.com/precios_stock_detallado/sw-24-ic-apgb59

EPA171 Gabinete de Piso 600X800X42U: https://camarasdeseguridad.com.gt/epa171-gabinete-de-piso-600x800x42u.html

UPS APC Smart RT 5000VA 208V 4 Salidas: https://www.pacifiko.com/compras-en-linea/ups-apc-smart-rt-5000va-208v-4-salidas&pid=NGU1YjZmNz

Placas, Jacks, Patch Cords:
https://oxdea.gt/product/patch-cord-cat6-de-30-cm-nexxt-pcgpcc6cm01gr/
https://oxdea.gt/product/cable-de-red-cat6e-7-5-mts/
https://oxdea.gt/product/placa-de-montaje-de-6-puertos-color-blanca-sprywire-sw-fp06a/
https://www.kemik.gt/jack-rj45-de-8-contactos-a-90-cat-6-tipo-keystone-blanco

Fibra Óptica y ODFs
https://oxdea.gt/product/cable-de-fibra-optica-gjxh-de-alta-calidad-para-interiores-de-2-nucleos-sw-gjxh-ftc-in2b/
https://www.conexionderedes.com/tienda/7dc3f8b2-d016-41f3-aa68-0a645a889167
https://chipcom.com.gt/producto/LP-ODF-8024-LINKEDPRO-BY-EPCOM-196654
