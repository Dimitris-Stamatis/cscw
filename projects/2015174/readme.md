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
Raspberry Pi 4 Model B - OS: Rasbian Buster Lite (Pure CLI)
## Άσκηση 1 - Connect to a wireless network
### 1.1
Διότι το raspberry θα το χρησιμοποιώ δίχως οθόνη ή περιφερειακά, αλλά με ssh μέσω LAN από terminal του desktop pc μου, χρειάζεται να το ρυθμίσω έτσι ώστε στο boot να ενεργοποιεί αυτόματα το wifi και να συνδέεται στο τοπικό μου δίκτυο. Αυτό γίνεται δημιουργώντας ένα wpa_supplicant configuration αρχείο στο boot partition του bootable media (SD Card). <br>
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
Μέσω του εργαλείου nmcli (Network-Manager Command-Line Interface) εμφανζίζουμε μια λίστα με τα διαθέσιμα ασύρματα δίκτυα και συνδεόμαστε σε ένα από αυτά.<br>
Commands:<br>
```
nmcli dev wifi list // Shows a list of all scanned and available wireless networks usign the wifi device (wlan0 in my case)
sudo nmcli dev wifi rescan // Scans for available wireless networks - Needs root privileges)
sudo nmcli dev wifi connect <ssid> password <"password"> // Connects to the network with ssid <ssid> and a pwd "pwd"
```
<a href="https://asciinema.org/a/304585" target="_blank"><img src="https://asciinema.org/a/304585.svg" /></a>
## Άσκηση 2 - Fetch the weather forecast for your home city and one more city that you want to travel to
### 2.1
Χρησιμοποιώντας το εργαλείο wttr λαμβάνουμε το δελτίο καιρού για την πόλη της Πάτρας. <br>
Commands:<br>
```
curl wttr.in/Patras
```
<a href="https://asciinema.org/a/304617" target="_blank"><img src="https://asciinema.org/a/304617.svg" /></a><br>
### 2.2
Με τη χρήση του ίδιου εργαλείου λαμβάνουμε το δελτίο καιρού για ένα αξιοθέατο το οποίο θέλουμε να επισκεπτούμε στην πόλη του Εδιμβούργου στη Σκωτία (Το κάστρο του Εδιμβούργου συγκεκριμένα).<br>
Commands:<br>
```
curl wttr.in/~Edinburgh+Castle
```
<a href="https://asciinema.org/a/aAouqLKpu1J2K1kxiVs8x9DCQ" target="_blank"><img src="https://asciinema.org/a/aAouqLKpu1J2K1kxiVs8x9DCQ.svg" /></a><br>

## Άσκηση 3 - Read the business news
### 3.1
Χρησιμοποιώντας το εργαλείο instantnews το οποίο τρέχει σε python, ζητάμε μια λίστα με όλες τις διαθέσιμες πηγές πληροφόρησης πάνω σε μια κατηγορία (π.χ. business, gaming, technology...) και ύστερα επιλέγουμε μία από αυτές τις πηγές για να μας εμφανίσει τους πρώτους τίτλους.
Commands (Θεωρώντας ότι έχει γίνει σωστή εγκατάσταση του εργαλείου και φόρτωση του API Key το οποίο λαμβάνουμε δημιουργώντας δωρεάν λογαριασμό στο αντίστοιχο site της υπηρεσίας):
```
instantnews -s business // Show Category
instantnews -n cnbc // Show the news' titles from the cnbc channel
```
Όταν όμως το έτρεξα υπήρξε ένα πρόβλημα κωδικοποίησης λόγω της χρήσης ascii από το σύστημα όπως φαίνεται στο παρακάτω demo<br>
<a href="https://asciinema.org/a/PPpdD5ZrJjpaSrenMU154S9qR" target="_blank"><img src="https://asciinema.org/a/PPpdD5ZrJjpaSrenMU154S9qR.svg" /></a><br>

Αυτό το πρόβλημα αντιμετωπίστηκε εύκολα με ένα γρήγορο ψάξιμο στα issues του αποθετηρίου του εργαλείου. Επεξεργάστηκα το source code της εφαρμογής ώστε να χρησιμοποιεί utf-8 κωδικοποίηση αντί για ascii και το πρόβλημα λύθηκε αμέσως. Η επίλυση του παραπάνω προβλήματος φαίνεται στο παρακάτω demo.<br>
<a href="https://asciinema.org/a/4A44y2M8Webhs71mBvbNMilY8" target="_blank"><img src="https://asciinema.org/a/4A44y2M8Webhs71mBvbNMilY8.svg" /></a><br>


