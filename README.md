# Projeto Estação Meteorológica

Repositório para o Projeto Estação Meteorológica, desenvolvido para monitorar condições ambientais em Amsterdam. Inclui controle de versão, documentação, código-fonte, e rastreamento de compras.

## Estrutura
- **/docs**: Documentação (controle de versão, dependências, compras).
  - `estacao_meteorologica_v170425.md`: Controle de versão (versão 170425, 17/04/2025).
  - `dependencies.md`: Bibliotecas Arduino para sensores.
  - `purchases.md`: Status de aquisição dos componentes.
- **/src**: Código-fonte (futuro, ex.: Arduino/ESP-IDF para ESP32-C3).
- **/tests**: Resultados de testes.
  - `test_log.md`: Modelo para registrar testes.

## Funcionalidades
- Velocidade do Vento e Rajadas
- Radiação Solar e Índice UV
- Precipitação
- Temperatura, Umidade e Pressão
- Temperatura Aparente
- Qualidade do Ar (PM2.5)
- Gerenciamento de Energia (solar, bateria LiPo 3500 mAh)

## Especificações
- **Microcontrolador**: ESP32-C3 (8 pinos usados, ~7-9 livres, Wi-Fi MQTT/HTTP, ESP-NOW).
- **Consumo**: ~14,1-14,5 mAh/dia.
- **Autonomia**: ~241-248 dias.
- **Custo**: ~€83,68-162,86.

## Próximos Passos
- Adquirir componentes (AliExpress, Mouser, DigiKey).
- Prototipar PCB (~50 x 40 mm), Caixa IP65 (~65 x 95 x 55 mm internas), Abrigo (~160 x 110 mm).
- Testar em Amsterdam (calibração com KNMI, RIVM).

## Contato
- Repositório mantido por [seu-usuario].
