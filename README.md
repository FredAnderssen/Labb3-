#include <stdio.h>
#include <math.h>
#include "Calendar.h"
#include <stdlib.h>

#define DECEMBER 12
#define JULDAG 24

//Func Deklarationer
int menu(void);
int underMenu(void);
void menuChoice(int);
void underMenuChoice(int choice);
void yearMonthDay(void);

int getYearFromUser(void);
int getMonthFromUser(void);
int getDayFromUser(void);

int showCalendar(void);
int getInteger(char* text);
char * dayName(int day);

void juldag(void);
void something(void);

void printCalendarMonth(int month, int year);


int main(void)
{
	system("chcp 1252");

	int choice = 0;
	do
	{
		choice = menu();
		if (choice == 2)
		{
			int newchoice = 0;
			newchoice = underMenu();
			underMenuChoice(newchoice);
			getchar();
		}
		else
		{
			menuChoice(choice);
			getchar();
		}
			
		
	} while (choice);
	
	return 0;

}

//Func Definitioner
int menu(void)
{
	system("cls");
	printf("\t Huvudmeny \n \t ========= \n\t1. Hämta dag för ett visst datum\n\t2. Hämta dag för helgdag\n\t3. Skriv ut en månadskalender\n\t0. Avsluta\n ");
	
	return getInteger("\n\t Välj ett val: ");
}

int underMenu(void)
{
	system("cls");
	printf("\t Hämta dag för helgdag \n \t ========= \n\t1. Juldag\n\t2. Nyårsdag\n\t3. Midsommardag\n\t0. Tillbaka till huvudmenyn\n ");

	return getInteger("\n\t Välj ett val: ");
}

void menuChoice(int choice)
{
	switch (choice)
	{
	case 1:
		//blala func 
		yearMonthDay();
		break;

	case 2:
		
		break;


	case 3:
		showCalendar();
		break;
		
	case 0:
		printf("\n\t Programmet kommer stängas ner, var vänlig klicka på en knapp");
		break;

	default:
		break;
	}
}

void underMenuChoice(int newchoice)
{
	
	switch (newchoice)
	{

	case 1:
		
		juldag();
		break;

	case 2:
		//kan använda samma func efters dagarna är på samma dag ändå
		juldag();
		break;

	case 3:
		something();

	case 0:
		printf("\n\t Du kommer återgå till Huvudmenyn, vänligen klicka");
		break;
		

	default:
		break;
	}
}

//something is insane
void something(void)
{
	int year, month, day;
	int Dagen;
	year = getYearFromUser();

	month = 6;
	for (int i = 20; i <= 26; i++)
	{
		Dagen = ((firstDayOfMonth(month, year) + i) % 7);
		dayName(i);
		if ( dayName(i) == "Lördag")
		{
			day = i;
			printf("%s", dayName(day));
		}
	}
	

	// Dagen = ((firstDayOfMonth(month, year) + day) % 7);
	// printf("%s", dayName(Dagen));
}


void juldag(void)
{
	int year, month, day;
	int Dagen;
	year = getYearFromUser();

	month = DECEMBER;
	day = JULDAG;
	
	Dagen = ((firstDayOfMonth(month, year) + day) % 7);
	printf("%s", dayName(Dagen));

}

void yearMonthDay(void)
{
	int year, month, day;
	int förstaDagen;

	year = getYearFromUser();
	month = getMonthFromUser();
	day = getDayFromUser();

					//Får ut antal dagar
	if (day <= monthDays(month, year))
	{
						//Får ut månadens första dag
		förstaDagen = ((firstDayOfMonth(month, year) + day) % 7);
		printf("%s", dayName(förstaDagen));

	}
}

int getYearFromUser(void)
{
	//temporär, year ska scannas in
	int year;
	printf("year:");
	scanf_s("%d", &year);
	getchar();
	if (year <= 1900) {

		printf("\n\t input not acceptable");

	}

	printf("År valt: %d", year);
	return year;
	

}

int getMonthFromUser(void)
{
	printf("\n \n month");
	int month;
	scanf_s("%d", &month);
	getchar();
	if (month >= 1 && month <= 12)
	{ 
		printf("Månad vald: %d", month);
		return month;
	}
	else printf("\n\t input not acceptable");
	
}

int getDayFromUser(void)
{
	int year, month;

	printf("\n\n dag: ");
	int dag;
	scanf_s("%d", &dag);
	getchar();

	return dag;
}

char * dayName(int day)
{
	switch (day)
	{
	case 1: return "Söndag"; break;
	case 2: return "Måndag"; break;
	case 3: return "Tisdag"; break;
	case 4: return "Onsdag"; break;
	case 5: return "Torsdag"; break;
	case 6: return "Fredag"; break;
	case 7: return "Lördag"; break;
	
	default: return "Not a valid day"; //We should never end up here
	}
}

int showCalendar(void)
{
	int year, month;
	year = getYearFromUser();
	month = getMonthFromUser();

	printCalendarMonth(month, year);
}



//function lånad av Anders Carstensen
int getInteger(char* text)
{
	int anIntegerNumber, c, count = 0, retValScanf = 0; //Forces into the loop
	while (!retValScanf || count > 0)
	{
		count = 0;
		printf("%s", text);
		retValScanf = scanf_s("%d", &anIntegerNumber);
		while ((c = getchar()) != '\n' && c != EOF) // Remove unnecessary characters
			count++;
		if (!retValScanf || count > 0)
			printf("\nWrong input. Try again!");
	}
	return anIntegerNumber;
}
