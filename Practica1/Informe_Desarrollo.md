# Informe de Desarrollo: Diseño de Infraestructura Física de Red
**Proyecto:** QuetzalDev S.A.
**Curso:** Redes de Computadoras 1

<div align="justify">

## 1. Proceso de Diseño
El diseño de la infraestructura física inició con el análisis del plano arquitectónico proporcionado para ubicar estratégicamente el Cuarto de Telecomunicaciones (MDF). Se determinó que el "Data Center" existente era el área óptima debido a que su ubicación cumple con las restricciones de distancia del estándar TIA/EIA-568, ya que el tramo más largo hacia el Departamento de Recepción no supera los 35 metros lineales. 

Posteriormente, se distribuyó el inventario exacto de dispositivos finales exigido: 30 computadoras de escritorio, 12 laptops y 6 servidores. Se asignó un switch de acceso a cada departamento y se estructuró un modelo jerárquico mediante el uso de patch panels departamentales y un patch panel principal en el rack del Data Center, garantizando el flujo normativo de la Capa 1 del Modelo OSI.

## 2. Criterios de Selección de Topologías
La arquitectura general de la red se definió bajo un modelo de **Árbol**.
*   **Topología por Departamento:** Se implementó una topología en estrella en cada área, donde los dispositivos finales convergen en un switch de acceso local. Esto garantiza alta tolerancia a fallos, impidiendo que la desconexión o falla de una terminal afecte a los demás usuarios del mismo departamento.
*   **Topología Troncal:** Los switches departamentales convergen hacia el Switch Core ubicado en el MDF. Este diseño centraliza la gestión del tráfico, aísla los dominios de colisión por área y permite escalar la red de forma modular.

## 3. Criterios para Selección de Medios de Transmisión
Se evitó la mezcla de categorías para estandarizar la infraestructura y asegurar compatibilidad de componentes pasivos (jacks, conectores, paneles).
*   **Cableado Horizontal (UTP Categoría 6):** Seleccionado para la conexión entre los switches departamentales y los dispositivos finales. Soporta velocidades de 1 Gbps, siendo el estándar actual para entornos corporativos con requerimientos de alta transferencia de datos como el área de Backend y Diseño e Innovación. 
*   **Cableado Troncal (Fibra Óptica Multimodo OM4):** Implementado para los enlaces entre el MDF y los switches de cada departamento. Su uso se justifica por la necesidad de soportar el ancho de banda agregado de múltiples hosts, garantizando enlaces de 10 Gbps sin atenuación por interferencias electromagnéticas ni limitaciones de ancho de banda.

## 4. Criterios para Selección de Equipo Activo
*   **Switch Core (MDF):** Se dimensionó un switch principal de 48 puertos (con interfaces SFP para la fibra) para igualar la capacidad del patch panel principal de 48 puertos, asegurando redundancia y capacidad de expansión.
*   **Switches de Distribución:** Equipos de 16 a 24 puertos en los departamentos para concentrar las conexiones locales, con soporte PoE en caso de futura integración de telefonía IP o puntos de acceso.
*   **Respaldo de Energía:** Se estipuló un UPS central de 5kVA para proteger los servidores y el equipo core en el MDF, complementado con unidades de 1kVA en los gabinetes departamentales para mantener la estabilidad del enlace.

## 5. Retos de Planificación Física
El principal reto de planificación fue definir la ruta física del cableado respetando las normativas de construcción corporativa. Inicialmente se consideró el paso a través de áreas de tránsito humano, lo cual viola los estándares de cableado estructurado. La solución implementada consistió en trazar el recorrido horizontal y troncal a través de una escalerilla metálica abierta alojada en el cielo falso de la Zona de Circulación General. A partir de allí, el cable UTP desciende hacia las tomas de red mediante tubería conduit metálica interna, garantizando protección física, estética y un correcto radio de curvatura para los cables.
