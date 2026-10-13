# LAB 13 — TOKEN DUE DILIGENCE
## Auditoría Técnica, On-Chain y Documental: Fair-Launch (DOGE) vs. Emisión Regulada Tohkn (MMLTI1)

**Curso:** TechFreedom (CS031) — Módulo 7: Tokenomics  
**Sesión:** Sesión 15 — Due Diligence de Tokens  
**Fecha de consulta y auditoría:** 12 de octubre de 2026, 23:40 CST  
**Zona horaria de referencia:** America/Guatemala (UTC-6)  
**Estado de la entrega:** Completa — Informe de Due Diligence, Auditoría On-Chain, Rúbrica Oficial S15, Memo Comparativo y Peer Presentation Notes  

---

## 1. RESUMEN EJECUTIVO

El presente informe constituye una auditoría forense de *due diligence* aplicada a dos activos representativos de extremos opuestos del espectro de activos digitales:
1. **Dogecoin (DOGE):** Criptoactivo de emisión abierta (*fair-launch*) bajo consenso Proof-of-Work, sin asignación previa a fundadores ni intermediarios legales, caracterizado por liquidez masiva global, acceso totalmente *permissionless* y volatilidad ligada puramente a dinámicas de mercado.
2. **MMLTI1 (Tramo 1 del Programa MMY de MultiMoney en TOHKN):** Oferta pública de activos digitales de deuda corporativa estructurada bajo la Ley de Emisión de Activos Digitales (LEAD) de El Salvador, supervisada por la Comisión Nacional de Activos Digitales (CNAD) y emitida mediante contratos inteligentes bajo el estándar ERC-3643 en la red Polygon.

### Hallazgos Principales de la Auditoría

```
+----------------------------------------------------------------------------------------------------+
|                                SÍNTESIS DE AUDITORÍA COMPARATIVA                                   |
+-----------------------------+-----------------------------------+----------------------------------+
| Dimensión                   | Dogecoin (DOGE)                   | MultiMoney Tranche 1 (MMLTI1)    |
+-----------------------------+-----------------------------------+----------------------------------+
| Naturaleza Jurídica         | Criptomoneda nativa (sin emisor)  | Token de deuda senior quirograf. |
| Marco Regulatorio           | Ninguno / Jurisprudencia global   | LEAD (El Salvador) / CNAD AD-0252|
| Infraestructura             | Dogecoin Blockchain (Scrypt PoW)  | Polygon (PoS) / Estándar ERC-3643|
| Trazabilidad On-Chain       | 100% auditable y código abierto   | Contrato NO verificado en explorer|
| Roles Administrativos       | Inexistentes (Consenso distribuido)| Owner, Agent, Pauser, Freeze    |
| Restricción de Transferencia| Cero fricción (Cualquier wallet)  | Lock-up 180 días + KYC Whitelist |
| Liquidez 24h                | ~$854M USD (Altísima)             | Iliquidez estructural (Sin AMM)  |
| Riesgo Predominante         | Riesgo de mercado y volatilidad   | Riesgo de crédito y contraparte  |
+-----------------------------+-----------------------------------+----------------------------------+
```

1. **Hallazgo Forense de Trazabilidad y Contratos:**  
   La página pública de TOHKN no publica la dirección del smart contract. La búsqueda documental reveló una discrepancia crítica entre fuentes oficiales:
   - El **Documento de Información Relevante (DIR)** estipula la dirección de Polygon Mainnet: `0x6682b57FA1148b3831aE8610cd6Cbe961d610329`.
   - El **Informe de Certificación Independiente (Armor Analytics)** evaluó la dirección `0x40bC415Fb08b49DC6853F067E61A1a4FF7490559`, admitiendo en el cuerpo del informe que dicha auditoría se ejecutó sobre **BSC Testnet** con migración pendiente a Polygon Mainnet.
   - La consulta RPC en Polygon Mainnet confirmó que `0x6682b57FA1148b3831aE8610cd6Cbe961d610329` existe y responde al nombre `"MIO3 MM Tokenized Senior Debt Note Tranch 1"` con símbolo `MMLTI1` y un supply pre-acuñado de 2,000,000 tokens. Sin embargo, en **PolygonScan el código fuente figura como NO VERIFICADO (`Unverified`)**, lo que impide la verificación pública directa del código fuente auditado contra el bytecode en producción.

2. **Poderes Administrativos ERC-3643:**  
   A través del desmontaje y resolución de selectores de la máquina virtual de Ethereum (EVM), se demostró la presencia activa de funciones de control centralizado: `pause()`, `freezePartialTokens()`, `setAddressFrozen()`, `forcedTransfer()`, `batchForcedTransfer()`, `burn()` y `recoveryAddress()`. Estos mecanismos otorgan al emisor y al PSAD la facultad tecnológica unilateral de inmovilizar, confiscar y transferir tokens sin el consentimiento de la llave privada del tenedor.

3. **Inconsistencia de Tasas y Estructura Financiera:**  
   Mientras el material comercial de TOHKN promociona un *"interés fijo anual del 6.20%"*, el informe técnico de certificación revela que el costo financiero efectivo total para el emisor es de **aproximadamente 6.97% anual** tras incorporar comisiones de estructuración, *listing*, suscripción y certificación. Paralelamente, el DIR certifica que MultiMoney coloca estos fondos en su cartera de créditos a una tasa bruta promedio superior al **30% anual**, configurando un negocio de intermediación financiera clásico donde el inversor asume el riesgo crediticio quirografario sin participar del margen financiero.

---

## 2. KICKOFF: MEME COIN SELECCIONADO (DOGECOIN - DOGE)

Para el análisis de referencia de cero fricción y emisión abierta, se seleccionó **Dogecoin (DOGE)** por constituir el arquetipo histórico y de mayor capitalización de *meme coin* con historial transparente y datos públicos auditables.

