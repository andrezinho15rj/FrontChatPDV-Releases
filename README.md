# FrontChat PDV — downloads oficiais

Este repositório reúne os instaladores compilados do FrontChat PDV. O código-fonte fica no repositório privado do FrontChat.

## Windows — 0.7.377

- [Baixar o instalador para Windows 64 bits](https://github.com/andrezinho15rj/FrontChatPDV-Releases/releases/download/v0.7.377/FrontChatPDV-Setup-0.7.377.exe)
- [Ver a publicação no GitHub](https://github.com/andrezinho15rj/FrontChatPDV-Releases/releases/tag/v0.7.377)
- [Baixar pelo site oficial](https://app2.frontchat.com.br/downloads/pdv/FrontChatPDV-Setup-0.7.377.exe)
- SHA-256: `e2cf543b6d8daeff6c361ef601493fef771457f172e4f97cce8ac178fbc6f82e`

Em um PDV que já está instalado, feche o aplicativo e execute o instalador com o mesmo usuário do Windows e na mesma pasta de instalação. Se o PDV estiver sem abrir, baixe e execute o instalador manualmente.

Em um caixa novo, abra o PDV e configure **Comunicação** com a empresa e a credencial gerada pelo Super Admin. Para verificar a impressora, instale ou emparelhe o equipamento no Windows e use **Imprimir teste**.

## Banco local corrompido no Windows

### Recuperação automática

Se o SQLite indicar corrupção na abertura, a versão 0.7.377 mostra **Recuperação do banco local** e informa o que está verificando. Se encontrar uma gravação interrompida recente e íntegra, o PDV preserva o arquivo original, restaura a cópia e tenta abrir novamente.

Se apenas um backup diário estiver disponível, o PDV verifica as cópias locais e indica o arquivo íntegro encontrado. A tela mostra a última venda e, quando disponível, a última NFC-e de produção da cópia. Use **Mostrar arquivo** para localizar o backup no Explorador.

### Onde ficam o banco e os backups

1. No usuário do Windows que opera o caixa, pressione **Win + R**.
2. Cole `%APPDATA%\frontchat-pdv-local` e pressione **Enter**.
3. O banco ativo costuma se chamar `frontchat-pdv.sqlite` ou `frontchat-pdv-company-<id>.sqlite`. Em instalações com várias empresas, confirme o arquivo da empresa ativa antes de mexer.
4. Procure na pasta `backups`. As versões atuais guardam as cópias diárias em uma subpasta por banco, com retenção das últimas 30 por banco. Cópias de versões anteriores podem estar diretamente em `backups`.

Os backups automáticos são gerados nos dias em que o PDV fica aberto. O arquivo `reparo-pdv.zip` da instalação é a cópia de reparo dos arquivos do aplicativo.

### Restauração manual

1. Feche o PDV e confirme que ele saiu. Copie a pasta de dados inteira para uma pasta de segurança. Preserve também `XML-NFCe` se ela estiver na pasta de instalação. Guarde os arquivos originais `.sqlite`, `.tmp`, `.bak` e `startup-backup` caso existam.
2. Escolha o backup mais recente que pertença ao mesmo caixa e à mesma empresa. Valide **uma cópia** com a ferramenta de suporte ou com o SQLite em modo somente leitura. Pela linha de comando, use `sqlite3 -readonly "C:\caminho\backup.sqlite" "PRAGMA integrity_check;"`. O resultado esperado é `ok`. Se falhar, teste a cópia anterior.
3. Confirme a última venda e as últimas NFC-e **gravadas dentro do backup**. Confira no histórico do terminal e nos XML guardados se existem vendas, notas autorizadas ou pendências posteriores. A data do arquivo indica quando a cópia foi feita. Se houver movimentos posteriores ou dúvida sobre a sequência fiscal, peça ao suporte para reconciliá-los antes de voltar a operar.
4. Na pasta original, renomeie o banco ativo para acrescentar `.antes-da-restauracao` ao final. Guarde esse arquivo. Ative **Exibir → Mostrar → Extensões de nomes de arquivos** no Explorador para ver o nome completo.
5. **Copie** o backup validado para a pasta de dados e renomeie a cópia com o nome exato do banco ativo anterior, incluindo `.sqlite`. Preserve a cópia de origem na pasta `backups`.
6. Abra o PDV para conferência. Verifique empresa, terminal, sessão do caixa, série fiscal, sequência da NFC-e e pendências antes de registrar vendas ou emitir documentos.

Se o PDV voltar a abrir, a tela **Segurança e diagnóstico** também oferece **Restaurar backup**. Se nenhuma cópia passar na verificação, preserve a pasta de dados, os XML e a mensagem exibida e encaminhe o diagnóstico ao suporte. Arquivos do banco, certificados e credenciais devem ficar nos canais autorizados de suporte.

## Android

Pela Play Store, entre com um e-mail autorizado no teste do FrontChat PDV, aceite o convite e instale a atualização. Para instalação direta, confira os APKs publicados na seção [Releases](https://github.com/andrezinho15rj/FrontChatPDV-Releases/releases).

Para impressão, emparelhe a térmica nas configurações Bluetooth do Android. Depois abra **Comunicação**, permita dispositivos próximos, selecione a impressora, escolha 58 mm ou 80 mm e toque em **Imprimir teste**.

## Atualização e modo offline

A instalação por cima da versão anterior preserva o banco local. Antes de desinstalar, confirme que a fila mostra zero pendências. Sem internet, vendas e pedidos continuam no aparelho. Quando a conexão retorna, o envio ao FrontChat é retomado automaticamente.

## Histórico — versão 0.7.0

- PDV e delivery offline para Windows e Android;
- sincronização automática de pedidos, vendas, produtos e estoque com a empresa correta no FrontChat;
- delivery para varejo, mercearia, supermercado, hortifruti, alimentação e restaurante;
- bloqueio automático do delivery em ferro-velho, sucata e reciclagem;
- etapas de pedido, entregadores, promoções, impressão e geração de PDF;
- impressão térmica no Windows pelas filas instaladas, inclusive USB, rede e Bluetooth;
- impressão ESC/POS por Bluetooth no Android em papel de 58 mm ou 80 mm.

