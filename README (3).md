
# 🔐 Habilitar Encryption Oracle e Configurar CredSSP no Windows

Este guia ensina a habilitar o **Encryption Oracle** e configurar manualmente o valor `AllowEncryptionOracle` no Registro do Windows para resolver problemas de autenticação RDP relacionados ao CredSSP.

Também inclui uma alternativa usando **Política de Grupo Local (gpedit.msc)**.

---

# 🧩 1. Habilitar o Oráculo de Criptografia (CredSSP) via Política de Grupo

1. Pressione **Win + R** e digite:
   ```
   gpedit.msc
   ```
2. Navegue até:

   ```
   Configuração do Computador
     └ Modelos Administrativos
         └ Sistema
             └ Delegação de Credenciais
   ```

3. Localize e abra a política:

   **Correção do Oráculo de Criptografia**

4. Configure como:
   - **Habilitado**
   - Nível de proteção: **Vulnerável** (ou conforme sua necessidade)

5. Clique em **Aplicar** e **OK**.

### 📸 Captura de Tela
![Editor de Registro](images/editor%20de%20registro.png)

---

# 🛠️ 2. Alterar Diretamente no Registro (regedit)

### ⚠️ Aviso
Modificar o Registro pode afetar o sistema. Faça com cuidado.

---

## 📍 Passo a Passo – Regedit

1. Pressione **Win + R** e digite:
   ```
   regedit
   ```

2. Navegue até o caminho:

   ```
   HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System\CredSSP\Parameters
   ```

3. Crie ou edite o valor **DWORD (32 bits)**:

   - **Nome:** `AllowEncryptionOracle`
   - **Tipo:** `DWORD`
   - **Valor:** conforme tabela abaixo:

### 🔧 Valores possíveis:
| Valor | Modo | Descrição |
|-------|-------------|-----------|
| `2` | **Vulnerável** | Permite conexões inseguras. Usado para compatibilidade. |
| `1` | **Mitigado** | Nível intermediário de segurança. |
| `0` | **Forçado** | Mais seguro, bloqueia conexões incompatíveis. |

4. Clique em **OK**.

5. **Reinicie o computador**.

### 📸 Captura de Tela
![Habilitar Oráculo](images/habilitar%20oraculo.png)

---

# ✅ Conclusão

Após seguir um dos métodos acima, o problema de conexão via RDP relacionado ao CredSSP deve ser resolvido.

Você pode optar por:
- **Política de Grupo** (GPEDIT) → mais organizado e gerenciável.
- **Registro do Windows** → mais rápido e direto.

Ambas as opções funcionam.

---
