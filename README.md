# days_until_month 
To show how many days until the month user inputs by using C.

#include <stdio.h>
#include <string.h>
#include <ctype.h>
#define SLEN 16

struct month {
	char name[SLEN];
	char abb[SLEN];
	int days;
	int index;
};

const struct month months[SLEN] = 
{
	{"January", "Jan", 31, 1},
	{"February", "Feb", 28, 2},
	{"March", "Mar", 31, 3},
	{"April", "Apr", 30, 4},
	{"May", "May", 31, 5},
	{"June", "Jun", 30, 6},
	{"July", "Jul", 31, 7},
	{"August", "Aug", 31, 8},
	{"September", "Sep", 30, 9},
	{"October", "Oct", 31, 10},
	{"November", "Nov", 30, 11},
	{"December", "Dec", 31, 12}
};

int days_mon(char *mon);

int main(void) {
	char mon[SLEN];
	int days;
	
	printf("Please enter your month in English: (# to quit)\n");
	while (scanf("%s", mon) == 1 && mon[0] != '#') {
		days = days_mon(mon);
		if (days > 0) {
			printf("There are %d days until %s.\n", days, mon);
		}
		else {
			printf("Invalid input. You should enter a correct name of a month.\n");
		}
		printf("The next month in English: (# quit)\n");
		while (getchar() != '\n')
			continue;
	}
	printf("Done.");
	
	return 0;
}

int days_mon(char *mon) {
	int i = 1;
	int ret = 0;
	
	mon[0] = toupper(mon[0]);
	while (mon[i] != '\0') {
		mon[i] = tolower(mon[i]);
		i++;
	}
	
	for (i=0; i<12; i++) {
		ret += months[i].days;
		if (strcmp(mon, months[i].name) == 0) {
			return ret;
		}
	}
	return -1;
}
