# Configurcão_repositorio_local

- configure uma VM no vagrant com centos7
- Pegue uma .iso centos minimal
- Monte a .iso com comando → mount CentOS-7-x86_64-Minimal-1810.iso /mnt
- Vá até cd /mnt/Packages
- Crie um diretório na raiz do seu sistema para copiar os pacotes exemplo → mkdir /pacotes
- Copie para o diretório que você criou cp *.rpm /pacotes/
- Para criar o metadata instale o →yum install createrepo
- Vá até a pasta que você criou cd /pacotes/ e execute → createrepo .
- vá até /etc/yum.repos.d →crie um arquivo.repo com parâmetros básicos
   
   [repoteste]
   name=Repositorio
   baseurl=file:///pacotes
   enabled=1
   gpgcheck=0 (Desabilitado pois só será necessário para a segurança/ como estamos fazendo          somente configuração básica, não é necessário, mas para produção    busque saber mais sobre  gpg)
   
- setenforce 0 para desabilitar o SeLinux (Recomendado não fazer isso em produção, porém desabilitei por que é um tutorial básico de repolocal)
- execute yum check-update
- instale o apache ou nginx →yum install httpd → systemctl enable httpd → systemctl start httpd
- Pegue o seu ip e coloque no navegador e veja se o apache está funcionando caso contrário será necessário executar firewall-cmd - -add-service=httpd - -permanent e →firewall-cmd - -reload
- vá até  /var/www/html e crie um diretorio mkdir repositorio crie um link → ln -s /pacotes /var/www/html/repositorio/
- entre no seu navegador e digite [http://seuip/repositorio](http://seuip/repositorio)/pacotes → verá que todos os pacotes estão disponibilizados
- vá até /etc/yum.repos.d abra o arquivo.repo que você criou e troque a baseurl ficando assim

- [repoteste]
  name=Repositorio
  baseurl=http://seuip/repositorio/pacotes/
  enabled=1
  gpgcheck=0
  
