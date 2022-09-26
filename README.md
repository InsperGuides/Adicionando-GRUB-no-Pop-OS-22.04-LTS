---
Insper: Laboratório Ágil
date: Setembro 2022
---

Adicionando o GRUB no Pop OS (Pop-OS 22.04 LTS)
===

Quando instalamos o Pop-OS, ela por padrão utiliza o systemd-boot (ou gummiboot) por padrão para inicializar o Sistema Operacional, e isto causa um problema quando estamos trabalhando com Dual Boot com outros OS, pois ele não irá detectar sozinho os demais sistemas instalados na sua máquina e criar o menu para boot de forma automática.

Com este tutorial, iremos trocar o gummiboot pelo GRUB, fazendo com que todos os OS instalados apareçam corretamente ao ligar a máquina

---

### Passo 1: Instalando o GRUB:

Após instalarmos o POP-OS, a primeira coisa que devemos fazer é instalar os pacotes necessários para criar o boot, sendo eles o grub-efi, o grub2-common, e o grub-customizer.

no bash, rode o seguinte comando:

```
sudo apt install grub-efi grub2-common
```

Após rodar o comando, basta esperar a conclusão da instalação dos dois pacotes. Porém, ainda precisamos instalar o pacote do GRUB Customizer. Para tal, precisamos primeiramente adicionar o repositório do programa com o comando abaixo:

```
sudo add-apt-repository ppa:danielrichter2007/grub-customizer
```

em seguida, atualize o gerenciador de pacotes:

```
sudo apt-get update
```

Antes de prosseguirmos com a instalação do Grub Customizer, vams instalar o GRUB com o comando abaixo:

```
sudo grub Install
```

Após concluir a instalação, verificando que não houve nenhum erro no processo, instale o Grub Customizer com o comando abaixo:

```
sudo apt-get install grub-customizer
```

Caso não ocorra nennum erro, prossiga para o próximo passo.

---

### Passo 2: Copiar os arquivos de boot para uma nova pasta:

Após instalarmos corretamente o GRUB e o GRUB Customizer, iremos criar um repositório para nossa configuração de boot. Utilize o código abaixo:

```
sudo cp /boot/grub/x86_64-efi/grub.efi /boot/efi/EFI/pop/grubx64.efi
```
Caso não ocorra nenhum erro, o arquivo deve ter sido copiado com sucesso. Prossiga para o próximo passo.

---

### Passo 3: Ajustes no GRUB Customizer:

Agora iremos utilizar o GRUB Customizer para ajustar nosso boot. Digite no bach:

```
grub-customizer
```
Autentique o acesso com a senha do seu computador (caso possua), e então, dentro do Customizer, vá na aba Files do menu superior, e clique em Change Enviroment...:
![image](https://user-images.githubusercontent.com/18387737/192347281-e1b85ff5-42c9-44d4-8e44-7e46e357218c.png)

Dentro da nova tela, altere a opção OUTPUT_FILE com a linha abaixo, para criar um novo arquivo de configuração do GRUB na nossa pasta gerada no passo anterior:

```
/boot/efi/EFI/pop/grub.cfg
```

Antes de clicar em Apply, marque a opção *Save this configuration* logo acima. No fim, seu setup deve estar como a imagem abaixo:

![image](https://user-images.githubusercontent.com/18387737/192347881-3ecea121-3e49-4085-8af8-c37a65fe302b.png)

Após clicar em Apply, devemos reiniciar nosso computador, e caso tudo tenha sido feito corretamente, uma nova opção de boot chamada *pop* deverá aparecer no boot da BIOS. Este será o boot para o GRUB na sua máquina.

Caso queira alterar a aparência ou ajsutar a ordem do GRUB, basta retornar ao seu Pop e abrir o Grub Customizer novamente para fazer estas configurações.

