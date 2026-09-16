#include <iostream>

// Définition d'une structure pour le vecteur 3D
struct Vecteur3D {
    double x;
    double y;
    double z;

    // Affiche le vecteur sous forme (x, y, z)
    void afficher() const {
        std::cout << "(" << x << ", " << y << ", " << z << ")" << std::endl;
    }

    // Addition de deux vecteurs
    Vecteur3D operator+(const Vecteur3D& autre) const {
        return {x + autre.x, y + autre.y, z + autre.z};
    }
};

// Fonctions de directions
Vecteur3D Avant() {
    return {0.0, 0.0, 1.0}; // Avancer dans la profondeur (axe Z)
}

Vecteur3D Haut() {
    return {0.0, 1.0, 0.0}; // Direction verticale (axe Y)
}

Vecteur3D Droit() {
    return {1.0, 0.0, 0.0}; // Direction horizontale (axe X)
}

// Programme principal
int main() {
    // Exemple d'utilisation
    Vecteur3D point = {2.0, 3.0, 4.0};
    std::cout << "Point initial : ";
    point.afficher();

    std::cout << "Direction Avant : ";
    Avant().afficher();

    std::cout << "Direction Haut : ";
    Haut().afficher();

    std::cout << "Direction Droit : ";
    Droit().afficher();

    // Combinaison des vecteurs
    Vecteur3D diagonale = Avant() + Haut() + Droit();
    std::cout << "Direction diagonale (Avant + Haut + Droit) : ";
    diagonale.afficher();

    return 0;
}
