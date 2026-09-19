# ARENA — o console da turma 🎮

![Status](https://github.com/DAVI3DS/ARENA-remake-/actions/workflows/status/badge.svg)
![Tamanho](https://img.shields.io/github/repo-size/DAVI3DS/ARENA-remake-)
![Linguagem](https://img.shields.io/badge/python-3.11-blue)
![Plataforma](https://img.shields.io/badge/windows-10%2B-lightgray)

> Copie a pasta, dê dois cliques e jogue. Não instala nada.

**ARENA** é um console retro portátil auto-contido: todos os jogos, emuladores, saves, recordes e configurações ficam dentro de uma única pasta. Copie a pasta para um pen drive USB, dê dois cliques em `ARENA.bat` e o navegador abre a interface de jogos.

## 🎯 O que é

- **47 consoles emulados**: NES, SNES, PlayStation 1/2, N64, GBA, Arcade, Mega Drive, Master System, Game Gear, PSP, Wii, Gamecube e muito mais
- **Sem instalação**: Python embutido na pasta, sem `pip install`, sem internet
- **Portátil**: Copie a pasta para qualquer lugar. Todos os dados viajam com você
- **Privacidade**: Apenas apelido. Sem nome completo, sem gravação de vídeo
- **Multi-jogador**: Mesmo Wi-Fi, cabo direto, notebook ou sem rede (pen drive)

## 📋 Pré-requisitos

| Componente | O que é | Onde encontrar |
|---|---|---|
| **Python embutido** | Interpretador Python standalone | `servidor/python/python.exe` (python 3.13) |
| **RetroArch** | Frontend de emulação | `retroarch/retroarch.exe` + cores (`.dll`) |
| **Navegador** | Para abrir a interface web | Edge/Chrome qualquer (já instalado) |
| **Jogos** | ROMs dos consoles que você quer | Coloque em `jogos/{livres,turma,pessoais}/{console}/` |

O Python embutido e o RetroArch **não** são incluídos neste repositório por questões de tamanho e licença. Veja a seção [Instalação](#instalação) para como preparar.

## 🚀 Instalação rápida

### 1. Prepare a pasta ARENA

```
ARENA/
├── ARENA.bat                    # Entrada de execução
├── LEIA-ME.md                   # Este arquivo
├── 1-COMECAR.md                 # Guia completo de preparação
├── servidor/                    # Código Python do servidor
│   ├── arena.py                 # Servidor HTTP principal
│   ├── controles.py             # Mapeamento de controles
│   ├── hardware.py              # Detecção de capacidade da máquina
│   ├── graficos.py              # Configuração de imagem
│   ├── cheats.py                # Cheats e save states
│   ├── db.py                    # SQLite (recordes e sessões)
│   └── ...
├── launcher/                    # Interface web (HTML/CSS/JS)
│   ├── index.html               # UI da interface
│   ├── app.js                   # Lógica da interface
│   └── estilo.css               # Estilo
├── jogos/                       # Suas ROMs (não commitadas)
│   ├── livres/                  # Domínio público / homebrew
│   ├── turma/                   # Jogos da turma
│   └── pessoais/                # Jogos pessoais
├── retroarch/                   # RetroArch + cores (não commitado)
│   └── retroarch.exe
└── dados/                       # Saves, recordes, configurações (não commitado)
```

### 2. Adicione o Python embutido

Baixe o [Python embeddable package](https://www.python.org/downloads/) (versão 3.11 ou 3.13) e extraia para `servidor/python/`. Ou use o já incluso se você tem a pasta completa.

### 3. Adicione o RetroArch

Baixe o [RetroArch](https://www.retroarch.com/) para Windows e extraia para `retroarch/`. O arquivo principal deve ser `retroarch.exe`. Os cores (`.dll`) ficam na mesma pasta ou em subpastas.

### 4. Coloque os jogos

Crie as pastas dos consoles dentro de `jogos/` e coloque as ROMs:

```
jogos/livres/nes/Mario.nes
jogos/livres/snes/SuperMario.sf7
jogos/turma/psx/FinalFantasy.iso
```

Cada console tem uma pasta com o nome do sistema (ex: `nes`, `snes`, `psx`, `n64`, `gba`, `arcade`, etc.).

### 5. Execute

Dê dois cliques em `ARENA.bat`. A janela preta abre — **não a feche**. Seu navegador abrirá automaticamente com a interface ARENA.

## 🎮 Como usar

1. **Escreva seu apelido** no campo "Jogando como" na parte superior
2. **Clique em "Criar pastas dos consoles"** para criar a estrutura
3. **Atualize a lista** para ver os jogos disponíveis
4. **Clique em um jogo** para abrir
5. **F10** fecha o jogo. **Esc** abre o menu (save, cheats, configurações)
6. Para desligar o ARENA, feche a janela preta

### Configuração de controles

- **Controles conhecidos** (Xbox, PlayStation, Switch): clique em "Mapear meu controle sozinho" para mapear automaticamente os 16 botões em 30 segundos
- **Controles genéricos**: clique em "Configurar com assistente" para um assistente passo-a-passo que detecta cada botão quando você aperta (X, A, setas, analógicos, etc.)

### Cheats e Save States

- **Cheats**:ativosável com códigos do tipo GameShark/Action Replay
- **Save States**: 10 slots (`.state0` a `.state9`) para salvar e carregar o estado exato do jogo

## 📁 Estrutura de diretórios

```
ARENA/
├── servidor/              # Backend Python (stdlib-only)
│   ├── arena.py           # Servidor HTTP (port 8777, ~25 endpoints)
│   ├── db.py              # SQLite + placar + sessão
│   ├── indexador.py       # Indexa jogos nas pastas
│   ├── hardware.py        # Detecta CPU, RAM, GPU, disco
│   ├── controles.py       # Mapeia controles para RetroArch
│   ├── cheats.py          # Gerencia cheats e save states
│   ├── graficos.py        # Gera retroarch-core-options.cfg
│   ├── acervo.py          # Manifesto de jogos autorizados
│   ├── diagnostico.py     # Verifica saúde do sistema
│   ├── transferencia.py   # Sincronização entre ARENAs
│   └── tests/             # Suite de testes (unittest, 44 testes)
├── launcher/              # Frontend web
│   ├── index.html         # Tela principal
│   ├── app.js             # Lógica JS (controles, jogos, menu)
│   └── estilo.css         # Estilo dark theme
├── jogos/                 # ROMs (não commitado no repo)
│   ├── livres/            # Domínio público / homebrew
│   ├── turma/             # Jogos compartilhados da turma
│   └── pessoais/          # Jogos pessoais
├── retroarch/             # RetroArch + cores (não commitado)
├── dados/                 # Saves, recordes, configurações (não commitado)
└── emuladores/            # Emuladores externos (Dolphin, PCSX2, etc.)
```

## 🛠️ Desenvolvimento

### Executando os testes

```bash
python servidor/tests/run.py
```

Suite com 44 testes usando `unittest` (stdlib). Cada teste cria seus próprios arquivos temporários.

### Diagnóstico

```bash
python servidor/diagnostico.py --tudo
```

Verifica: Python, RetroArch, drivers, disco, GPU, configurações, integridade do banco.

### Arquivos importantes

- `servidor/consoles.json` — Catálogo dos 47 consoles com extensões, perfis, emuladores externos
- `servidor/perfis_controle.json` — Mapeamentos de controles por tipo (Xbox, PlayStation, etc.)
- `servidor/graficos.json` — Configurações de imagem por núcleo emulador
- `servidor/recursos.json` — Recursos habilitados (cheats, netplay, etc.)

## 📄 Documentação completa

| Arquivo | Conteúdo |
|---|---|
| `LEIA-ME.md` | Visão geral e(primeiros passos |
| `1-COMECAR.md` | Preparação da mídia e instalação completa |
| `2-JOGOS.md` | Como organizar os jogos por console |
| `3-IMAGEM-SOM-CONTROLE.md` | Configuração avançada de imagem, som e controles |
| `4-SAVES.md` | Save states, load states, gerenciamento |
| `5-AMIGOS.md` | Rede, descoberta de amigos, netplay |
| `6-RECURSOS-E-REPARO.md` | Recursos avançados, troubleshooting |

## 🔒 Segurança e privacidade

- **Dados minimos**: Apenas apelido (nickname), nunca nome completo
- **Sem gravação**: Configuração explícita para não gravar vídeo/audio (razão escolar/LGPD)
- **Atomic writes**: Todo arquivo crítico é escrito com arquivo temporário + `os.replace` (survive USB removal)
- **Input validation**: Todos os endpoints API validam entrada (tamanho, tipo, conteúdo)
- **Sem pip**: Stdlib Python apenas — sem dependências externas, sem risco de supply chain

## ⚖️ Licença

Este projeto é distribuído como software prático para uso educacional e doméstico. Os emuladores e cores incluídos seguem suas próprias licenças. As ROMs não são incluídas — você deve prover suas próprias cópias legais de jogos que você possui.

## 🤝 Contribuindo

1. Fork o repositório
2. Crie uma branch (`git checkout -b feature/nova-funcionalidade`)
3. Faça suas mudanças
4. Adicione testes se applicable
5. Commit (`git commit -m 'feat: descrição'`)
6. Push (`git push origin feature/nova-funcionalidade`)
7. Abra um Pull Request

### Guia de contribuição

- **Sem pip**: Novas dependências não são aceitas. Use stdlib Python.
- **Testes**: Novas funcionalidades devem ter testes na suite `servidor/tests/`
- **Offline-first**: Todas as funcionalidades devem funcionar sem internet
- **Portable**: Tudo deve funcionar a partir da pasta, sem instalação

## 🐛 Solução de problemas

Veja `6-RECURSOS-E-REPARO.md` para troubleshooting completo. Alguns problemas comuns:

- **Janela preta fecha sozinha**: Verifique se `servidor/python/python.exe` existe
- **RetroArch não abre**: Verifique se `retroarch/retroarch.exe` existe e está na versão correta
- **Jogos não aparecem**: Execute "Atualizar lista" após adicionar jogos
- **Controle não funciona**: Verifique se o controle está conectado e clicado "Mapear meu controle sozinho"
- **Erro de disco**: Alguns pen drives lentos podem causar timeout. Use SSD ou HD interno.

## 🌐 GitHub Pages

A página de instalação está disponível em:

**https://davi3ds.github.io/ARENA-remake-**/

Ela inclui:
- Botão de instalação rápida
- Lista de funcionalidades
- Passo a passo de instalação
- Links para documentação completa

## 🎓 Créditos

Desenvolvido por **Jorge Luís** como projeto prático de emulação retro portátil para uso educacional e doméstico.

Icones e referências visuais inspirados em interfaces de consoles retro clássicos.

---

**Se você gosta do ARENA, considere dar uma ⭐ no repositório!**
