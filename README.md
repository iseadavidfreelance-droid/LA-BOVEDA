<div align="center">

<img width="100%" alt="La Bóveda Banner" src="la-boveda-v-0-1.jpg?v=2" />


# LA BÓVEDA | Tactical Asset Command & Control

*Sistema Avanzado de Gestión de Inventario Digital y Optimización de Activos de Alto Rendimiento.*

[![React](https://img.shields.io/badge/React-18.3-blue?style=for-the-badge&logo=react)](https://reactjs.org/)
[![Supabase](https://img.shields.io/badge/Supabase-DB-3ECF8E?style=for-the-badge&logo=supabase)](https://supabase.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4-38B2AC?style=for-the-badge&logo=tailwind-css)](https://tailwindcss.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?style=for-the-badge&logo=typescript)](https://www.typescriptlang.org/)

</div>

---

## 🚀 Visión General
**LA BÓVEDA** no es un CRUD tradicional, es una aplicación web de control táctico que se presenta como un ecosistema **Serverless ELT** (Extract, Load, Transform) diseñado bajo la filosofía **"Data-Driven Governance"**. Su motor transforma el tráfico orgánico y los metadatos de **Pinterest** en inteligencia de negocio, permitiendo a los operadores asignar recursos, cubrir brechas de monetización y tomar decisiones basadas en el **retorno de inversión real (ROI)**.

---

## ⚙️ Motor de Scoring: "El Protocolo Mercenario"
El núcleo analítico del sistema. Elimina las métricas de vanidad aplicando una fórmula asimétrica que castiga la inacción y premia la intención de compra. Los activos son auditados y reclasificados automáticamente en tiempo real.

> **Ponderación Táctica:**
> `Score = (Revenue × 20.0) + (Clicks × 5.0) + (Saves × 0.5) + (Impressions × 0.001)`

<div align="center">
  <b>[  DUST ]</b> < 100 <b>|</b>
  <b>[  COMMON ]</b> ≥ 100 <b>|</b>
  <b>[  UNCOMMON ]</b> ≥ 500 <b>|</b>
  <b>[  RARE ]</b> ≥ 1500 <b>|</b>
  <b>[  LEGENDARY ]</b> ≥ 5000
</div>

---

## 🏗️ Ontología de Datos y Arquitectura
El modelo relacional (PostgreSQL) asegura cero incertidumbre operativa mediante una jerarquía estricta de 3 niveles:

1.  **Nivel 1: Matrices (Brands/Silos).** Entidades de máximo nivel (`matrix_registry`). Consolidan la eficiencia, KPIs y salud financiera de todos los activos bajo su mando.
2.  **Nivel 2: Activos de Negocio (SKUs).** La unidad central de valor (`business_assets`). Contienen el estado de rareza, infraestructura y enlaces de pasarelas de pago (Payhip/Drive).
3.  **Nivel 3: Nodos Tácticos (Pins).** Los captadores de tráfico (`pinterest_nodes`). Se enlazan al SKU para transferirle poder y estadísticas.

---

## 📡 Radares Operativos (Business Intelligence)
La lógica pesada recae en **Vistas SQL**, dejando que el Frontend actúe como una torre de control ultrarrápida:

*  **Void Terminal:** Identifica nodos orgánicos huérfanos y permite su emparejamiento manual con SKUs.
*  **Hemorrhage Console:** Detecta fugas críticas de capital (Activos `RARE`/`LEGENDARY` carentes de link de monetización).
*  **Infra Console:** Auditoría de brechas de infraestructura digital (Productos sin asset final en Google Drive).
*  **Ghost Console:** Identificación y purga de SKUs creados sin tráfico asociado, limpiando el registro.
*  **Elite Vault:** Dashboard gerencial aislado para escalar las campañas de los activos de nivel Legendario.

---

## 💻 Instalación y Despliegue Local

### 1. Variables de Entorno
Crea un archivo `.env.local` en la raíz. El motor táctico depende de Supabase para los recálculos en la base de datos:
```env
VITE_SUPABASE_URL=tu_supabase_url
VITE_SUPABASE_ANON_KEY=tu_supabase_anon_key
```
### 2. Inicialización de la Interfaz
Compilado sobre Vite para un HMR (Hot Module Replacement) instantáneo:

```Bash
npm install
npm run dev
```
---

## Guía de Instalación en Supabase (Backend)
Para desplegar el cerebro de LA BÓVEDA, sigue estos pasos en el editor SQL de tu proyecto de Supabase:

### Paso 1: Creación de Esquema y Tablas
```SQL
-- 1. Registro de Matrices
CREATE TABLE matrix_registry (
  matrix_code TEXT PRIMARY KEY,
  visual_name TEXT,
  type TEXT DEFAULT 'PRIMARY',
  asset_count INT DEFAULT 0,
  total_score NUMERIC DEFAULT 0,
  last_audit_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- 2. Activos de Negocio
CREATE TABLE business_assets (
  sku TEXT PRIMARY KEY,
  primary_matrix_id TEXT REFERENCES matrix_registry(matrix_code),
  rarity_tier TEXT DEFAULT 'DUST',
  total_score NUMERIC DEFAULT 0,
  traffic_score NUMERIC DEFAULT 0,
  revenue_score NUMERIC DEFAULT 0,
  drive_link TEXT,
  payhip_link TEXT,
  last_audit_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- 3. Nodos de Tráfico
CREATE TABLE pinterest_nodes (
  pin_id TEXT PRIMARY KEY,
  asset_sku TEXT REFERENCES business_assets(sku),
  image_url TEXT,
  cached_impressions INT DEFAULT 0,
  cached_outbound_clicks INT DEFAULT 0,
  cached_pin_clicks INT DEFAULT 0,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### Paso 2: Implementación de la Lógica de Auditoría
Debes crear funciones de base de datos que repliquen la lógica de forceMatrixRecalculation para asegurar que las matrices se actualicen cuando un activo cambia.

### Paso 3: Despliegue de Vistas (Radares)
```SQL
CREATE VIEW radar_the_void AS
SELECT * FROM pinterest_nodes WHERE asset_sku IS NULL;

CREATE VIEW radar_monetization_ready AS
SELECT * FROM business_assets 
WHERE rarity_tier IN ('RARE', 'LEGENDARY') AND payhip_link IS NULL;
```

### Paso 4: Automatización (Edge Functions)
Para que el sistema "viva", configura un Cron Job que invoque las tareas de sincronización (Inventory Sync) y el recálculo masivo ("The Judge") cada 15-60 minutos.

---
