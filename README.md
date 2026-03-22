# #include <iostream>
#include <string>
#include <limits>
#include <iomanip>
using namespace std;

const int MAXE = 20;

void registrar(string n[], double x[], int &c) {
    cout << "Cantidad (1-" << MAXE << "): ";
    while(!(cin >> c) || c<1 || c>MAXE){ cin.clear(); cin.ignore(numeric_limits<streamsize>::max(), '\n'); cout<<"Invalido: "; }
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
    for(int i=0;i<c;i++){
        cout << "Nombre " << i+1 << ": "; getline(cin, n[i]);
        cout << "Nota (0-100): ";
        while(!(cin >> x[i]) || x[i]<0 || x[i]>100){ cin.clear(); cin.ignore(numeric_limits<streamsize>::max(), '\n'); cout<<"Invalida: "; }
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
    }
}

bool listo(int c){ if(c<=0){ cout<<"Primero registre (opcion 1)\n"; return false;} return true; }

double promedio(const double x[], int c){ double s=0; for(int i=0;i<c;i++) s+=x[i]; return c? s/c : 0; }
int idxMax(const double x[], int c){ int m=0; for(int i=1;i<c;i++) if(x[i]>x[m]) m=i; return m; }
int idxMin(const double x[], int c){ int m=0; for(int i=1;i<c;i++) if(x[i]<x[m]) m=i; return m; }

int main(){
    string nombres[MAXE]; double notas[MAXE]; int cant=0, op;
    cout<<fixed<<setprecision(2);
    do{
        cout<<"\n1 Registrar\n2 Promedio\n3 Nota mas alta\n4 Nota mas baja\n5 Aprobados\n6 Salir\nOpcion: ";
        if(!(cin>>op)){ cin.clear(); cin.ignore(numeric_limits<streamsize>::max(), '\n'); cout<<"Opcion invalida\n"; continue; }
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
        if(op==1) registrar(nombres, notas, cant);
        else if(op==2 && listo(cant)) cout<<"Estudiantes: "<<cant<<"\nPromedio: "<<promedio(notas,cant)<<"\n";
        else if(op==3 && listo(cant)){ int i=idxMax(notas,cant); cout<<"Max: "<<notas[i]<<" ("<<nombres[i]<<")\n"; }
        else if(op==4 && listo(cant)){ int i=idxMin(notas,cant); cout<<"Min: "<<notas[i]<<" ("<<nombres[i]<<")\n"; }
        else if(op==5 && listo(cant)){ bool hay=false; cout<<"Aprobados (>=70):\n"; for(int i=0;i<cant;i++) if(notas[i]>=70){ cout<<"- "<<nombres[i]<<": "<<notas[i]<<"\n"; hay=true; } if(!hay) cout<<"(Ninguno)\n"; }
        else if(op==6) cout<<"Adios\n";
        else if(op!=1) cout<<"Opcion invalida o sin datos\n";
    }while(op!=6);
    return 0;
}

![IMG-20260321-WA0035(1)](https://github.com/user-attachments/assets/fd902b67-47e2-4a3c-9245-68572af592d5)

![IMG-20260321-WA0036(1)](https://github.com/user-attachments/assets/3a9e52eb-c00c-4c6f-9a4c-f1d4cda7f798)

