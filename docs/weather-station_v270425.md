# Controle de Versão - Projeto Estação Meteorológica

## Metadados da Versão
- **Versão**: 270425
- **Data**: 27/04/2025
- **Descrição**: Adiciona sensor SHT31 para monitoramento interno de temperatura e umidade no case plástico, complementando o BME280 (externo). Mantém configuração original com BME280 como sensor principal. Atualiza Lista de Componentes, requisitos, testes, e histórico. Custo ajustado (~€86,68-167,86).
- **Autor**: Grok (xAI)

## Lista de Componentes
| **Componente** | **Função Associada** | **Quantidade** | **Custo (\~€)** | **Fonte Sugerida** | **Informações Relevantes** |
| --- | --- | --- | --- | --- | --- |
| **ESP32-C3** | Todas (controle) | 1 | 2,49-7,55 | AliExpress ([link](https://nl.aliexpress.com/item/1005006170575141.html), vendedor >4,5 estrelas) | Microcontrolador, I2C, UART, GPIO, Wi-Fi (MQTT/HTTP, ESP-NOW). 3,3 V, deep sleep (\~5-10 µA). |
| **Bateria LiPo 3500 mAh** | Gerenciamento de Energia | 1 | 8-17 | AliExpress (busca: “3500mAh LiPo”) | 3,7 V, autonomia \~241-248 dias (14,1-14,5 mAh/dia). Proteção contra sobrecarga. |
| **CN3791 (MPPT)** | Gerenciamento de Energia | 1 | 3-8 | AliExpress (busca: “CN3791 MPPT”) | Carregador solar, 4,2 V saída, eficiência \~90%. |
| **TP4056** | Gerenciamento de Energia | 1 | 1-2 | AliExpress (busca: “TP4056 charger”) | Carregador USB, proteção integrada. |
| **Painel Solar 1,5-2 W** | Gerenciamento de Energia | 1 | 5-10 | AliExpress (busca: “5V 300mA solar panel”) | 5-6 V, 300-400 mA, \~1200-1600 mAh/dia (4 h sol). Testar vs. 2-3 W (\~€8-17). |
| **RTC DS3231** | Gerenciamento de Energia | 1 | 2-3 | AliExpress (busca: “DS3231 module”) | I2C, wake-up para deep sleep, bateria CR2032. |
| **INA219** | Gerenciamento de Energia (monitoramento tensão/corrente) | 1 | 2-5 | AliExpress (busca: “INA219 module”) | I2C, mede tensão (0-6 V) e corrente (0-600 mA) do painel. |
| **Anemômetro** | Velocidade do Vento, Rajadas, Temperatura Aparente | 1 | 18 | AliExpress ([link](https://www.aliexpress.com/item/1005007510911298.html)) | RS485, 5 V (via MT3608), resolução 0,1 m/s, precisão ±(0,3 + 0,03V) m/s, IP65. |
| **Conversor RS485-TTL** | Velocidade do Vento, Rajadas, Temperatura Aparente | 1 | 2-3 | AliExpress (busca: “RS485 to TTL”) | Interface UART, 3,3 V lógica, 5 V (via MT3608). |
| **MT3608 (Boost Converter)** | Velocidade do Vento, Rajadas, Qualidade do Ar, Temperatura Aparente | 1 | 1-2 | AliExpress (busca: “MT3608 boost”) | 3,7 V → 5 V, \~2 A máx., alimenta anemômetro, RS485-TTL, PMS5003. |
| **BME280** | Temperatura, Umidade, Pressão, Temperatura Aparente | 1 | 3-8 | AliExpress (busca: “BME280 module”) | I2C (0x76/0x77), 3,3 V, ±0,5°C, ±3%, ±1 hPa, IP67 com abrigo. |
| **SHT31** | Temperatura, Umidade (interno) | 1 | 3-5 | AliExpress ([link](https://www.aliexpress.com/item/1005006781627853.html)) | I2C (0x44/0x45), 3,3 V, ±0,2°C, ±2%, case plástico, ~0,8 mA ativo, ~0,6 µA standby. |
| **SI1145 (Adafruit 1777)** | Radiação Solar, Índice UV | 1 | 8-17 | AliExpress (busca: “SI1145 sensor”), Mouser, DigiKey | I2C (0x60), 3,3 V, cúpula UV-resistente, ±10% (radiação), ±5% (UV). Alertas Wi-Fi para UV ≥7. |
| **Misol Pluviômetro** | Precipitação | 1 | 8-25 | AliExpress ([link](https://nl.aliexpress.com/item/1005006457407759.html), vendedor >4,5 estrelas) | Báscula, 0,28 mm, ±10%, pulsos (GPIO), IP65, filtro anti-detritos. |
| **PMS5003** | Qualidade do Ar (PM2.5) | 1 | 8-17 | AliExpress (busca: “PMS5003 air quality”) | UART, 5 V (via MT3608), 0-500 µg/m³, ±15 µg/m³, ventoinha, IP65. |
| **Abrigo Meteorológico** | Temperatura, Umidade, Pressão, Temperatura Aparente | 1 | 8-12 | AliExpress ([link](https://nl.aliexpress.com/item/1005005459581452.html)) | Ventilado, IP67, evita exposição solar. Dimensões: \~160 mm (altura) x 110 mm (diâmetro). DIY (PVC/3D) viável. |
| **Mastro (2 m)** | Velocidade do Vento, Rajadas, Precipitação, Temperatura Aparente | 1 | 3-8 | AliExpress (busca: “2m pole mount”) | PVC/metal, local aberto. |
| **Caixa IP65 (Eletrônica)** | Gerenciamento de Energia, Qualidade do Ar, Velocidade do Vento | 1 | 5,19-8,50 | AliExpress ([link](https://nl.aliexpress.com/item/1005005691489549.html)) | Protege ESP32-C3, MT3608, RS485-TTL, PMS5003, INA219, SHT31 (entrada de ar). Dimensões internas: \~65 x 95 x 55 mm; externas: \~80 x 130 x 70 mm. |
| **Cúpula Transparente** | Radiação Solar, Índice UV | 1 | 2-3 | AliExpress (busca: “UV acrylic dome”) | UV-resistente, exposição solar. |
| **Cabo RJ11/4 fios** | Velocidade do Vento, Rajadas, Precipitação, Temperatura Aparente | 2 | 1-2 | AliExpress (busca: “RJ11 cable”) | Conexão anemômetro (1) e pluviômetro (1). Comprimento \~1-2 m cada. |
| **Cabo UART** | Qualidade do Ar | 1 | 1 | AliExpress (busca: “UART cable”) | Conexão PMS5003, \~0,5-1 m. |
| **Filtro HEPA (Opcional)** | Qualidade do Ar | 1 | 2-3 | AliExpress (busca: “HEPA filter small”) | Protege PMS5003 contra poeira. Opcional, substituição periódica. |

**Custo Total Estimado**: \~€86,68-167,86 (excluindo resistores, varia com frete/impostos).

## Requisitos e Especificações
### Funções
- **Velocidade do Vento e Rajadas**: Anemômetro RS485 (0,1 m/s, ±(0,3 + 0,03V) m/s), UART (GPIO 7, 6).
- **Radiação Solar e Índice UV**: SI1145 (I2C, 0x60, ±10% radiação, ±5% UV), alertas Wi-Fi para UV ≥7, amostragem 6h-18h.
- **Precipitação**: Misol Pluviômetro (0,28 mm, ±10%), pulsos (GPIO 10).
- **Temperatura, Umidade, Pressão**: BME280 (I2C, 0x76/0x77, ±0,5°C, ±3%, ±1 hPa), modo forçado, alertas seletivos.
- **Temperatura, Umidade (Interno)**: SHT31 (I2C, 0x44/0x45, ±0,2°C, ±2%), modo forçado, monitoramento no case plástico.
- **Temperatura Aparente**: Calculada com BME280 (temperatura, umidade) e anemômetro (vento).
- **Qualidade do Ar (PM2.5)**: PMS5003 (UART, GPIO 20, 21, 0-500 µg/m³, ±15 µg/m³), média móvel.
- **Gerenciamento de Energia**: Bateria LiPo 3500 mAh, CN3791 (MPPT), TP4056 (USB), painel solar 1,5-2 W (~1200-1600 mAh/dia, 4 h sol), RTC DS3231 (I2C), INA219 (I2C, 0-6 V, 0-600 mA), deep sleep 15 min.

### Microcontrolador
- **ESP32-C3**:
  - Pinos Usados (8): I2C (GPIO 8, 9: BME280, SHT31, SI1145, RTC, INA219), UART (GPIO 7, 6: anemômetro; GPIO 20, 21: PMS5003), GPIO (GPIO 10: pluviômetro), ADC (GPIO 2: divisor de tensão).
  - Pinos Livres (~7-9): GPIO 0, 1, 3, 4, 5; ADC1: GPIO 0, 1, 3, 4.
  - Wi-Fi: MQTT/HTTP para dados, ESP-NOW para redes locais.
  - Deep Sleep: ~5-10 µA, ciclos de 15 min.

### Consumo e Autonomia
- Consumo: ~14,1-14,5 mAh/dia (ESP32-C3, sensores, Wi-Fi, incluindo SHT31 ~0,8 mA ativo, ~0,6 µA standby).
- Autonomia: ~241-248 dias (bateria LiPo 3500 mAh).
- Recarga: Painel solar 1,5-2 W (~300-400 mA, 5-6 V), CN3791 (MPPT, ~90% eficiência).

### Dimensões
- **PCB**: ~50 x 40 mm (ESP32-C3, MT3608, RS485-TTL, INA219, CN3791, TP4056, RTC, SHT31).
- **Caixa IP65 (Eletrônica)**: Internas ~65 x 95 x 55 mm, externas ~80 x 130 x 70 mm (ESP32-C3, PMS5003, bateria, SHT31, conexões).
- **Case Plástico (SHT31)**: ~100 x 60 x 25 mm, IP55, furos para ventilação.
- **Abrigo Meteorológico**: ~160 mm (altura) x 110 mm (diâmetro) (BME280).
- **Outros**: Mastro ~2 m, cúpula transparente (~50-100 mm diâmetro), pluviômetro (~150 x 100 mm), anemômetro (~200 x 150 mm).

### Otimizações
- **SI1145**: Alertas UV ≥7, amostragem 6h-18h (economia de energia).
- **BME280**: Modo forçado, alertas seletivos (ex.: temperatura <0°C, umidade >90%).
- **SHT31**: Modo forçado, monitoramento interno, comparado com BME280.
- **PMS5003**: Monitoramento contínuo, média móvel para PM2.5.
- **MT3608**: Único boost converter (3,7 V → 5 V) para anemômetro, RS485-TTL, PMS5003.
- **ESP-NOW**: Comunicação local eficiente.
- **Amostragem Adaptativa**: Vento e precipitação ajustados por condições (ex.: rajadas, chuva intensa).
- **Deep Sleep**: 15 min, Wi-Fi ativo ~2 s/ciclo.
- **Painel Solar**: 1,5-2 W, otimizado para ~4 h sol/dia (Amsterdam).

## Testes
### Validação de Componentes
- **Pinos do ESP32-C3**: Testar conflitos (ex.: Wi-Fi vs. ADC), validar I2C (GPIO 8, 9: BME280, SHT31, SI1145, RTC, INA219), UART (GPIO 7, 6, 20, 21), GPIO (GPIO 10), ADC (GPIO 2).
- **BME280**: Comparar temperatura (±0,5°C), umidade (±3%), pressão (±1 hPa) com KNMI (Schiphol).
- **SHT31**: Comparar temperatura (±0,2°C), umidade (±2%) com BME280 e KNMI (Schiphol). Validar no case plástico (ventilação).
- **SI1145**: Validar radiação (±10%), UV (±5%) com referências (ex.: KNMI UV index).
- **PMS5003**: Comparar PM2.5 (±15 µg/m³) com RIVM (Vondelpark).
- **Anemômetro**: Validar velocidade (0,1 m/s, ±(0,3 + 0,03V) m/s) e rajadas com KNMI.
- **Pluviômetro**: Testar pulsos (0,28 mm, ±10%) com chuva simulada ou KNMI.
- **Energia**: Medir tensão/corrente (INA219, multímetro), confirmar ~14,1-14,5 mAh/dia, autonomia ~241-248 dias.

### Testes de Campo
- **Local**: Amsterdam (jardim, local aberto, sem superfícies refletoras).
- **Condições**: Rajadas (até 40 m/s), PM2.5 (10-100 µg/m³), UV (0-10), chuva (~800 mm/ano), -10°C a 35°C.
- **Validações**:
  - Estanqueidade (IP65/IP67): Caixa IP65 e sensores (anemômetro, pluviômetro, BME280, SI1145) em chuva simulada/real.
  - Ventilação do Abrigo: Temperatura do BME280 vs. termômetro externo (sem aquecimento solar, ~5-10°C de erro).
  - Ventilação do Case Plástico: Temperatura e umidade do SHT31 vs. BME280 (sem condensação).
  - Wi-Fi: Conexão MQTT/HTTP, ESP-NOW, latência <5 s, alcance ~50 m.
  - Energia: Consumo (multímetro), recarga solar (~1200-1600 mAh/dia, 4 h sol).

### Testes de Software
- **Bibliotecas**: Confirmar compatibilidade (Arduino/ESP-IDF) para BME280, SHT31, SI1145, PMS5003, DS3231, INA219.
- **Alertas**: Testar Wi-Fi para UV ≥7, temperatura <0°C, umidade >90%, PM2.5 >50 µg/m³, bateria <3,4 V.
- **Deep Sleep**: Validar ciclos de 15 min, consumo ~5-10 µA (ESP32-C3, incluindo SHT31).

## Histórico de Mudanças
- **Versão Inicial (Pré-170425)**:
  - Definição do projeto com ESP32-C3, funções: Velocidade do Vento e Rajadas, Radiação Solar e Índice UV, Precipitação, Temperatura, Umidade e Pressão, Temperatura Aparente, Qualidade do Ar (PM2.5), Gerenciamento de Energia.
  - Lista de Componentes inicial: ~€76,49-154,55, sem quantidades.
  - Pinos: 8 usados (GPIO 8, 9, 7, 6, 20, 21, 10, 2), ~7-9 livres.
  - Consumo: ~14,1-14,5 mAh/dia, autonomia ~241-248 dias.
- **Alteração 1: Cancelamento da Direção do Vento**:
  - Revertido anemômetro com direção (~€18-25) para anemômetro original (~€18, RS485, sem direção).
  - Custo ajustado para ~€76,49-154,55, consumo ~14,1-14,5 mAh/dia.
  - Motivo: Solicitação do usuário para manter configuração anterior.
- **Alteração 2: Adição de Quantidades**:
  - Incluída coluna **Quantidade** na Lista de Componentes (ex.: 1 para maioria, 2 para Cabo RJ11, 1 opcional para Filtro HEPA).
  - Custo mantido (~€76,49-154,55).
- **Alteração 3: Dimensões de Abrigo e Caixa IP65**:
  - **Abrigo Meteorológico**: Adicionado ~150-200 mm (altura) x 100-150 mm (diâmetro).
  - **Caixa IP65**: Adicionado ~80 x 60 x 40 mm.
  - Detalhes de utilização e necessidade (proteção do BME280, eletrônicos).
- **Alteração 4: Validação de Novas Alternativas**:
  - **Abrigo**: Confirmado item ([link](https://nl.aliexpress.com/item/1005005459581452.html), ~€8-12, ~160 x 110 mm), substituindo ~€3-8, ~150-200 mm x 100-150 mm.
  - **Caixa IP65** (1ª tentativa): Analisada alternativa (~75 x 58 x 35 mm, ~€3,17-4,12), viável, mas espaço restrito.
  - **Caixa IP65** (2ª tentativa): Confirmada nova alternativa ([link](https://nl.aliexpress.com/item/1005005691489549.html), ~€5,19-8,50, ~65 x 95 x 55 mm internas, ~80 x 130 x 70 mm externas), substituindo ~€3-8, ~80 x 60 x 40 mm.
- **Versão 170425 (17/04/2025)**:
  - Consolidação de todas as alterações.
  - Lista de Componentes atualizada: ~€83,68-162,86.
  - Inclusão de controle de versão com requisitos, testes, e histórico.
- **Versão 270425 (27/04/2025)**:
  - Adição do sensor SHT31 para monitoramento interno de temperatura e umidade no case plástico (~100 x 60 x 25 mm, IP55).
  - Atualização da Lista de Componentes: Inclui SHT31 (~€3-5, I2C 0x44/0x45, ±0,2°C, ±2%).
  - Requisitos: Adiciona SHT31 (I2C, modo forçado, sem conflitos com BME280).
  - Testes: Inclui validação do SHT31 vs. BME280 e KNMI (Schiphol).
  - Custo ajustado: ~€86,68-167,86.

## Checklist de Validação
- [ ] **Componentes**: Todos os componentes adquiridos (verificar links, vendedores >4,5 estrelas, >100 vendas).
- [ ] **Pinos**: Validados sem conflitos (I2C, UART, GPIO, ADC).
- [ ] **Consumo**: Confirmado ~14,1-14,5 mAh/dia (multímetro).
- [ ] **Autonomia**: Testada ~241-248 dias (bateria 3500 mAh).
- [ ] **IP65/IP67**: Estanqueidade confirmada (Caixa IP65, anemômetro, pluviômetro, BME280, SI1145).
- [ ] **Ventilação**: Abrigo testado (BME280 sem aquecimento solar). Case plástico testado (SHT31 sem condensação).
- [ ] **Calibração**: Comparada com KNMI (Schiphol), RIVM (Vondelpark).
- [ ] **Wi-Fi**: MQTT/HTTP, ESP-NOW funcionando (latência <5 s, alcance ~50 m).
- [ ] **Montagem**: PCB (~50 x 40 mm), Caixa IP65 (~65 x 95 x 55 mm internas), Abrigo (~160 x 110 mm), Case plástico (~100 x 60 x 25 mm) validados.
- [ ] **Testes de Campo**: Concluídos em Amsterdam (rajadas, PM2.5, UV, chuva).

## Notas
- **Estado Atual**: Projeto otimizado, com Lista de Componentes consolidada, incluindo SHT31 para monitoramento interno. Requisitos e testes atualizados. Pronto para aquisição (~€86,68-167,86), montagem (PCB ~50 x 40 mm, Caixa IP65, Abrigo, Case plástico), e testes (Amsterdam, KNMI/RIVM).
- **Próximos Passos**:
  - **Compras**: Adquirir SHT31 ([link](https://www.aliexpress.com/item/1005006781627853.html), ~€3-5) e componentes pendentes (priorizar AliExpress, vendedores >4,5 estrelas). Verificar frete (~€10-20) e impostos (~20-40%, UE) via [internationalparceltracking.com](http://internationalparceltracking.com).
  - **Montagem**: Prototipar com ESP32-C3 (GPIO 8, 9, 7, 6, 20, 21, 10, 2), integrar BME280 (Abrigo), SHT31 (Case plástico), PMS5003 (Caixa IP65), e sensores externos (anemômetro, pluviômetro, SI1145).
  - **Testes**: Validar pinos, consumo, IP65/IP67, ventilação (Abrigo e Case), Wi-Fi, e calibração (BME280 e SHT31 vs. KNMI).
  - **Documentação**: Manter esquemático, salvar links de fornecedores, registrar resultados de testes.
