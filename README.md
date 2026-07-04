# Zolana.gg / Zenko Auto-Farmer Bot & Suite 🚀

![Zolana Auto-Farmer Bot Banner](github_banner.png)

Uma suíte de automação multithread e verificação criptográfica para o jogo Web3 **Zolana.gg (Zenko)** na blockchain Solana. Esta ferramenta foi construída com foco em resiliência de execução prolongada, latência mínima nas ações e evasão de heurísticas de detecção de sistemas anti-cheat (OpSec).

---

## 🌟 Principais Recursos

* **Farm Inteligente e Concorrente (`farm.py`):** Gerencia múltiplas contas concorrentemente (multithread) com pool de sessões HTTP persistentes (`requests.Session` Keep-Alive) para otimizar o tempo de resposta das requisições de dungeons e claims.
* **Restauração de Stamina On-chain Real:** Automatiza o fluxo de pagamento da Solana blockchain. Transfere **50 ZOLANA (Token-2022)** para a tesouraria oficial do jogo, monitora a confirmação na rede e valida a transação enviando a assinatura para o backend do jogo.
* **Derivação Determinística de ATA:** Calcula localmente as Associated Token Accounts (ATA) de ZOLANA de cada jogador via curva elíptica da Solana, eliminando chamadas repetitivas de rede à RPC.
* **Heurísticas Humanizadas (OpSec):** Aplica tempos de espera dinâmicos e variações aleatórias (Gaussianas/Random) antes de iniciar dungeons, evoluir criaturas e reivindicar recompensas, simulando a interação humana.
* **Descanso Inteligente (Campfire):** Detecta stamina baixa e coloca as criaturas no modo repouso na fogueira da AFK Zone, dobrando a regeneração passiva de stamina de forma automatizada.
* **Mecanismo Provably Fair & Simulador (`verificador_fairness.py`):** 
  * Audita a integridade criptográfica das sementes de chocagem (Server/Client Seed) via SHA-256 para garantir que o jogo não alterou os resultados.
  * Realiza simulações de chocagem (Monte Carlo) mapeando a taxa de drops de Shinies, Lendários, Míticos e o impacto do sistema de Pity acumulativo.
* **Zenko Helper HUD (`zenko_helper.user.js`):** Script de usuário Tampermonkey de edição avançada que injeta um HUD flutuante no jogo via Shadow DOM para interceptar tokens de sessão e monitorar estatísticas do jogador de forma transparente.

---

## 🛠️ Requisitos e Instalação

O projeto está estruturado para utilizar uma pasta de interpretador Python embarcado local (`Tools/python_embeded`) para evitar conflitos de variáveis de ambiente globais.

### Dependências Utilizadas

| Biblioteca | Finalidade |
| :--- | :--- |
| `requests` | Requisições HTTP robustas com persistência de conexões |
| `base58` | Codificação e decodificação de chaves públicas/privadas Solana |
| `pynacl` | Criptografia NaCl para assinaturas de segurança local |
| `solders` | Binding Rust-Python de alta performance para interações na Solana |
| `pyttsx3` | Notificação por voz TTS (Text-to-Speech) em caso de eventos importantes |

Você pode instalar as dependências de forma simplificada no interpretador local utilizando o painel central:
```bash
control_panel.bat
```
Ou manualmente no console do terminal de desenvolvimento:
```bash
Tools\python_embeded\python.exe -m pip install requests base58 pynacl solders pyttsx3
```

---

## ⚙️ Como Configurar

Crie ou edite o arquivo `wallets.json` no diretório raiz do projeto para cadastrar suas contas:

```json
{
    "conta1": {
        "wallet": "Endereço_Público_da_Carteira_Solana",
        "token": "Token_x-zenko-session_interceptado_pelo_Helper",
        "private_key": "Chave_Privada_Solana_Hex_Base58_ou_Array_Bytes"
    }
}
```

> [!TIP]
> **Como pegar o Token de Sessão:** Ative o script `zenko_helper.user.js` no Tampermonkey, faça login no site oficial `https://play.zolana.gg` e copie o token interceptado que aparecerá no menu HUD flutuante no topo direito do navegador.

---

## 🚀 Como Executar

A suíte possui um menu interativo facilitador. Inicie o painel executando:
```bash
control_panel.bat
```

Você também pode iniciar os scripts diretamente utilizando o Python local:

1. **Iniciar Bot de Farm:**
   ```bash
   Tools\python_embeded\python.exe farm.py
   ```
2. **Validar wallets.json e chaves:**
   ```bash
   Tools\python_embeded\python.exe validar_config.py
   ```
3. **Rodar Diagnóstico de Stamina:**
   ```bash
   Tools\python_embeded\python.exe diagnostico_restore.py
   ```
4. **Executar Auditor de Drop/Gacha:**
   ```bash
   Tools\python_embeded\python.exe verificador_fairness.py
   ```
