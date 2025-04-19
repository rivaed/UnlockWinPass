
# UnlockWinPass

## Descrição  
Método manual de redefinição de senha no Windows 10/11 via substituição do **Utilman.exe** pelo **Cmd.exe**, sem uso de scripts.  

---

## Pré‑requisitos  
- Acesso físico ao equipamento.  
- Mídia de instalação do Windows 10/11 ou acesso ao WinRE (Ambiente de Recuperação).  
- Permissões de administrador no ambiente de recuperação.

---

## Passo a Passo (sem scripts)

### 1. Acesse o Modo de Recuperação  
1. Na tela de login, segure **Shift** e clique em **Reiniciar**.  
2. Selecione **Solução de Problemas** > **Opções Avançadas** > **Prompt de Comando**.  

### 2. Identifique a Unidade do Sistema  
No prompt, teste qual letra corresponde ao Windows (normalmente C: ou D:):  
```bat
dir C:\
dir D:\
```  
Quando encontrar pastas como `Windows`, digite:
```bat
C:
```
(substitua por D: se for o caso)

### 3. Navegue até o System32  
```bat
cd \Windows\System32
```

### 4. Faça backup e substitua o utilman.exe  
```bat
ren utilman.exe utilman_backup.exe
ren cmd.exe    utilman.exe
```

### 5. Reinicie normalmente  
```bat
exit
```
— Na tela de login, clique no ícone **Facilidade de Acesso**.  
— Será aberto um **Prompt de Comando** com privilégios de **SYSTEM**.

### 6. Redefina a senha  
Opção A – via net user:  
```bat
net user <NomeDoUsuário> <NovaSenha>
```  
Opção B – via interface gráfica:  
```bat
control userpasswords2
```  
Selecione a conta, clique em **Redefinir Senha**, informe a nova senha e confirme.

### 7. Restaure o utilman.exe original  
1. Repita **Passos 1 e 3** para abrir o Prompt de Comando no WinRE.  
2. Novamente em `C:\Windows\System32`, execute:  
   ```bat
   ren utilman.exe cmd.exe
   ren utilman_backup.exe utilman.exe
   ```
3. Reinicie normalmente.

---

## Considerações de Segurança  
- Use somente em máquinas autorizadas.  
- Sempre restaure o backup para não deixar a brecha de segurança aberta.  
- Documente datas e responsáveis pelo procedimento.

---

## Licença  
MIT License – consulte o arquivo `LICENSE` para detalhes.  
