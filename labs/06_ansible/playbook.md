# Übungsaufgabe: Ansible Playbook

In dieser Übung erstellen Sie ein Ansible Playbook. 

# Aufgabenstellung 

1. Erstellen Sie ein Ansible Playbook mit mindestens folgenden Bestandteilen: 
    * Playbook-Datei 
    * Hosts-Datei 
    * Den erforderlichen Rollen 
2. Host-Datei 
    * Als Zielsystem nutzen Sie `localhost` oder `172.0.0.1`
3. Erstellen Sie ein Playbook, das folgende Rollen beinhaltet
    * [UFW](https://help.ubuntu.com/community/UFW) 
        * Sämtliche Ports sind geschlossen
        * Geöffnet sind die Ports 
            * 22
            * 80
            * 443
            * 110
            * 587
    * [Cron](https://help.ubuntu.com/community/CronHowto) 
        * Erstellen Sie einen Cron-Job, der jede Nacht Punkt 04:00 den Server rebootet
    * SSH Login  
        * Stellen Sie sicher, dass es nicht mehr möglich ist sich mit einem Passwort anzumelden.
        * Stichwort `sshd_config`
        * Hinweis: Bei einem solchen Vorgehen ist es erforderlich, dass Sie vorher den public Key Ihres SSH-Schlüssels auf die Maschine laden (dies ist kein Bestandteil dieser Übung)
4. Stellen Sie sicher, dass jede Rolle einzeln ausgeführt werden kann 
5. Erstellen Sie eine Readme-Datei (README.txt), in der der erforderliche Kommando steht, die zum Ausführen des Playbooks erforderlich ist. 

* Ihr Zielsystem ist ein [Ubuntu 20.04 LTS](https://releases.ubuntu.com/20.04/)
* Nutzen Sie eine [VirtualBox](https://www.virtualbox.org/) in der Sie Ihr Ubuntu installieren 
* Das System ist Host als auch Node gleichzeitig, d.h. Sie führen das Playbook in Ihrer VirtualBox aus.
* Geben Sie die gesamte Verzeichnis-Struktur mit allen erforderlichen Dateien als ZIP-Datei ab.