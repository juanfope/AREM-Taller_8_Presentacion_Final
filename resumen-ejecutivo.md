#RESUMEN EJECUTIVO: TRANSFORMACIÓN ARQUITECTÓNICA DE THEGEEKHUB
1. Introducción y Planteamiento del Problema
THEGEEKHUB es un emprendimiento minorista dedicado a la comercialización de artículos coleccionables de series, películas y videojuegos. Desde su creación a finales de 2023, el negocio ha operado bajo un modelo artesanal y 100% virtual, canalizando sus interacciones y captación de clientes a través de redes sociales (Instagram, Facebook) y Mercado Libre.

A pesar de contar con una tracción comercial inicial, el negocio enfrenta barreras críticas que limitan su capacidad para alcanzar las ventas esperadas y escalar de forma segura. El diagnóstico técnico de su arquitectura actual (AS-IS) reveló las siguientes problemáticas estructurales:
- Dependencia de Procesos Manuales y Hojas de Cálculo: Toda la información contable, de inventario y de clientes se registra manualmente en archivos de Excel fragmentados por año. Esto genera silos de información y una alta probabilidad de errores humanos por doble digitación.
- Inconsistencia Crítica de Inventario: Al no existir una integración entre los canales de venta (redes sociales y Mercado Libre), el stock real se desfasa constantemente. Esto produce escenarios de sobreventa o pérdidas de transacciones por no contar con un SKU estandarizado para las referencias de los productos.
- Vulnerabilidad de Datos y Falta de Trazabilidad: Los datos de contacto y envío de los compradores se almacenan de manera efímera y sin cifrar, eliminándose tras la entrega. Esto viola regulaciones de protección de datos personales y destruye el histórico necesario para estrategias de retención.
- Ausencia de Auditoría Financiera: Los flujos de dinero se validan visualmente mediante capturas de pantalla de pasarelas como Nequi y MercadoPago, y las transferencias internas entre estas cuentas no quedan registradas, generando un riesgo latente de fraude o descuadre de caja.

2. Solución Propuesta
Para solucionar de raíz estos problemas y habilitar el crecimiento hacia un local físico o un e-commerce formal, se diseñó una solución integral que transfiere el negocio hacia una arquitectura orientada a eventos y microservicios basada en servicios en la nube (AWS), soportada por un modelo relacional estricto de 6 entidades: Ventas, Referencia, Comprador, Transacción, Fuente y CambioFuente. La infraestructura propuesta (TO-BE) se compone de:
- API Gateway / Controlador: Actúa como el único punto de entrada unificado que centraliza, autentica y valida las peticiones de pedidos provenientes de Instagram, Facebook, Mercado Libre y un Dashboard administrativo para socios.
- Cola de Eventos de Venta (Messaging Queue - AWS SQS): Funciona como un amortiguador asíncrono. Absorbe picos masivos de tráfico en temporadas altas sin pérdida de datos ni caídas del sistema, distribuyendo las órdenes hacia los servicios internos.
- Estrategia de Persistencia con bases de datos: Base de Datos Relacional Central (SQL - AWS RDS) e Historial NoSQL (AWS DynamoDB/MongoDB).

3. Propuesta de Valor y Ventaja Competitiva
La propuesta de valor de esta transformación radica en profesionalizar la operación interna de THEGEEKHUB sin alterar la agilidad de sus canales comerciales front-end. Contando con claros diferenciadores en la forma de desacoplamiento absoluto del negocio, donde al separar el "acto comercial" (Venta) del "movimiento físico de dinero" (Transacción) y de los movimientos internos (CambioFuente), el sistema provee una claridad financiera absoluta, permitiendo identificar discrepancias en Nequi o MercadoPago al instante.

Otro de los factores que aportan valor a nuestra solucion, radica en el control de SKU, el modelo introduce un motor de inventario único que bloquea el stock en todas las plataformas simultáneamente cuando se concreta una venta, eliminando la mala experiencia de usuario por cancelaciones de pedidos.

Finalmente optamos por laimplementación de seguridad por capas, el uso del Gateway oculta las credenciales de las APIs financieras y centraliza la autenticación (AWS IAM). Los datos de los clientes se resguardan bajo cifrado automático, permitiendo el cumplimiento normativo.

4. Mercado Objetivo
El mercado objetivo de THEGEEKHUB se compone de un nicho de consumo en Colombia:
- Perfil del Cliente Ideal: Jóvenes adultos, profesionales de 18 a 35 años, entusiastas de la cultura pop, coleccionistas de figuras de acción, figuras Funko Pop, y mercancía exclusiva de anime, series de streaming y videojuegos de última generación.
- Dinámica del Nicho: Este cliente busca inmediatez en la atención (chats rápidos) pero exige una precisión absoluta en el estado de sus pedidos y envíos. Al formalizar la base de datos de la entidad Comprador, THEGEEKHUB puede segmentar este nicho para ofrecer preventas exclusivas basadas en sus hábitos históricos de compra.

5. Modelo de Negocio y Finanzas
THEGEEKHUB genera ingresos de forma directa a través de la venta minorista de artículos coleccionables con márgenes de valor variables. Al realizar la migración al modelo cloud propuesto para los registros y seguimiento de ventas y clientes, la estructura de costos se transforma de un gasto de capital fijo (servidores locales) a un modelo de costo operativo elástico basado en el consumo (Pay-as-you-go). La inversión inicial y costos fijos estimados son mínimos gracias a la capa gratuita de AWS en etapas tempranas. Los costos de hosting en la nube estimados en menos de $40 USD mensuales, consumidos principalmente por la base de datos relacional (RDS micro) y el API Gateway. Asi mismo, el sistema está dimensionado para soportar un incremento del 400% en transacciones concurrentes sin necesidad de rediseño técnico, requiriendo únicamente un escalado vertical automatizado de las bases de datos conforme aumente el volumen de facturación.

6. Conclusión
La transición arquitectónica de THEGEEKHUB demuestra que el orden tecnológico y el éxito financiero van de la mano. Al reemplazar las hojas de cálculo tradicionales por un ecosistema robusto de microservicios distribuidos y persistencia políglota, la empresa mitiga los 12 riesgos críticos de seguridad, consistencia y disponibilidad operativa evaluados por la metodología de Arquitectura Empresarial. El modelo propuesto es técnica y financieramente viable, preparando al emprendimiento para expandirse con éxito hacia el comercio electrónico masivo y tiendas físicas.
