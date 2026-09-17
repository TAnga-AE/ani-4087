#include <iostream>
using namespace std;

struct Vecteur {
    double x, y, z;
};

struct Quaternion {
    double w, x, y, z;
};

struct Pose {
    Vecteur position;
    Quaternion rotation;
};

Vecteur appliquerPose(const Pose& pose, const Vecteur& point) {
    Quaternion q = pose.rotation;

    // Quaternion du point
    Quaternion p = {0, point.x, point.y, point.z};

    // q * p
    Quaternion qp;
    qp.w = -q.x * p.x - q.y * p.y - q.z * p.z;
    qp.x = q.w * p.x + q.y * p.z - q.z * p.y;
    qp.y = q.w * p.y - q.x * p.z + q.z * p.x;
    qp.z = q.w * p.z + q.x * p.y - q.y * p.x;

    // (q * p) * q^-1
    Quaternion resultat;
    resultat.x = qp.x * q.w - qp.w * q.x - qp.y * q.z + qp.z * q.y;
    resultat.y = qp.y * q.w - qp.w * q.y - qp.z * q.x + qp.x * q.z;
    resultat.z = qp.z * q.w - qp.w * q.z - qp.x * q.y + qp.y * q.x;

    // Translation
    Vecteur transforme;
    transforme.x = resultat.x + pose.position.x;
    transforme.y = resultat.y + pose.position.y;
    transforme.z = resultat.z + pose.position.z;

    return transforme;
}

int main() {
    Pose pose;
    Vecteur point;

    // Position de la pose
    cin >> pose.position.x >> pose.position.y >> pose.position.z;

    // Quaternion : w x y z
    cin >> pose.rotation.w
        >> pose.rotation.x
        >> pose.rotation.y
        >> pose.rotation.z;

    // Point
    cin >> point.x >> point.y >> point.z;

    Vecteur resultat = appliquerPose(pose, point);

    cout << resultat.x << " "
         << resultat.y << " "
         << resultat.z << endl;

    return 0;
}
