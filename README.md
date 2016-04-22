// Individual Project-Olympics.cpp : Donatas-Petrauskas
// Year1 final project
 
#include "stdafx.h"
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
 
void name(char *c);
void sport(char *c);
void country(char *c);
void year(char *c);
 
void main() {
    printf(" ------------------------\n|OLYMPICS RESULTS ARCHIVE|\n ------------------------\n\n");
    printf("* To find medals won by athlete, type \"name\" followed by athletes name.\n");
    printf("* To find athlete with most medal in particular sport, type \"sport\" follwed by name of sport\n");
    printf("* To find number of medals won by country, type \"country\" followed by name of country\n");
    printf("* To find results in a sport by year, type \"year\" followed by the year, then the sport name.\n\n");
 
    char temp[100];
    char *c;
    int namea;
    int sporta;
    int countrya;
    int yeara;
   
    gets_s(temp, 100);
    c = strtok(temp, " ");
    namea = strcmp(c, "name");
    sporta = strcmp(c, "sport");
    countrya = strcmp(c, "country");
    yeara = strcmp(c, "year");
    if (namea == 0){
        name(c);
    }
    else if (sporta == 0) {
        sport(c);
    }
    else if (countrya == 0) {
        country(c);
    }
    else if (yeara == 0) {
        year(c);
    }
}
 
void name(char *c) {
 
    char dump[100];
    char *name;
    char *age;
    char *country;
    char *year;
    char *sport;
    char *gold;
    char *silver;
    char *bronze;
    char *total;
 
    int j = 2;
    int k = 1;
    FILE *f;
    f = fopen("D:\\olympics.txt", "r");
    c = strtok(NULL, "/");
    while (!feof(f)) {
        fgets(dump, 100, f);
        name = strtok(dump, "\t");
        j = strcmp(c, name);
        if (j == 0) {
            printf("Name: %s\n", name);
            age = strtok(NULL, "\t");
            printf("Age: %d\n", atoi(age));
            country = strtok(NULL, "\t");
            printf("Country: %s\n", country);
            year = strtok(NULL, "\t");
            printf("Year: %d\n", atoi(year));
            sport = strtok(NULL, "\t");
            printf("Sport: %s\n", sport);
            gold = strtok(NULL, "\t");
            printf("Number of gold medals: %d\n", atoi(gold));
            silver = strtok(NULL, "\t");
            printf("Number of silver medals: %d\n", atoi(silver));
            bronze = strtok(NULL, "\t");
            printf("Number of bronze medals: %d\n", atoi(bronze));
            total = strtok(NULL, "\t");
            printf("Total number of medals: %d\n\n", atoi(total));
            k = 0;
        }
    }
    if (k != 0) {
        printf("Error in name entered!\n");
    }
    fclose(f);
}
 
void sport(char *c) {
    char *sport;
    char dump[100];
    char *discard;
    char *name;
    char *country;
    char *year;
    char *total;
    int j = 2;
    int k = 0;
    int numMedals = 0;
   
    sport = c;
    c = strtok(NULL, "/");
    FILE *f;
    f = fopen("D:\\olympics.txt", "r");
    while (!feof(f)) {
        fgets(dump, 100, f);
        name = strtok(dump, "\t");
        discard = strtok(NULL, "\t");
        country = strtok(NULL, "\t");
        year = strtok(NULL, "\t");
        discard = strtok(NULL, "\t");
        j = strcmp(c, discard);
        if (j == 0) {
            discard = strtok(NULL, "\t");
            discard = strtok(NULL, "\t");
            discard = strtok(NULL, "\t");
            total = strtok(NULL, "\t");
            if (atoi(total) > numMedals) {
                numMedals = atoi(total);
            }
        }
    }
    printf("The people with the most nummber of medals in %s are:\n", sport);
    fseek(f, 0, SEEK_SET);
    while (!feof(f)) {
        fgets(dump, 100, f);
        name = strtok(dump, "\t");
        discard = strtok(NULL, "\t");
        country = strtok(NULL, "\t");
        year = strtok(NULL, "\t");
        discard = strtok(NULL, "\t");
        j = strcmp(c, discard);
        if (j == 0) {
            discard = strtok(NULL, "\t");
            discard = strtok(NULL, "\t");
            discard = strtok(NULL, "\t");
            total = strtok(NULL, "\t");
            if (atoi(total) == numMedals) {
                printf("\nName: %s\nCountry: %s\nYear: %d\nNumber of medals: %d\n", name, country, atoi(year), numMedals);
            }
        }
    }
 
    fclose(f);
}
 
void country(char *c) {
    int numMedals = 0;
    char *discard;
    char *total;
    char *country;
    char dump[100];
    int j;
 
    c = strtok(NULL, "/");
    FILE *f;
    f = fopen("D:\\olympics.txt", "r");
    while (!feof(f)) {
        fgets(dump, 100, f);
        discard = strtok(dump, "\t");
        discard = strtok(NULL, "\t");
        country = strtok(NULL, "\t");
        j = strcmp(c, country);
        if (j == 0) {
            discard = strtok(NULL, "\t");
            discard = strtok(NULL, "\t");
            discard = strtok(NULL, "\t");
            discard = strtok(NULL, "\t");
            discard = strtok(NULL, "\t");
            total = strtok(NULL, "\t");
            numMedals = numMedals + atoi(total);
        }
    }
    printf("%s has won %d medals in the Olympics.\n", c, numMedals);
    fclose(f);
}
 
void year(char *c) {
    char *discard;
    char *name;
    char *country;
    char *sport;
    char *bronze;
    char *silver;
    char *gold;
    int j;
    int year;
    int l;
    char dump[100];
 
    c = strtok(NULL, " ");
    j = atoi(c);
    c = strtok(NULL, "/");
    FILE *f;
    f = fopen("D:\\olympics.txt", "r");
    while (!feof(f)) {
        fgets(dump, 100, f);
        name = strtok(dump, "\t");
        discard = strtok(NULL, "\t");
        country = strtok(NULL, "\t");
        year = atoi(strtok(NULL, "\t"));
        if (j == year) {
            sport = strtok(NULL, "\t");
            l = strcmp(c, sport);
            if (l == 0) {
                gold = strtok(NULL, "\t");
                silver = strtok(NULL, "\t");
                bronze = strtok(NULL, "\t");
                printf("Name: %s\nCountry: %s\n Number of Gold Medals: %d\nNumber of Silver Medals: %d\nNumber of Bronze Medals: %d\n\n", name, country, atoi(gold), atoi(silver), atoi(bronze));
            }
        }
    }
    fclose(f);
}
