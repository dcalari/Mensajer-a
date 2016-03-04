# Mensajer-a

//Proyecto construcción de software

//PROYECTO QUE BUSCA CREAR UNA APLICACIÓN PARA EL REGISTRO DE CORRESPONDENCIA DE UNA COMPAÑIA

#include <stdio.h>
#include <conio.h>
#include <iostream>
using namespace std;

#define bool int
#define true 1
#define false 0

FILE *archivo, *temporal;

int p=0;

void AGREGAR_CORREO()

{
	int consecutivo=0, registro;
	char remitente[20], empresa[20], destinatario[15], resp;
	bool no_encontrado;

	do {

		if ((archivo = fopen("Directorio.ang", "r")) == NULL)
		{
			cout << "\n No se Encuentra el Archivo!";
			cout << "\n\n Pulse una tecla para continuar...";
			getch();
		}
		else {

			system("cls");
			no_encontrado = true;
			registro=p++;
			while ((!feof(archivo)) && (no_encontrado))
			{
				fscanf(archivo, "%d %s %s %s", &consecutivo, &remitente, &empresa, &destinatario);
				if (registro == consecutivo)
				{
					no_encontrado = false;
				}
			}
			fclose(archivo);
			if (no_encontrado)
			{
				archivo = fopen("Directorio.ang", "a");
				consecutivo = registro;
				cout << "\n Introduzca el Remitente: "; cin >> remitente;
				cout << " Introduzca la Empresa: "; cin >> empresa;
				cout << " Introduzca el Destinatario: "; cin >> destinatario;
				fprintf(archivo, "%d %s %s %s\n", consecutivo, remitente, empresa, destinatario); 
			}
			else {
				cout << "\n Este correo ya fue Registrado!";
			}
			cout << "\n\n Desea Registrar Otra Documento? S/N: "; resp = getch();
			fclose(archivo);
		}
	} while ((resp == 's') || (resp == 'S'));
} 

void CONSULTAR_CORREO()

{

	int registro, consecutivo;
	char remitente[20], empresa[20], destinatario[15], resp;
	bool no_encontrado;

	do {

		if ((archivo = fopen("Directorio.ang", "r")) == NULL)
		{
			cout << "\n No se Encuentra el Archivo!";
			cout << "\n\n Pulse una tecla para continuar...";
			getch();
		}
		else {
			system("cls");
			no_encontrado = true;
			cout << "\n Introduzca la consecutivo a Consultar: "; cin >> registro;
			while ((!feof(archivo)) && (no_encontrado))
			{
				fscanf(archivo, "%d %s %s %s", &consecutivo, &remitente, &empresa, &destinatario);
				if (registro == consecutivo)
				{
					no_encontrado = false;
				}
			}
			if (no_encontrado)
			{
				cout << "\n No Existe un Registro con esa consecutivo!\n\n";
			}
			else {
				cout << "\n Registro Encontrado!\n\n";
				cout << " consecutivo:   " << consecutivo << "\n";
				cout << " remitente: " << remitente << "\n";
				cout << " empresa:   " << empresa << "\n";
				cout << " destinatario: " << destinatario << "\n\n";
			}
			cout << " Desea Realizar Otra Consulta? S/N: "; resp = getch();
			fclose(archivo);
		}
	} while ((resp == 's') || (resp == 'S'));
} 


void LISTAR_CORREOS()

{
	char consecutivo[8], remitente[20], empresa[20], destinatario[15];
	if ((archivo = fopen("Directorio.ang", "r")) == NULL)
	{
		cout << "\n No se Encuentra el Archivo!";
		cout << "\n\n Pulse una tecla para continuar...";
		getch();
	}
	else {
		system("cls");
		cout << "  consecutivo        remitente        empresa        destinatario\n\n";
		while (!feof(archivo))
		{
			fscanf(archivo, "%s %s %s %s\n", &consecutivo, &remitente, &empresa, &destinatario);
			cout << " " << consecutivo << "     " << remitente << "         " << empresa << "          " << destinatario << "\n";
		}
		fclose(archivo);
		cout << "\n\n Pulse una tecla para continuar...";
		getch();
	}
} 

void MENU()

{
	cout << "\n    BIENVENIDO AL RADICADOR DE CORRESPONDENCIA <--\n";
	cout << "          Seleccione una de las siguiente opciones: \n";
	cout << " 1- Radicar un nuevo correo.\n";
	cout << " 2- Consultar el radicado de un correo.\n";
	cout << " 3- Listar todos los correos radicados.\n";
	cout << " S- Salir.\n";
}

int main()
{
	char op;
	bool salir = false;
	do {
		system("cls");
		if ((archivo = fopen("Directorio.ang", "r")) == NULL)
		{
			cout << "\n No hay correos radicados.\n";
			cout << " Presiona una tecla para Iniciar a radicar...";
			getch();
			archivo = fopen("Directorsio.ang", "w");
			fclose(archivo);
			cout << "\n\n El Archivo se ha Creado con Exito!!!\n\n";
			MENU();
			cout << "\n Seleccione una Opcion: "; op = getch();
		}
		else {
			MENU();
			cout << "\n Seleccione una Opcion: "; op = getch();
		}
		switch (op)
		{
		case '1':
			AGREGAR_CORREO();
			break;
		case '2':
			CONSULTAR_CORREO();
			break;
		case '3':
			LISTAR_CORREOS();
			break;
		case 's': case 'S':
			salir = true;
			break;
		}
	} while (salir == false);
	return 0;
} 
 

