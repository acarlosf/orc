# ORC — Orçamentação de Sistemas de Segurança

Aplicação web single-page (SPA) para geração de orçamentos internos de instalação de sistemas de segurança contra incêndio e proteção de vãos. Sem backend, sem dependências externas — corre inteiramente no browser.

## Funcionalidades

- **Cálculo automático de Mão de Obra** por sistema (montagem + instalação + enfiamento + ensaios)
- **Insumos por sistema** (cabos, tubos VD, calhas, ISOGRIS) com preços editáveis
- **Trabalhos Adicionais** livres por sistema (nome, unidade, tempo de execução, quantidade, preço)
- **Email de orçamento** gerado com M.O. e insumos detalhados por sistema
- **Persistência** via `localStorage` — os dados mantêm-se ao fechar o browser

## Sistemas suportados

| Sistema | Descrição |
|---|---|
| **SADI** | Deteção Automática de Incêndio |
| **SAIE** | Iluminação de Emergência |
| **SINAL Emergência** | Sinais de saída e vias de evacuação (verdes) |
| **SINAL Incêndio** | Sinais de equipamentos e sistemas (vermelhos) |
| **Extinção** | Extintores portáteis e agulhetas |
| **SPV** | Sistema de Proteção de Vão (molas, fechaduras, barras antipânico) |
| **Desenfumagem** | Controlo de extração de fumo (dampers, motores, botões) |
| **Deteção de Gás** | Gás natural e butano/propano com electroválvula |
| **Deteção de CO** | Monóxido de carbono |
| **Ajax Sem Fio** | Central Ajax Hub, FireProtect, sirenes sem fio |

## Como usar

Abrir `index.html` diretamente no browser — não é necessário servidor.

1. Preencher quantidades de equipamentos em cada sistema
2. Expandir **Cabos e Insumos** para adicionar metros de cabo, tubos VD, calhas ou ISOGRIS
3. Expandir **Trabalhos Adicionais** para itens não tabelados
4. Ajustar **€/hora equipa** e **Extra (%)** na barra de configuração
5. Clicar **⚡ Gerar Email** — o texto fica pronto a colar

## Lógica de cálculo

- **Montagem**: tempo tabelado por tipo de equipamento × quantidade × fator altura (≤3 m / >3 m)
- **Instalação**: fixação de bases, ligações, colocação de detetores, ensaios (em segundos por equipamento)
- **Enfiamento**: 90 s/m de cabo, ativado automaticamente quando há metros de tubo VD, calha ou ISOGRIS no sistema
- **Passagem VD**: 450 s/m de tubo/calha/ISOGRIS
- **M.O. total** = (horas montagem + horas instalação) × €/hora × (1 + extra%)
- **Insumos** = custo de cabos + tubos + calhas + materiais livres

## Ficheiros

| Ficheiro | Descrição |
|---|---|
| `index.html` | Aplicação completa (HTML + CSS + JS numa só página) |
| `index.html.bak` | Cópia de segurança anterior ao refactor por sistema |
