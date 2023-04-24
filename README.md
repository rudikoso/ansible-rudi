# ansible-tfptd-hpa
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