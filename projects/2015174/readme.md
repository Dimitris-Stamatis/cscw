# ΙΟΝΙΟ ΠΑΝΕΠΙΣΤΗΜΙΟ 


# ΤΜΗΜΑ ΠΛΗΡΟΦΟΡΙΚΗΣ 


# ΜΑΘΗΜΑ
## Κινητά και Κοινωνικά Μέσα
 
Επιβλέπων καθηγητής: Χωριανόπουλος Κωνσταντίνος 


# Επιλογή Εργασίας
## Συνεργατική Κατασκευή Ιστοσελίδας του Τμήματος

Δημήτριος Σταμάτης <br>
ΑΜ: Π2015174

# ΑΣΚΗΣΕΙΣ
## Περιβάλλον ανάπτυξης ασκήσεων: 
[Raspberry Pi 4 Model B](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/) - OS: [Rasbian Buster Lite (Pure CLI)](https://www.raspberrypi.org/downloads/raspbian/)
## Άσκηση 1 - Connect to a wireless network
### 1.1
Διότι το raspberry θα το χρησιμοποιώ δίχως οθόνη ή περιφερειακά, αλλά με [ssh](https://www.ssh.com/) μέσω LAN από terminal του desktop pc μου, χρειάζεται να το ρυθμίσω έτσι ώστε στο boot να ενεργοποιεί αυτόματα το wifi και να συνδέεται στο τοπικό μου δίκτυο. Αυτό γίνεται δημιουργώντας ένα wpa_supplicant configuration αρχείο στο boot partition του bootable media (SD Card). [Setting up a Raspberry Pi headless](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md) <br>
Στο συγκεκριμένο παράδειγμα το wifi SSID είναι "Stamatis" και ο κωδικός "1234567890123"
```
country=GR # Alpha-2 Unicode ISO Identifier για το WiFi πρωτόκολλο
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev # Path στο οποίο θα γίνει η αντιγραφή των καινούριων ρυθμίσεων στο σύστημα καθώς και το group στο οποίο θα δωθεί η ιδιοκτησία του αρχείου
update_config=1 # Να επιτρέπονται οι εγγραφές στο παραπάνω path για αυτό το session

network={ # Τα στοιχεία του δικτύου στο οποίο θέλουμε να συνδεθούμε
    ssid="Stamatis"
    psk="1234567890123"
}
```
### 1.2
Μέσω του εργαλείου [nmcli (Network-Manager Command-Line Interface)](https://developer.gnome.org/NetworkManager/stable/nmcli.html) εμφανζίζουμε μια λίστα με τα διαθέσιμα ασύρματα δίκτυα και συνδεόμαστε σε ένα από αυτά.<br>
Commands:<br>
```
nmcli dev wifi list // Shows a list of all scanned and available wireless networks usign the wifi device (wlan0 in my case)
sudo nmcli dev wifi rescan // Scans for available wireless networks - Needs root privileges)
sudo nmcli dev wifi connect <ssid> password <"password"> // Connects to the network with ssid <ssid> and a pwd "pwd"
```
<a href="https://asciinema.org/a/CmYgSFE25eamKYCX83zzzwqXs" target="_blank"><img src="https://asciinema.org/a/CmYgSFE25eamKYCX83zzzwqXs.svg" /></a><br>
## Άσκηση 2 - Fetch the weather forecast for your home city and one more city that you want to travel to
### 2.1
Χρησιμοποιώντας το εργαλείο [wttr](https://github.com/chubin/wttr.in) λαμβάνουμε το δελτίο καιρού για την πόλη της Πάτρας. <br>
Commands:<br>
```
curl wttr.in/Patras
```
<a href="https://asciinema.org/a/u8bHN2AFpE9vqJFV4aChRk4Zr" target="_blank"><img src="https://asciinema.org/a/u8bHN2AFpE9vqJFV4aChRk4Zr.svg" /></a><br>
### 2.2
Με τη χρήση του ίδιου εργαλείου λαμβάνουμε το δελτίο καιρού για ένα αξιοθέατο το οποίο θέλουμε να επισκεπτούμε στην πόλη του Εδιμβούργου στη Σκωτία (Το [κάστρο του Εδιμβούργου](https://en.wikipedia.org/wiki/Edinburgh_Castle) συγκεκριμένα).<br>
Commands:<br>
```
curl wttr.in/~Edinburgh+Castle
```
<a href="https://asciinema.org/a/sPASOgWB3gWyNX8n639P8q1bQ" target="_blank"><img src="https://asciinema.org/a/sPASOgWB3gWyNX8n639P8q1bQ.svg" /></a><br>

## Άσκηση 3 - Read the business news
### 3.1
Χρησιμοποιώντας το εργαλείο [instantnews](https://github.com/shivam043/instantnews) το οποίο τρέχει σε python, ζητάμε μια λίστα με όλες τις διαθέσιμες πηγές πληροφόρησης πάνω σε μια κατηγορία (π.χ. business, gaming, technology...) και ύστερα επιλέγουμε μία από αυτές τις πηγές για να μας εμφανίσει τους πρώτους τίτλους.<br>
Commands (Θεωρώντας ότι έχει γίνει σωστή εγκατάσταση του εργαλείου και φόρτωση του API Key το οποίο λαμβάνουμε δημιουργώντας δωρεάν λογαριασμό στο αντίστοιχο site της υπηρεσίας):
```
instantnews -s business // Show Category
instantnews -n cnbc // Show the news' titles from the cnbc channel
```
Όταν όμως το έτρεξα υπήρξε ένα πρόβλημα κωδικοποίησης λόγω της χρήσης ascii από το σύστημα όπως φαίνεται στο παρακάτω demo<br>
<a href="https://asciinema.org/a/dokdjEiI9KhnAN2w9mQkFnvRD" target="_blank"><img src="https://asciinema.org/a/dokdjEiI9KhnAN2w9mQkFnvRD.svg" /></a><br>

Αυτό το πρόβλημα αντιμετωπίστηκε εύκολα με ένα γρήγορο ψάξιμο στα [issues](https://github.com/shivam043/instantnews/issues/19) του αποθετηρίου του εργαλείου. Επεξεργάστηκα το source code της εφαρμογής ώστε να χρησιμοποιεί utf-8 κωδικοποίηση αντί για ascii και το πρόβλημα λύθηκε αμέσως. Η επίλυση του παραπάνω προβλήματος φαίνεται στο παρακάτω demo.<br>
<a href="https://asciinema.org/a/vTcm6Wh04nojUCVUL6Jp7xyov" target="_blank"><img src="https://asciinema.org/a/vTcm6Wh04nojUCVUL6Jp7xyov.svg" /></a><br>


## Άσκηση 4 - Use your favorite text-based browser to retrieve information from the web
### 4.1
Για αυτήν την άσκηση χρησιμοποίησα το εργαλείο [links](https://en.wikipedia.org/wiki/Links_(web_browser)) ώστε να πλοηγηθώ στην ιστοσελίδα της Wikipedia και συγκεκριμένα στη σελίδα που μιλάει για το εργαλείο links. Χρησιμοποίησα keyboard shortcuts για να κάνω scroll στη σελίδα και arrow keys για να επιλέξω τα links που ήθελα να clickαρω. Στη συνέχεια θέλησα να δω αν αυτή η σελίδα έχει download link για το links. Χρησιμοποιώντας το αντίστοιχο shortcut έκανα εύρεση για τον όρο "download" και στη συνέχεια μεταφέρθηκα στο index των διαθέσιμων αρχείων λήψης του links. Επέλεξα την πιο πρόσφατη έκδοση και κατέβασα το αρχείο.<br>
<a href="https://asciinema.org/a/SkzvmVymzDJlIp0DQT7ALzILn" target="_blank"><img src="https://asciinema.org/a/SkzvmVymzDJlIp0DQT7ALzILn.svg" /></a><br>
