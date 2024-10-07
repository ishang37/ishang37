const int boutonMontee = 2;   // Bouton pour monter l'oreiller
const int boutonDescente = 3; // Bouton pour descendre l'oreiller
const int moteurPin = 9;      // Pin pour contrôler le moteur

void setup() {
  pinMode(boutonMontee, INPUT);
  pinMode(boutonDescente, INPUT);
  pinMode(moteurPin, OUTPUT);
}

void loop() {
  if (digitalRead(boutonMontee) == HIGH) {
    // Monter l'oreiller
    digitalWrite(moteurPin, HIGH);
  } else if (digitalRead(boutonDescente) == HIGH) {
    // Descendre l'oreiller
    digitalWrite(moteurPin, LOW);
  } else {
    // Arrêter le moteur quand aucun bouton n'est pressé
    digitalWrite(moteurPin, LOW);
  }
}
table escamotable
// Déclaration des pins
const int boutonOuvrirPin = 2;    // Pin du bouton pour ouvrir la table
const int boutonFermerPin = 3;    // Pin du bouton pour fermer la table
const int moteurAvantPin = 9;     // Pin pour avancer (ouvrir) le moteur
const int moteurArrierePin = 10;  // Pin pour reculer (fermer) le moteur
const int finDeCourseOuvert = 4;  // Pin du capteur fin de course "ouvert"
const int finDeCourseFerme = 5;   // Pin du capteur fin de course "fermé"

void setup() {
  // Configuration des pins
  pinMode(boutonOuvrirPin, INPUT_PULLUP);    // Bouton pour ouvrir
  pinMode(boutonFermerPin, INPUT_PULLUP);    // Bouton pour fermer
  pinMode(moteurAvantPin, OUTPUT);           // Moteur pour ouverture
  pinMode(moteurArrierePin, OUTPUT);         // Moteur pour fermeture
  pinMode(finDeCourseOuvert, INPUT_PULLUP);  // Fin de course ouvert
  pinMode(finDeCourseFerme, INPUT_PULLUP);   // Fin de course fermé
}

void loop() {
  // Lecture des états des boutons et des capteurs
  int boutonOuvrirEtat = digitalRead(boutonOuvrirPin);
  int boutonFermerEtat = digitalRead(boutonFermerPin);
  int finDeCourseOuvertEtat = digitalRead(finDeCourseOuvert);
  int finDeCourseFermeEtat = digitalRead(finDeCourseFerme);

  // Si on appuie sur le bouton pour ouvrir et que la table n'est pas encore ouverte
  if (boutonOuvrirEtat == LOW && finDeCourseOuvertEtat == HIGH) {
    ouvrirTable();  // Fonction pour déployer la table
  }
  // Si on appuie sur le bouton pour fermer et que la table n'est pas encore fermée
  else if (boutonFermerEtat == LOW && finDeCourseFermeEtat == HIGH) {
    fermerTable();  // Fonction pour rétracter la table
  }
  else {
    arreterMoteur();  // Arrêter le moteur si aucun bouton n'est pressé
  }
}

// Fonction pour ouvrir la table (activer le moteur dans le sens "avant")
void ouvrirTable() {
  digitalWrite(moteurAvantPin, HIGH);
  digitalWrite(moteurArrierePin, LOW);  // Assurez-vous que le moteur ne tourne que dans une direction à la fois
}

// Fonction pour fermer la table (activer le moteur dans le sens "arrière")
void fermerTable() {
  digitalWrite(moteurAvantPin, LOW);
  digitalWrite(moteurArrierePin, HIGH);  // Activer la fermeture
}

// Fonction pour arrêter le moteur
void arreterMoteur() {
  digitalWrite(moteurAvantPin, LOW);     // Désactiver l'avant
  digitalWrite(moteurArrierePin, LOW);   // Désactiver l'arrière
}