```
+----------------------------------------------------------------------------------------------------+
|                                FICHA TÉCNICA Y DE MERCADO: DOGECOIN                                |
+------------------------------------+---------------------------------------------------------------+
| Parámetro                          | Dato Registrado / Evidencia On-Chain                          |
+------------------------------------+---------------------------------------------------------------+
| Nombre y Ticker                    | Dogecoin (DOGE)                                               |
| Tipo de Activo                     | Criptomoneda nativa / Meme coin de primera generación          |
| Blockchain                         | Dogecoin Core (Capa 1 nativa, bifurcación Scrypt de Litecoin)  |
| Mecanismo de Consenso              | Proof-of-Work (AuxPoW / Merge-mined con Litecoin desde 2014)  |
| Venue / Mercado de Referencia      | Binance Spot (Par DOGE/USDT)                                  |
| Fecha y Hora de la Consulta        | 12 de octubre de 2026, 23:40 CST (America/Guatemala, UTC-6)   |
| Precio Spot (Binance DOGE/USDT)    | $0.08475 USDT                                                 |
| Precio Promedio Global (CoinGecko) | $0.08458 USD                                                  |
| Rango 24h (Binance)                | Mínimo: $0.08004 USDT | Máximo: $0.08797 USDT                 |
| Capitalización de Mercado          | $13,221,459,279 USD (~$13.22B USD)                            |
| Suministro Circulante              | 156,302,196,383 DOGE (CoinGecko)                              |
| Suministro Total                   | 172,014,613,126 DOGE (Emisión infinita / desinflacionaria)    |
| Volumen Negociado 24h (Binance)    | 868,485,162 DOGE (~$73,013,649 USDT en quoteVolume)           |
| Volumen Global 24h (CoinGecko)     | $854,054,862 USD (Consolidado multicambio)                    |
| Número de Operaciones 24h (Binance)| 482,667 transacciones ejecutadas en el par DOGE/USDT          |
+------------------------------------+---------------------------------------------------------------+
```

### Proporción de Compradores vs. Vendedores (24 Horas)
- **Limitación en Spot:** La API pública de Binance Spot proporciona el conteo de ejecuciones (482,667 operaciones), pero no desagrega el número exacto de billeteras individuales compradoras frente a vendedoras (dato no reportado a nivel de identidades por la estructura de orden emparejada).
- **Evidencia Técnica en Taker Volume (Binance Futures & CoinGlass Metrics):**
  Para evaluar la presión compradora y vendedora en la ventana de 24 horas, se consultaron las métricas de volumen agresivo (*Taker Buy/Sell Ratio*) en el contrato perpetuo DOGEUSDT de Binance:
  - **Taker Buy/Sell Ratio:** `0.8088` (Dominancia neta vendedora en las últimas 24 horas).
  - **Volumen Vendedor Agresivo (Taker Sell Volume):** 2,786,900,050 DOGE (equivalente al **55.28%** del volumen agresivo).
  - **Volumen Comprador Agresivo (Taker Buy Volume):** 2,254,019,711 DOGE (equivalente al **44.72%** del volumen agresivo).
  - **Ratio de Cuentas Top Traders Long/Short:** 75.50% cuentas en posición neta larga frente a 24.50% en posición corta (Ratio: 3.0817), lo que demuestra acumulación minorista en posiciones largas mientras el flujo de mercado spot/taker presiona ventas de liquidación.

