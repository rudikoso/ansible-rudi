# Opdracht automatiseren voor SIMLAB2
 
Voor deze opdracht zal ik de service tftp installeren en configureren via een playbook.
 
## start met een ping
Voor ik de installatie begin voer ik een ping uit.  Krijg ik hier een error dan weet ik dat de machine niet bereikbaar is.
 
## Installeer tftpd-hpa
Na de replay van de ping wordt tftpd-hpa geinstalleerd.
De configguratie zal volledig verlopen via de playbook.
 
## Installeren van een package.
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/package_module.html

## Maak de directory /tftpboot aan.
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/file_module.html
Plaats deze in de root en geef het een umask van 0777.  Pas owner en group aan naar tftp:tftp

## Neem een backup van de config tftpd-hpa.
Voor dat je een config file bewerkt neem je best een backup van deze file.
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/copy_module.html

## PAs de config file van tftpd-hpa aan.
Geef de locatie op waar tftp de files bewaard. In dit geval is dit /tftpboot.
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/lineinfile_module.html

## Stop tftpd-hpa.service.
tftpd-hpa maakt enkel een log aan in de syslog over wanneer de service is gestart of gestopt.  
Ik wil een beter zicht krijgen over welke files er getransporteerd worden door deze service en van en naar waar deze verstuurt worden.
Hievoor gaan we een debug inschakelen.  De service zal eerst gestopt worden, we passen de config file aan zodat er logs gemaakt worden en starten nadien de service handmatig op met -verbosity 5.  Dit geeft zowat de meeste output van logs.
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/service_module.html

## Pas config tftpd-hpa aan.
Pas TFTP_OPTIONS aan naar "--secure --create --verbose".
Hierdoor zullen er logs gemaakt worden in /var/log/syslog.

## Start service tftpd-hpa handmatig op.
We starten deze keer niet via systemctl de service op maar gaan dit handmatig opstarten.
Hierdoor kan ik verbosity 5 meegeven wat ervoor zorgt dat het maximum aan logging wordt gegenereerd.
Dit zal via het volde cmd gebeuren "sudo service tftpd-hpa start -verbosity 5 ".

## logfile.
Vervolgens maak ik de file tftp.log aan via touch en geef ik deze file rw-rw-r rechten zodat deze beschreven kan worden.
Deze file is nodig omdat er dagelijks een script zal runnen via crontab om de tftp logs uit de syslog weg te schijven.

