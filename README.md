// Viljami Jokela 25TietoA
// MyGrep-projekti 

#include <iostream>
#include <fstream>
#include <string>
#include <locale>

using namespace std;

int main(int argc, char* argv[]) {
    setlocale(LC_ALL, "FI_fi");

    if (argc == 1) {
        string iso, haku;

        cout << "Anna merkkijono josta etsitään: ";
        getline(cin, iso);

        cout << "Anna haettava merkkijono: ";
        getline(cin, haku);

        int pos = iso.find(haku);

        if (pos != -1)
            cout << "\"" << haku << "\" löytyi merkkijonosta \""
            << iso << "\" kohdasta " << pos << endl;
        else
            cout << "\"" << haku << "\" EI löytynyt merkkijonosta \""
            << iso << "\"" << endl;

        return 0;
    }

    if (argc == 3) {
        string haku = argv[1];
        string tiedosto = argv[2];

        ifstream f(tiedosto);
        if (!f.is_open()) {
            cout << "Tiedostoa \"" << tiedosto << "\" ei voitu avata." << endl;
            return 1;
        }

        string rivi;
        while (getline(f, rivi)) {
            if (rivi.find(haku) != string::npos)
                cout << rivi << endl;
        }

        return 0;
    }

    cout << "Käyttö:\n"
        << "  ./mygrep                 (kyselytila)\n"
        << "  ./mygrep hakusana tiedosto.txt\n";

    return 0;
}