### Enlaces y Evidencia Documental
- Binance API Endpoint Spot: `https://api.binance.com/api/v3/ticker/24hr?symbol=DOGEUSDT`
- Binance Futures Taker Metrics: `https://fapi.binance.com/futures/data/takerlongshortRatio?symbol=DOGEUSDT&period=1d`
- CoinGecko Dogecoin Overview: [CoinGecko DOGE](https://www.coingecko.com/en/coins/dogecoin)
- Explorador Dogecoin Blockchair: [Dogecoin Explorer](https://blockchair.com/dogecoin)

---

## 3. EMISIÓN PÚBLICA TOHKN: ANÁLISIS INTEGRAL DE MMLTI1

```
+----------------------------------------------------------------------------------------------------+
|                                FICHA TÉCNICA REGULADA: MMLTI1                                      |
+------------------------------------+---------------------------------------------------------------+
| Campo                              | Especificación Técnica / Legal                                |
+------------------------------------+---------------------------------------------------------------+
| Ticker del Tramo                   | MMLTI1                                                        |
| Denominación del Programa          | Programa de Emisión de Deuda Tokenizada MMY                   |
| Entidad Emisora                    | Sociedad de Ahorro y Crédito MultiMoney, S.A.                 |
| Naturaleza del Emisor              | Institución financiera supervisada por la SSF (El Salvador)   |
| Plataforma de Emisión              | TOHKN (URL: https://www.tohkn.com/es/issuances/mmlti1)        |
| PSAD y Agente de Pago              | MIO3, S.A. de C.V. (Registro CNAD: PSAD-0016)                 |
| Certificador Independiente         | Armor Analytics, S.A. de C.V. (Registro CNAD: CERT-0005)      |
| Jurisdicción y Ley Aplicable       | República de El Salvador — Ley de Emisión de Activos Digitales|
| Registro Público CNAD              | Número de Registro: AD-00252 (Emisor registrado: EAD-0046)    |
| Red Blockchain                     | Polygon Mainnet (Proof-of-Stake EVM Layer 2 / Sidechain)      |
| Estándar de Tokenización           | ERC-3643 (Suite T-REX de permissioned security tokens)        |
| Tipo de Activo Digital             | Token de deuda corporativo / Valor digital representativo     |
| Activo Subyacente                  | Derecho crediticio quirografario frente al emisor             |
| Monto Máximo del Programa          | Hasta US$10,000,000.00                                        |
| Monto Máximo del Primer Tramo      | Hasta US$2,000,000.00 (MMLTI1)                                |
| Valor Nominal Unitario             | US$100.00 por token                                           |
| Número Máximo de Tokens (Tramo 1)  | Hasta 20,000 tokens MMLTI1                                    |
| Inversión Mínima                   | US$100.00 (Equivalente a 1 token MMLTI1)                      |
| Importe Mínimo de Colocación       | US$50,000.00 (Si no se alcanza en 5 meses, se devuelve capital)|
| Tasa de Interés Nominal Fija       | 6.20% anual fija para el Primer Tramo                         |
| Tasa de Interés Moratoria          | Tasa nominal aplicable + 3.00% anual moratorio                |
| Periodicidad de Pago de Intereses  | Mensual, vencido y sucesivo (último día hábil de cada mes)    |
| Amortización de Capital            | Pago único al vencimiento (Estructura Bullet a 24 meses)      |
| Plazo de Vigencia del Tramo        | 24 meses contados desde la fecha de emisión                   |
| Moneda de Denominación / Pago      | Denominado en USD; liquidado en stablecoins (USDT o USDC)     |
| Período de Inmovilización (Lock-up)| 180 días calendario desde la adquisición en billetera digital |
| Mecanismo de Redención Anticipada  | Exclusivamente a opción del Emisor tras 90 días calendario     |
| Mercado Secundario                 | Restringido exclusivamente a TOHKN si se habilita (Sin AMM)   |
| Destino de Fondos Declarado        | Crecimiento y expansión de la cartera de crédito de MultiMoney|
+------------------------------------+---------------------------------------------------------------+
```

### Documentación Oficial Verificada
1. **Documento de Información Relevante (DIR) y Anexos:** 310 páginas. Incluye estados financieros auditados, estructura corporativa, balance patrimonial y características del programa.
2. **Términos y Condiciones del Programa y Primer Tramo:** 7 páginas. Detalla las reglas contractuales, procedimientos de mora, custodia y cláusulas de exoneración.
3. **Informe de Certificación Independiente (Armor Analytics):** 42 páginas. Evaluación de razonabilidad legal, económica y técnica bajo normativa CNAD.
4. **Aviso de Oferta Pública:** 2 páginas. Publicación formal de apertura de la oferta.

---

## 4. AUDITORÍA FORENSE DEL SMART CONTRACT DE MMLTI1

### 4.1. Búsqueda y Localización del Contrato
El Session Doc S15 señala explícitamente: *"La ausencia de 0x en la landing es parte del lab"*. La landing page oficial de TOHKN omite deliberadamente la dirección pública del contrato, obligando al auditor a rastrear el contrato a través de los expedientes regulatorios.

```
                              RASTREO DOCUMENTAL DEL SMART CONTRACT
                                                │
                 ┌──────────────────────────────┴──────────────────────────────┐
                 ▼                                                             ▼
     Documento DIR (Pág. 3 / Anexos)                             Informe Certificación (Pág. 10)
     Address: 0x6682b57FA1148b3831aE8610cd6Cbe961d610329         Address: 0x40bC415Fb08b49DC6853F067E61A1a4FF7490559
     Red: Polygon Mainnet                                        Red declarada: Polygon (Pero auditado en BSC Testnet)
                 │                                                             │
                 ▼                                                             ▼
         CONSULTA RPC POLYGON                                          CONSULTA RPC POLYGON
     Bytecode: EXISTE (3,220 chars)                              Bytecode: 0x (NO EXISTE EN POLYGON)
     Estado: ACTIVO / MMLTI1                                     Bytecode en BSC Testnet: EXISTE (3,220 chars)
```

- **Inconsistencia de Direcciones:**
  - El DIR declara formalmente como dirección única de MMLTI1:  
    `0x6682b57FA1148b3831aE8610cd6Cbe961d610329`
  - La Certificación de Armor Analytics evaluó:  
    `0x40bC415Fb08b49DC6853F067E61A1a4FF7490559`  
    El dictamen admite en la página 27: *"El DIR indica que fue desplegado inicialmente en BSC Testnet, con migración pendiente a Polygon mainnet sujeta a autorización regulatoria, lo que implica que la versión de producción definitiva aún no ha sido validada en el entorno final"*.
- **Verificación On-Chain en PolygonScan:**
  - Enlace oficial: [PolygonScan 0x6682...0329](https://polygonscan.com/address/0x6682b57FA1148b3831aE8610cd6Cbe961d610329)
  - **Estado de verificación:** **UNVERIFIED (Código no verificado)**. PolygonScan reporta textualmente: `Contract: Unverified | Token Rep: Unknown | Balance: $0 across 0 Chains | Transactions: 0`.

### 4.2. Arquitectura Técnica de MMLTI1 en Polygon Mainnet
A pesar de la falta de verificación en el explorador, la consulta mediante llamadas RPC de bajo nivel (`eth_call`, `eth_getStorageAt`, `eth_getCode`) permitió reconstruir la arquitectura completa:

```
+----------------------------------------------------------------------------------------------------+
|                              ARQUITECTURA DE TRES CAPAS (TOKENY T-REX)                             |
+----------------------------------------------------------------------------------------------------+
| 1. TokenProxy (Capa de Acceso y Almacenamiento):                                                   |
|    Dirección: 0x6682b57FA1148b3831aE8610cd6Cbe961d610329                                          |
|    Bytecode: 1,610 bytes (3,220 hex chars)                                                         |
|    Almacena variables de estado: balances, roles, listas blancas e historial.                     |
|                                                                                                    |
| 2. ImplementationAuthority (Capa de Gobernanza y Actualización):                                   |
|    Dirección: 0x387b9ced9a3e638168dbd4992d06a0b5ba6ece18                                          |
|    Almacenada en el storage slot: 0xc5f16f0fcc639fa48a6947836d9850f504798523bf8c9a3a87d5876cf622bcf7|
|    Bytecode: 8,894 bytes (17,788 hex chars)                                                        |
|    Gobernador Owner: 0x0921785a4b0f184141a9afff0f8b3b37e50caf46                                   |
|                                                                                                    |
| 3. Token Implementation Logic (Capa de Ejecución ERC-3643):                                       |
|    Dirección: 0x1ba05496ec2bf932d522d0e2820428ca78f7a317                                          |
|    Obtenida mediante llamada estática: 0x709bc7f3                                                  |
|    Bytecode: 14,415 bytes (28,830 hex chars)                                                       |
+----------------------------------------------------------------------------------------------------+
```

### 4.3. Variables de Estado Leídas On-Chain
- `name()` (`0x06fdde03`): `"MIO3 MM Tokenized Senior Debt Note Tranch 1"`
- `symbol()` (`0x95d89b41`): `"MMLTI1"`
- `decimals()` (`0x313ce567`): `18` (0x12)
- `totalSupply()` (`0x18160ddd`): `2,000,000,000,000,000,000,000,000` (2,000,000 * 10^18)
- `owner()` (`0x8da5cb5b`): `0xc7369964d6151fc0c095d5781b30eb3b80562a59`
- `paused()` (`0x5c975abb`): `false` (0x00)

> [!WARNING]
> **Discrepancia en Supply Acuñado vs. Valor Nominal:**  
> El DIR define que el valor nominal de cada token es de **US$100.00** y que el Primer Tramo comprende hasta **20,000 tokens** (Total: US$2,000,000.00). Sin embargo, el contrato inteligente fue desplegado con un `totalSupply` de **2,000,000 de unidades completas** (18 decimales). Esto indica que a nivel de contrato cada token numérico representa **US$1.00**, o bien el emisor acuñó el equivalente al valor en dólares en lugar de la cantidad de títulos unitarios declarada en el prospecto.

### 4.4. Desmontaje Forense de Funciones Privilegiadas (Selectores EVM)
Del análisis del despachador del contrato lógico (`0x1ba054...a317`), se identificaron y resolvieron 46 selectores que configuran los poderes de la administración sobre los inversionistas:

```
+----------------------------------------------------------------------------------------------------+
|                         MATRIZ DE FUNCIONES PRIVILEGIADAS Y RIESGO INVERSOR                        |
+-------------+------------------------------------+------------------+------------------------------+
| Selector    | Función EVM Identificada           | Rol Autorizado   | Impacto Directo al Inversor  |
+-------------+------------------------------------+------------------+------------------------------+
| 0x8456cb59  | pause()                            | Agent / Owner    | Congela todas las            |
| 0x3f4ba83a  | unpause()                          | Agent / Owner    | transferencias del token.    |
+-------------+------------------------------------+------------------+------------------------------+
| 0xc69c09cf  | setAddressFrozen(address,bool)     | Agent / Owner    | Bloquea billeteras concretas |
| 0x1a7af379  | batchSetAddressFrozen(...)         | Agent / Owner    | por orden judicial o interna.|
+-------------+------------------------------------+------------------+------------------------------+
| 0x125c4a33  | freezePartialTokens(address,amt)   | Agent / Owner    | Inmoviliza una cantidad      |
| 0x1fe56f7d  | unfreezePartialTokens(address,amt) | Agent / Owner    | específica de saldo.         |
+-------------+------------------------------------+------------------+------------------------------+
| 0x9fc1d0e7  | forcedTransfer(from, to, amt)      | Agent / Owner    | Transfiere tokens sin permiso|
| 0x42a47abc  | batchForcedTransfer(...)           | Agent / Owner    | de la llave privada.         |
+-------------+------------------------------------+------------------+------------------------------+
| 0x9dc29fac  | burn(address, uint256)             | Agent / Owner    | Destruye tokens en billetera |
| 0x4a6cc677  | batchBurn(address[], uint256[])    | Agent / Owner    | de cualquier titular.        |
+-------------+------------------------------------+------------------+------------------------------+
| 0x40c10f19  | mint(address, uint256)             | Agent / Owner    | Emite nuevos tokens sin      |
| 0x68573107  | batchMint(address[], uint256[])    | Agent / Owner    | restricción matemática dura. |
+-------------+------------------------------------+------------------+------------------------------+
| 0x9285948a  | recoveryAddress(lost, new, id)     | Agent / Owner    | Recuperación por pérdida de  |
|             |                                    |                  | llaves o incautación.        |
+-------------+------------------------------------+------------------+------------------------------+
| 0xcbf3f861  | setIdentityRegistry(address)       | Owner            | Modifica el registro de KYC  |
| 0xf8981789  | setCompliance(address)             | Owner            | y las reglas de elegibilidad.|
+-------------+------------------------------------+------------------+------------------------------+
| 0x709bc7f3  | upgrade (vía ImplAuthority)        | Owner IA         | Reemplaza todo el bytecode   |
|             |                                    |                  | por una lógica arbitraria.   |
+-------------+------------------------------------+------------------+------------------------------+
```

---

## 5. CLAIMS CONTRA CÓDIGO Y DOCUMENTACIÓN

```
+------------------------------------------------------------------------------------------------------------------------------------------+
|                                                   TABLA DE AUDITORÍA: CLAIMS VS. REALIDAD                                                |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Claim Público        | Fuente             | Evidencia Técnica / Documental            | Resultado              | Riesgo para el Inversor |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Tasa de Interés      | Web TOHKN          | DIR pág. 3: 6.20% nominal fija.           | Inconsistente /        | El inversor recibe una  |
| Fija 6.20%           | Landing MMLTI1     | Certificación pág. 27: Costo financiero   | Parcialmente           | tasa inferior a la      |
|                      |                    | emisor es 6.97% por fees. Rentabilidad    | Confirmado             | inflación real o al     |
|                      |                    | cartera MultiMoney: >30% anual.           |                        | spread del emisor.      |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Derechos del Token   | Web TOHKN &        | DIR pág. 2 y Términos Cláusula 3:         | Confirmado             | Si MultiMoney quiebra,  |
| (Crédito, no Equity) | DIR Sección 8.1    | Crédito quirografario, no subordinado,    |                        | no hay garantías reales |
|                      |                    | sin colateral ni participación societaria.|                        | ni respaldo de activos. |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Propiedad sobre      | Expectativa común  | Términos Cláusula 3: Los tokens no        | No Confirmado          | Cero derechos políticos,|
| MultiMoney           | en retail crypto   | otorgan votos, acciones ni propiedad.     | (Mito refutado)        | dividendos ni control.  |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Liquidez del Activo  | Web TOHKN          | Términos Cláusula 7: "No existe garantía  | Inconsistente con      | Iliquidez absoluta      |
| Digital              | "Invierte fácil"   | de liquidez... ni obligación de recompra".| marketing              | forzosa durante 24      |
|                      |                    | Lock-up estricto de 180 días on-chain.    |                        | meses de plazo.         |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Transferibilidad     | Narrativa Web3     | Código Polygon: Selector 0x134e18f4       | No Confirmado          | No transferible libre-  |
| Abierta              | "Activos digitales"| (Identity Registry) y 0xc69c09cf freeze.  | (Permissioned total)   | mente; censurable.      |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Lock-up de 180 días  | DIR & Términos     | Términos Cláusula 8.2: Inmovilización     | Confirmado             | Imposibilidad de vender |
|                      | Cláusula 8.2       | tecnológica de 180 días calendario.       | documentalmente        | ante emergencias.       |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Regulación y         | Web TOHKN &        | Registro CNAD AD-00252 y EAD-0046.        | Parcialmente           | La CNAD habilita oferta;|
| Respaldo Estatal     | Comunicados LEAD   | Supervisión SSF es a MultiMoney como SAC, | Confirmado             | el Estado no garantiza  |
|                      |                    | NO avala ni asegura el pago del token.    |                        | solvencia ni reembolsos.|
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Liquidación de       | Landing & DIR      | Se pagan en USDT o USDC dentro de la      | Confirmado             | Riesgo de despegue de   |
| Pagos en Stablecoins | Sección 8.1.5      | app TOHKN. Intermediación centralizada.   |                        | paridad (depeg) y PSAD. |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Descentralización y  | Narrativa Blockchain| Bytecode en Polygon: 0x9fc1d0e7 (forced   | Falso / Inconsistente  | Control autocrático:    |
| Control del Usuario  | TOHKN              | transfer) y 0x8456cb59 (pause) activos.   | con Web3               | el emisor puede mover   |
|                      |                    | Código NO verificado en Polygonscan.      |                        | o congelar el dinero.   |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
| Dirección Unívoca    | Landing vs. DIR vs.| DIR indica 0x6682...0329 en Polygon.      | Inconsistente          | Se auditó un contrato   |
| de Contrato          | Certificación      | Certificación indica 0x40bC...0559 en BSC.| entre documentos       | en testnet distinto al  |
|                      |                    | Landing no publica ninguna dirección.     |                        | desplegado en mainnet.  |
+----------------------+--------------------+-------------------------------------------+------------------------+-------------------------+
```

---

## 6. APLICACIÓN DE LA RÚBRICA OFICIAL DE DUE DILIGENCE (SESIÓN 15)

Conforme a lo especificado en el documento rector de la **Sesión 15 (CS031 · Tokenomics)**, se aplica la rúbrica oficial de 10 criterios de evaluación económica y técnica. Cada ítem se puntúa de **0 a 2 puntos** (0: ausente/opaco, 1: parcial, 2: claro y verificable).  
- **Puntuación Máxima:** 20 puntos.  
- **Conversión:** Puntuación base 10 (`Score / 2`) y Porcentaje de Cumplimiento (`Score / 20 * 100`).

```
+----------------------------------------------------------------------------------------------------+
|                             EVALUACIÓN OFICIAL DE RÚBRICA S15 (10 CRITERIOS)                       |
+----+--------------------------------+-------+-------+----------------------------------------------+
| #  | Criterio Oficial S15           | DOGE  | MMLTI1| Justificación Comparativa                    |
+----+--------------------------------+-------+-------+----------------------------------------------+
| 1  | Clarity of unit                |   2   |   2   | DOGE: 1 DOGE = 1 unidad de red sin deuda.    |
|    | ¿Está claro qué representa     |       |       | MMLTI1: 1 Token = $100 de crédito senior     |
|    | 1 token?                       |       |       | frente a SAC MultiMoney (DIR Cláusula 8.1).  |
+----+--------------------------------+-------+-------+----------------------------------------------+
| 2  | Supply / cap honesty           |   2   |   1   | DOGE: Emisión determinista (10k DOGE/bloque).|
|    | Total vs circulating; mint     |       |       | MMLTI1: DIR dice 20,000 tokens de $100, pero |
|    | authority; surprises           |       |       | contrato acuñó 2,000,000 unidades completas. |
+----+--------------------------------+-------+-------+----------------------------------------------+
| 3  | Allocation & unlocks           |   2   |   1   | DOGE: Fair launch sin pre-mine ni insiders.  |
|    | Team/investors/community;      |       |       | MMLTI1: Lock-up de 180 días declarado en DIR |
|    | cliffs; next unlock            |       |       | pero no auditable en código no verificado.   |
+----+--------------------------------+-------+-------+----------------------------------------------+
| 4  | Sinks / spend                  |   1   |   1   | DOGE: Tarifas de transacción (muy bajas).    |
|    | Uso real vs yield circular     |       |       | MMLTI1: Se fondea crédito al consumo; el     |
|    |                                |       |       | yield proviene de deudores de MultiMoney.    |
+----+--------------------------------+-------+-------+----------------------------------------------+
| 5  | Emission schedule              |   2   |   2   | DOGE: 5 mil millones de DOGE/año constantes. |
|    | Quién recibe inflación y ritmo |       |       | MMLTI1: Sin inflación; tramo cerrado de      |
|    |                                |       |       | hasta $2M con vigencia bullet a 24 meses.    |
+----+--------------------------------+-------+-------+----------------------------------------------+
| 6  | Value accrual falsable         |   0   |   1   | DOGE: Cero devengo intrínseco (pura memética)|
|    | Demanda ligada a uso/activo    |       |       | MMLTI1: Flujo de interés 6.20% anual ligado  |
|    |                                |       |       | a capacidad de pago quirografaria del emisor.|
+----+--------------------------------+-------+-------+----------------------------------------------+
| 7  | Governance / admin keys        |   2   |   0   | DOGE: Consenso descentralizado PoW.          |
|    | Quién puede cambiar reglas o   |       |       | MMLTI1: Monarquía absoluta: Owner y Agents   |
|    | ruggear                        |       |       | tienen pause, freeze, burn y upgradeability. |
+----+--------------------------------+-------+-------+----------------------------------------------+
| 8  | Liquidity & market structure   |   2   |   0   | DOGE: Mercados globales profundos ($854M/día)|
|    | LP locks, venues, manipulación |       |       | MMLTI1: Cero liquidez externa; prohibido en  |
|    |                                |       |       | DEX; sin garantía de mercado secundario.     |
+----+--------------------------------+-------+-------+----------------------------------------------+
| 9  | Disclosure & docs              |   1   |   1   | DOGE: Código C++ público; sin DIR corporativo|
|    | DIR/whitepaper vs realidad     |       |       | MMLTI1: 310 pág. de DIR pero código NO       |
|    | on-chain                       |       |       | verificado y discrepancia BSC vs Polygon.    |
+----+--------------------------------+-------+-------+----------------------------------------------+
| 10 | Jurisdiction / distribution    |   1   |   2   | DOGE: Riesgo regulatorio global difuso.      |
|    | LEAD/CNAD (ES) vs GT / Howey   |       |       | MMLTI1: Registro CNAD AD-00252 en ES. En GT  |
|    |                                |       |       | requeriría análisis bajo Decreto 15-2026.    |
+----+--------------------------------+-------+-------+----------------------------------------------+
| TOTAL SCORE (sobre 20 puntos)       |  15   |  11   | Puntuaciones finales consolidadas            |
| SCORE ESCALA 0 A 10                 |  7.5  |  5.5  | Dogecoin: 7.5 / 10 | MMLTI1: 5.5 / 10        |
| PORCENTAJE DE CUMPLIMIENTO          | 75.0% | 55.0% | Review Gradebook (>50% -> Aprobado)          |
+-------------------------------------+-------+-------+----------------------------------------------+
```

### Síntesis de Calificación
- **Dogecoin (7.5 / 10):** Obtiene puntuaciones perfectas en transparencia de emisión, ausencia de llaves maestras centralizadas, liquidez extrema y reglas inmutables de suministro. Pierde puntos en *Value Accrual* (su valor no depende de flujos de caja ni activos) y en documentación formal corporativa.
- **MMLTI1 (5.5 / 10):** Destaca en claridad de derechos de crédito, estructuración regulatoria formal y marco de rendición de cuentas financiero (LEAD/CNAD). Sin embargo, es severamente castigado en *Governance/Admin Keys* (0/2 por funciones autocráticas de censura y confiscación), *Liquidity* (0/2 por iliquidez estructural y ausencia de mercado secundario real) y *Supply Honesty* (1/2 por código no verificado y contradicción entre el prospecto y el bytecode acuñado).

---

## 7. MEMO COMPARATIVO: DEUDA REGULADA VS. FAIR-LAUNCH MEME

**Para:** Comité de Inversión y Análisis de Tokenomics (TechFreedom)  
**De:** Equipo de Auditoría de Tokens (Estudiante Universitario CS031)  
**Fecha:** 12 de octubre de 2026  
**Asunto:** Evaluación de Riesgo Estructural: MultiMoney MMLTI1 (Emisión LEAD) vs. Dogecoin (Fair-Launch)

---

### Introducción: El Espejismo de la Descentralización Institucional
Cuando uno empieza a estudiar finanzas descentralizadas, el discurso predominante asegura que la tokenización de activos del mundo real (*Real-World Assets* o RWA) representa la maduración de la industria: traer contratos legales a la blockchain para erradicar el casino especulativo de los *meme coins*. Sin embargo, al desarmar el código y contrastar los contratos inteligentes contra los prospectos legales, la realidad es mucho más cínica. La pregunta fundamental de este *due diligence* no es qué activo tiene mejor mercadeo, sino qué garantías y qué riesgos sobreviven cuando quitamos el logo de la empresa y los memes de internet.

### 1. Fair-Launch sin Fricción vs. Emisión Hiperregulada
Dogecoin representa el modelo de **cero fricción**: nació en 2013 como una broma, sin preventa, sin asignación para los creadores (*zero insider allocation*), sin capital de riesgo y sin intermediarios. Cualquiera puede minarlo, comprarlo, auditar su blockchain o transferirlo a cualquier rincón del planeta en segundos. No pide permiso, no discrimina jurisdicciones y no exige un pasaporte para interactuar con la red.

En el extremo opuesto se encuentra **MMLTI1**. Estructurado bajo la Ley de Emisión de Activos Digitales (LEAD) de El Salvador y registrado ante la CNAD bajo el código AD-00252, es un pagaré digital emitido por una entidad de ahorro y préstamo tradicional (MultiMoney). Para tocar este token, el inversionista debe someterse a una verificación exhaustiva de identidad (KYC/AML), registrarse en la aplicación propietaria de TOHKN (operada por MIO3) y aceptar que sus tokens vivirán en un entorno estrictamente permisionado. No es un activo descentralizado; es un producto financiero tradicional que utiliza la máquina virtual de Polygon como un libro contable electrónico.

### 2. Transparencia Técnica: La Paradoja del Código No Verificado
Aquí encontramos el primer gran hallazgo incómodo del laboratorio. En Dogecoin, el protocolo es 100% abierto y auditable; las reglas de consenso están selladas por miles de nodos mineros. En MMLTI1, nos encontramos con que:
- La página web comercial no publica la dirección del smart contract.
- El informe de certificación independiente auditó un contrato desplegado en **BSC Testnet** (`0x40bC...0559`), mientras que el prospecto legal (DIR) lista una dirección distinta en **Polygon Mainnet** (`0x6682...0329`).
- Al buscar el contrato oficial en PolygonScan, el código fuente **no está verificado** (`Unverified`).

Esto rompe la promesa básica de la tecnología blockchain: *"no confíes, verifica"*. En MMLTI1, el inversionista no puede verificar el código en el explorador y se ve obligado a confiar ciegamente en el prospecto legal y en el certificador independiente. Si un token regulado no permite verificar su bytecode de producción de forma transparente, pierde la superioridad moral técnica sobre los proyectos comunitarios abiertos.

### 3. Derechos Económicos y la Realidad del Negocio
Desde el punto de vista económico, los dos activos responden a motores diametralmente opuestos:
- **DOGE:** No otorga derechos a nada. Poseer DOGE no da derecho a flujos de caja, dividendos ni intereses. Su precio es un juego puro de oferta y demanda global, liquidez macroeconómica y atención comunitaria.
- **MMLTI1:** Es un **token de deuda pura**, no una acción. Muchos inversionistas minoristas cometen el grave error de pensar que comprar MMLTI1 equivale a comprar parte de MultiMoney. Los términos oficiales son tajantes: el token confiere un derecho de crédito frente al emisor (capital más 6.20% de interés anual fijo a 24 meses). No otorga votos, ni participación patrimonial, ni utilidades.

Más revelador aún es el *spread* financiero: MultiMoney levanta capital al 6.20% anual (con un costo financiero efectivo de 6.97% para la empresa), pero en el DIR reporta que coloca sus créditos al consumo a una tasa promedio superior al **30% anual**. Es decir, MultiMoney utiliza a los inversores de TOHKN como fondeo barato para financiar préstamos de alto rendimiento, asumiendo el inversionista un riesgo crediticio quirografario (sin garantías reales) a cambio de un cupón modesto.

### 4. Gobernanza y Censura: Las Puertas Traseras de ERC-3643
El estándar ERC-3643 (T-REX) utilizado por MMLTI1 está diseñado específicamente para cumplir con regulaciones financieras, lo que en la práctica significa **eliminar la soberanía del usuario**. Mediante el desmontaje de los selectores EVM del contrato en Polygon, confirmamos que el emisor y el PSAD tienen el poder técnico de:
1. Pausar todas las operaciones de la red (`pause`).
2. Congelar billeteras particulares (`setAddressFrozen`) o inmovilizar montos parciales (`freezePartialTokens`).
3. Confiscar o reasignar fondos unilateralmente sin la firma del dueño (`forcedTransfer`).
4. Quemar saldos existentes (`burn`).
5. Reemplazar la lógica del contrato mediante el `ImplementationAuthority`.

En Dogecoin, nadie —ni los desarrolladores originales, ni los mineros más poderosos, ni un tribunal— puede revertir una transacción válida ni congelar una billetera. En MMLTI1, el titular de la llave privada no es el dueño soberano del token; es un depositante sujeto al control discrecional del administrador del contrato.

### 5. Comparativa de Riesgos: Mercado vs. Crédito
```
+---------------------------+-----------------------------------+----------------------------------+
| Dimensión de Riesgo       | Dogecoin (DOGE)                   | MultiMoney (MMLTI1)              |
+---------------------------+-----------------------------------+----------------------------------+
| Riesgo de Mercado         | Extremo (Volatilidad de precio)   | Nulo en valor nominal (Pactado)  |
| Riesgo de Crédito / Pef.  | Inexistente (No hay emisor)       | Elevado (Depende de MultiMoney)  |
| Riesgo de Contraparte     | Nulo (Custodia propia posible)    | Total (MIO3, TOHKN, MultiMoney)  |
| Riesgo de Censura/Bloqueo | Imposible en la capa base         | Máximo (Funciones on-chain activ)|
| Riesgo de Iliquidez       | Mínimo ($850M+ volumen diario)    | Extremo (Lock-up de 180 días)    |
| Riesgo Regulatorio        | Ambigüedad de clasificación       | Alto (Régimen LEAD / El Salvador)|
+---------------------------+-----------------------------------+----------------------------------+
```

### Ventajas y Desventajas para el Inversionista
- **Invertir en DOGE:**
  - *Ventajas:* Liquidez instantánea en cualquier mercado del mundo; custodia soberana real sin riesgo de congelamiento; potencial alcista asimétrico si el ciclo de mercado lo favorece.
  - *Desventajas:* Cero protección legal; volatilidad extrema; sin rendimiento intrínseco ni respaldo en activos.
- **Invertir en MMLTI1:**
  - *Ventajas:* Flujo de caja predecible (6.20% fijo pagadero mensualmente); marco regulatorio formal bajo la LEAD; emisor con estados financieros auditados y supervisado por la SSF.
  - *Desventajas:* Iliquidez absoluta por 180 días; sin mercado secundario garantizado; riesgo quirografario (si MultiMoney quiebra, no hay colateral que liquide la deuda); control administrativo absoluto del contrato; código no verificado en PolygonScan.

### Reflexión Regulatoria: LEAD (El Salvador) vs. Guatemala (Decreto 15-2026) y Howey
La existencia de MMLTI1 es posible gracias a la Ley de Emisión de Activos Digitales (LEAD) de El Salvador, que creó una categoría legal expresa para emisiones tokenizadas con supervisión de la CNAD. Sin embargo, si esta oferta se comercializara activamente a residentes en Guatemala, la situación cambiaría sustancialmente:
- Bajo el nuevo marco guatemalteco (Decreto 15-2026 sobre Proveedores de Servicios de Activos Virtuales - PSAV), comercializar instrumentos financieros extranjeros a usuarios locales sin registro ni cumplimiento con la Superintendencia de Bancos (SIB) y la Ley del Mercado de Valores y Mercancías podría constituir una oferta pública irregular.
- Bajo el análisis del *Test de Howey* estadounidense, MMLTI1 cumple indiscutiblemente todos los criterios de un *security* (inversión de dinero en una empresa común con expectativa razonable de ganancias derivadas exclusivamente del esfuerzo del emisor), lo que confirma por qué debe estar restringido a inversionistas fuera de jurisdicciones no amparadas por la LEAD.

### Conclusión del Estudiante
Al final del día, la auditoría demuestra que ninguna de las dos opciones ofrece un "almuerzo gratis":
- **Dogecoin es el rostro honesto del libre mercado especulativo:** no te promete rendimientos, no finge tener un balance contable detrás y no te puede congelar la cuenta. Asumes riesgo de precio, pero tienes libertad técnica absoluta.
- **MMLTI1 es una emisión corporativa tradicional disfrazada de Web3:** ofrece la promesa de renta fija bajo el amparo de la ley, pero sacrifica toda la descentralización, te somete a un riesgo de crédito puro sin colateral, impone iliquidez forzosa y mantiene un control tecnológico centralizado con código no verificado.

Para un perfil conservador que busca renta fija en dólares y confía plenamente en la solvencia del sistema financiero salvadoreño, MMLTI1 puede tener sentido como pagaré. Pero para cualquiera que entienda la tecnología blockchain, catalogar a MMLTI1 como "activo descentralizado" es un error conceptual: es simplemente un contrato legal tradicional que utiliza Polygon como base de datos permisionada.

---

## 8. PEER PRESENTATION NOTES (PREGUNTAS Y RESPUESTAS DEFENSIVAS)

A continuación se presentan las 10 preguntas y respuestas clave preparadas para la sesión de defensa y presentación entre pares:

### 1. ¿Qué diferencia estructural hay entre DOGE y MMLTI1?
**R:** DOGE es una criptomoneda nativa sin emisor, basada en su propia blockchain de consenso Proof-of-Work, con emisión determinista y liquidez masiva global. MMLTI1 es un token de deuda corporativa emitido en Polygon bajo el estándar ERC-3643 por una sociedad financiera regulada en El Salvador, sujeto a restricciones legales, sin liquidez abierta y respaldado únicamente por la promesa de pago del emisor.

### 2. ¿MMLTI1 representa acciones o propiedad sobre MultiMoney?
**R:** No. MMLTI1 es un token de deuda senior quirografario (un pagaré digital). No confiere acciones, derechos de voto, dividendos ni participación en las utilidades de MultiMoney. Solo confiere un derecho de crédito para recibir el pago de capital e intereses pactados.

### 3. ¿Qué ocurre si MultiMoney entra en insolvencia o no paga?
**R:** El token no cuenta con garantías reales, hipotecarias ni fondos de seguro estatal. Al ser deuda quirografaria, los inversionistas quedan como acreedores comunes no garantizados en un concurso o liquidación mercantil en El Salvador, asumiendo una pérdida total o parcial del capital sin respaldo de colateral on-chain.

### 4. ¿Por qué el estándar ERC-3643 no equivale automáticamente a seguridad para el usuario?
**R:** ERC-3643 está diseñado para dar seguridad y cumplimiento al *emisor* y al *regulador*, no para proteger la soberanía del usuario. Incluye funciones que permiten al administrador congelar billeteras, pausar transferencias y confiscar tokens forzosamente (`forcedTransfer`), eliminando la inmutabilidad y la autocustodia que caracterizan a las redes públicas.

### 5. ¿Qué puede hacer un administrador del contrato de MMLTI1 con mis tokens?
**R:** El administrador (Owner y Agents) tiene facultades técnicas para: pausar las transferencias globales del token (`pause`), congelar una billetera específica (`setAddressFrozen`), bloquear saldo parcial (`freezePartialTokens`), transferir tokens fuera de tu billetera sin tu firma (`forcedTransfer`), quemar tus tokens (`burn`) y reemplazar el código lógico por completo a través del `ImplementationAuthority`.

### 6. ¿Por qué la falta de dirección pública y código no verificado es un hallazgo crítico?
**R:** Porque vulnera el principio de transparencia de blockchain. Si la landing comercial oculta el contrato y el explorador PolygonScan reporta el código como no verificado (`Unverified`), el inversionista no puede auditar el código fuente real que custodia su capital, viéndose obligado a confiar en documentos publicitarios y dictámenes externos.

### 7. ¿La aprobación regulatoria de la CNAD y la supervisión de la SSF eliminan el riesgo de la inversión?
**R:** De ninguna manera. La CNAD autoriza la oferta pública y verifica el cumplimiento de la LEAD, y la SSF supervisa a MultiMoney como entidad de ahorro y préstamo. Ninguno de estos reguladores garantiza el pago, ni asegura el rendimiento, ni indemnizará a los tenedores de tokens en caso de impago o quiebra del emisor.

### 8. ¿Cuál de los dos activos tiene mayor liquidez y por qué?
**R:** Dogecoin tiene una liquidez infinitamente superior. Negocia más de $850 millones de dólares diarios en decenas de exchanges globales con libros de órdenes profundos. MMLTI1 tiene liquidez nula: tiene un lock-up obligatorio de 180 días, no puede listarse en exchanges descentralizados (DEX) y ni TOHKN ni MultiMoney garantizan la existencia de compradores en el mercado secundario.

### 9. ¿Cuál activo tiene mayor riesgo de crédito?
**R:** MMLTI1. En DOGE no existe riesgo de crédito porque no hay ningún emisor que deba pagar nada; el activo ya existe. En MMLTI1, el 100% de la inversión depende de la solvencia financiera de MultiMoney para devolver los 2 millones de dólares de capital y los intereses en el plazo de 24 meses.

### 10. ¿Cuál tiene mayor riesgo de censura o bloqueo de fondos?
**R:** MMLTI1 tiene el riesgo máximo de censura. Si un emisor, una orden judicial o un error de cumplimiento ocurre, el administrador puede bloquear la billetera o confiscar los fondos on-chain. En DOGE, siempre que el usuario custodie sus llaves privadas en una billetera no custodial, ninguna entidad puede bloquear sus fondos en la cadena.

---

## 9. LIMITACIONES DE LA INVESTIGACIÓN

1. **Código no verificado en PolygonScan:** Al no estar publicado el código Solidity original en el explorador oficial, la auditoría del smart contract se basó en el desmontaje de bytecode y resolución de selectores de la EVM, corroborada con las especificaciones del estándar ERC-3643 de Tokeny y los documentos legales.
2. **Ausencia de transacciones públicas en mainnet:** El contrato desplegado en Polygon registra cero transacciones activas de usuarios en el explorador al momento de la consulta, lo que sugiere que las operaciones comerciales de suscripción en TOHKN se gestionan internamente en bases de datos del PSAD o en billeteras custodias antes del perfeccionamiento masivo de transferencias on-chain.
3. **Documento del Aviso de Oferta Pública:** El archivo `public-offering-notice-es-mmlti1.pdf` consiste en imágenes escaneadas sin capa de texto embebida, requiriendo verificación complementaria a través del DIR y los Términos oficiales.

---

## 10. REFERENCIAS Y FUENTES CONSULTADAS

- **Página de Emisiones TOHKN:** [https://www.tohkn.com/es/issuances](https://www.tohkn.com/es/issuances)
- **Ficha Oficial de MMLTI1 en TOHKN:** [https://www.tohkn.com/es/issuances/mmlti1](https://www.tohkn.com/es/issuances/mmlti1)
- **Documento de Información Relevante (DIR) de MMLTI1:** [DIR y Anexos Oficiales](https://www.tohkn.com/assets/documents/issuances/mmlti1/dir-es-mmlti1-annexes.pdf)
- **Términos y Condiciones del Programa MMY y Primer Tramo:** [Términos y Condiciones MMLTI1](https://www.tohkn.com/assets/documents/issuances/mmlti1/terms-es-mmlti1.pdf)
- **Informe de Certificación Independiente (Armor Analytics):** [Informe de Certificación MMLTI1](https://www.tohkn.com/assets/documents/issuances/mmlti1/certification-es-mmlti1.pdf)
- **Aviso de Oferta Pública:** [Aviso de Oferta Pública MMLTI1](https://www.tohkn.com/assets/documents/issuances/mmlti1/public-offering-notice-es-mmlti1.pdf)
- **Contrato Inteligente MMLTI1 en PolygonScan:** [PolygonScan Contract 0x6682b57FA1148b3831aE8610cd6Cbe961d610329](https://polygonscan.com/address/0x6682b57FA1148b3831aE8610cd6Cbe961d610329)
- **ImplementationAuthority de MMLTI1:** [PolygonScan Address 0x387b9ced9a3e638168dbd4992d06a0b5ba6ece18](https://polygonscan.com/address/0x387b9ced9a3e638168dbd4992d06a0b5ba6ece18)
- **Registro Público de Emisiones CNAD (El Salvador):** [CNAD Emisiones](https://cnad.gob.sv/issuances/) | [CNAD Emisores](https://cnad.gob.sv/issuers/)
- **Documento de Cátedra Sesión 15 (CS031 · Tokenomics):** [Session Doc S15 Google Docs](https://docs.google.com/document/d/1nszidR2_ESJoa5iPnO0PPHR865rwhG1hi6x97PZouAM/edit)
- **Binance API Spot (DOGE/USDT):** [Binance 24hr Ticker](https://api.binance.com/api/v3/ticker/24hr?symbol=DOGEUSDT)
- **Binance Futures Data (DOGE/USDT Taker Metrics):** [Binance Taker Long/Short Ratio](https://fapi.binance.com/futures/data/takerlongshortRatio?symbol=DOGEUSDT&period=1d)
- **CoinGecko Dogecoin Data:** [CoinGecko DOGE](https://www.coingecko.com/en/coins/dogecoin)
