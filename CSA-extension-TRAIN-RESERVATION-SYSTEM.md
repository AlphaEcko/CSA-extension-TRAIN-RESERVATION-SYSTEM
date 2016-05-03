# CSA-extension-TRAIN-RESERVATION-SYSTEM

This is an initial algorithm that can be integrated with CSA algorithm, so that when the customer wants to consult his itinerary 
he will have an integrated reservation system. That allows to the customer use the same platform and it makes the things more easy. So that we have an integrated system that allows to us perform a seat reservation and also to consult the desired itinerary.

#include <math.h>
#include <string.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

/* run this program using the console pauser or add your own getch, system("pause") or input loop */

int main(int argc, char *argv[]) {
	
int seat;
int i,j;
int seats[4][10];
int opciones=1;
int option;
int user_reservations=0;
int more_reservations=0;
int remaining_seats=5;/*NOTE: I put 5 seats for that you can see that when there is no more seats available you can't do a reservation, but you can change it to 10 (number of seats in First class)*/
int remaining_seats2=10;/*NOTE: I put 10 seats to show you can see that when there is no more seats available you can't do a reservation, but you can change it to 30 (number of seats in Economy class)*/
int reserved =0;
int no_seats=0;
int exit_opt1=0;
int final_reservation=0;
int seat_number=0;
int reserved_seat=0;
int row_seat;
int column_seat;
int additional_reservation=0;
int cancellation;
int no_seat_found=0;
char name[20];
char surname[20];
char origin[20];
char destination[20];
int day,month,year;
int ticket=0;
int cancellation_complete=0;
int count=0;
int found=0;
int cancel=0;
time_t t;
time(&t);

printf("WELCOME TO TRAIN RESERVATION SYSTEM. Next you will see the train seats and \nrelevant information for perform the reserve.\n\n");

for(i=0; i < 4 ; i++){
	for(j=0; j < 10; j++){
		
		seats[i][j]=0;
		printf("%d-%d(%d)\t",i,j,seats[i][j]);

	}
	
}



printf("\nThe legend of the seats is the next:\n\n");
printf("Example: 1-2(0) means The Seat of Row 1 and Column 2 is not ocuppied, where 0 \nis not reserved and 1 is reserved.\n");
do{

printf("\n\n******************************** MENU ***************************************\n");
printf("\nPlease choose a option:\n\n");
printf("1-First class reservation\n");
printf("2-Economy class reservation\n");
printf("3-Cancel reservation\n");
printf("4-Print ticket\n");
printf("5-Consult itinerary\n");
printf("6-Exit\n\n");
printf("Option selection: ");
scanf("%d",&option);
printf("\n");

additional_reservation=0;
exit_opt1=0;/*if we exit the first option (case1) we need to ensure that we will can re-enter this option*/

while(option < 1 || option > 6){
		
		printf("\n\n******************************** MENU ***************************************\n");
		printf("\n\nOption not valid, please only enter a option between 1 and 5\n\n");
		printf("\nPlease choose a option:\n\n");
		printf("1-First class reservation\n");
		printf("2-Economy class reservation\n");
		printf("3-Cancel reservation\n");
		printf("4-Print ticket\n");
		printf("5-Consult itinerary\n");
		printf("6-Exit\n\n");
		printf("Option selection: ");
		scanf("%d",&option);
		printf("\n");		
	}
	
switch(option){

case 1:


while(exit_opt1==0){

if(remaining_seats==0){/*there is seats available ?*/
		printf("\n\nWe are sorry, there is no more seats available.\n\n");
		no_seats=1;
		exit_opt1=1;
}


if(no_seats==0 && additional_reservation ==0 ){/*Yes, there is seats available*/
printf("************** WELCOME TO FIRST CLASS RESERVATION SECTION **************\n\n");

printf("Please enter the station of origin: ");
scanf("%s",&origin);
printf("\nPlease enter the station of destination: ");
scanf("%s",&destination);

printf("\nPlease enter the date of your travel: ");
printf("\n\nDay: ");
scanf("%d",&day);
printf("Month: ");
scanf("%d",&month);
printf("Year: ");
scanf("%d",&year);

while(day>31 || month >12 || year > 2018 || year < t){
printf("\n\nThe date entered is wrong, please note that the maximum days of a month are 31, the months are 12, the maximum year for reserves is 2018 and you can't enter\n a date less than %s .\n\n",ctime(&t));
printf("Please enter the date of your travel: ");
printf("\n\nDay: ");
scanf("%d",&day);
printf("Month: ");
scanf("%d",&month);
printf("Year: ");
scanf("%d",&year);
}

printf("\nHow many reservations in First class would you like to do ?");
printf("\n\n**Please note that there is %d available seats in First class",remaining_seats);
printf("\n\nReserves: ");
scanf("%d",&user_reservations);

while(user_reservations > remaining_seats){/*the number of reservations of the user are greater than the number of seats available ?*/
	printf("\n\nWe are sorry, the number of reservations that you entered are greater than the \nnumber of seats available, you can reserve a maximum of %d seats due to seats \navailability.\n\n",remaining_seats);
	printf("How many reservations in First class would you like to do ?");
	printf("\n\n**Please note that there is %d available seats in First class",remaining_seats);
	printf("\n\nReserves: ");
	scanf("%d",&user_reservations);
}
}

opciones=1;

while(opciones<=user_reservations && no_seats==0){
	
printf("\n\n");
row_seat=0; /*we fix row_seat=0 because the seats of First class are in this row, i.e., the row 0 is for First class customers only*/

for(i=0; i < 4 ; i++){
	for(j=0; j < 10; j++){
		
		printf("%d-%d(%d)\t",i,j,seats[i][j]);

	}
	
}

printf("\n****PLEASE NOTE THAT YOU CAN CONSULT THE TRAIN CHART ABOVE\n\n");
printf("\n\n**** NOTE that seats of First class are from seat 0-0 to 0-9, for that you will be asked only to enter the seat column.\n\n\n");

printf("Enter the column seat, that is between 0 and 9: ");
scanf("%d",&column_seat);

while (column_seat < 0 || column_seat > 9){
	
printf("\n\nThe seat that you selected it is not a First class seat\n\n");
row_seat=0;
printf("Please enter a column seat that is between 0 and 9: ");
scanf("%d",&column_seat);
}
printf("\n\n");

for(i=0; i < 4 ; i++){
	for(j=0; j < 10; j++){
		if(row_seat == i && column_seat == j){ 
			if(seats[i][j]==1){
				reserved=1;

			}else{
			
			    seats[i][j]=1;
				reserved=0;
				ticket=1;
				remaining_seats--;
				opciones++;
				final_reservation++;
			
			}

				}
				printf("%d-%d(%d)\t",i,j,seats[i][j]);

}
}

if(reserved==1){
	printf("\nTHE SEAT SELECTED IS RESERVED, PLEASE CHOOSE ANOTHER SEAT WITHOUT A VALUE OF 1\n");
	reserved=0;
}else{

printf("\nThe reservation has been successful, your seat is %d-%d, thank you for your \nreservation and have a nice trip!\n\n",row_seat,column_seat);
}
}

if(opciones>user_reservations &&  remaining_seats!=0 ){/*the initial reserve has been done and there is seats available*/

exit_opt1=0;
printf("Do you want to do another reservation? Please type 1 for Yes and 0 for No: ");
scanf("%d",&more_reservations);
printf("\n\n");	


while(more_reservations < 0 || more_reservations > 1){
		printf("\n\nOption not valid, do you want to do another reservation? Please type 1 for Yes and 0 for No: ");
		scanf("%d",&more_reservations);
		printf("\n\n");		
	}

if(more_reservations==1){
	opciones=1;
	additional_reservation=1;
	printf("How many additional reservations would you like to do ? ");
	printf("\n\n***NOTE: Seats remaining in First class: %d\n\n",remaining_seats);
	printf("Additional reservation: ");
	scanf("%d",&user_reservations);
	exit_opt1=0;

	printf("\n");

	
	while(user_reservations > remaining_seats){
    printf("\n\nWe are sorry, the number of reservations that you entered are greater than the \nnumber of seats available, you can reserve a maximum of %d seats due to seats \navailability.\n\n",remaining_seats);
	printf("How many additional reservations would you like to do ? ");
	printf("\n\nAdditional reservation: ");
	scanf("%d",&user_reservations);
	printf("\n");
		
	}
	
}else{
	exit_opt1=1;

}
}


if(opciones>final_reservation || exit_opt1==1){
	printf("\n************************ FINAL OF RESERVATION **************************\n\n");

}
}
break;

/*--------------------------------------------------------------------------------------OPTION2---------------------------------------------------------------------------------------------------*/

case 2:

while(exit_opt1==0){

printf("************** WELCOME TO ECONOMY CLASS RESERVATION SECTION **************\n\n");

if(remaining_seats2==0){/*there is seats available ?*/
		printf("\n\nWe are sorry, there is no more seats available.\n",remaining_seats2);
		no_seats=1;
		exit_opt1=1;

}

if(no_seats==0 && additional_reservation ==0 ){/*Yes, there is seats available*/

printf("Please enter the station of origin: ");
scanf("%s",&origin);
printf("\nPlease enter the station of destination: ");
scanf("%s",&destination);

printf("\nPlease enter the date of your travel: ");
printf("\n\nDay: ");
scanf("%d",&day);
printf("Month: ");
scanf("%d",&month);
printf("Year: ");
scanf("%d",&year);

while(day>31 || month >12 || year > 2018 || year < t){

printf("\n\nThe date entered is wrong, please note that the maximum days of a month are 31, the months are 12, the maximum year for reserves is 2018 and you can't enter\n a date less than %s\n\n",ctime(&t));
printf("Please enter the date of your travel: ");
printf("\n\nDay: ");
scanf("%d",&day);
printf("Month: ");
scanf("%d",&month);
printf("Year: ");
scanf("%d",&year);
}

printf("\nHow many reservations in Economy class would you like to do ?");
printf("\n\n**Please note that there is %d available seats in Economy class",remaining_seats2);
printf("\n\nReserves: ");
scanf("%d",&user_reservations);

while(user_reservations > remaining_seats2){/*the number of reservations of the user are greater than the number of seats available ?*/
	printf("\n\nWe are sorry, the number of reservations that you entered are greater than the \nnumber of seats available, you can reserve a maximum of %d seats due to seats \navailability.\n\n",remaining_seats);
	printf("How many reservations in Economy class would you like to do ?");
	printf("\n\n**Please note that there is %d available seats in Economy class",remaining_seats2);
	printf("\n\nReserves: ");
	scanf("%d",&user_reservations);
}
}

opciones=1;

while(opciones<=user_reservations && no_seats==0){

for(i=0; i < 4 ; i++){
	for(j=0; j < 10; j++){
		
		printf("%d-%d(%d)\t",i,j,seats[i][j]);

	}
	
}

printf("\n****PLEASE NOTE THAT YOU CAN CONSULT THE TRAIN CHART ABOVE\n\n");
printf("\n\n**** NOTE that seats of Economy class are from seat 1-0 to 3-9.\n\n\n");

printf("\n\n");
printf("Enter the seat row, that is between 1 and 3: ");
scanf("%d",&row_seat);
printf("Enter the column seat, that is between 0 and 9: ");
scanf("%d",&column_seat);

while (column_seat < 0 || column_seat > 9 || row_seat < 1 || row_seat > 3){
	
printf("\n\nThe seat that you selected it is not a Economy class seat\n\n");
printf("Enter the seat row, that is between 1 and 3: ");
scanf("%d",&row_seat);
printf("Enter the seat column, that is between 0 and 9: ");
scanf("%d",&column_seat);
}
printf("\n\n");

for(i=0; i < 4 ; i++){
	for(j=0; j < 10; j++){
		if(row_seat == i && column_seat == j){ 
			if(seats[i][j]==1){
				reserved=1;

			}else{
			
			    seats[i][j]=1;
				reserved=0;
				ticket=1;
				remaining_seats2--;
				opciones++;
				final_reservation++;
			
			}

				}
				printf("%d-%d(%d)\t",i,j,seats[i][j]);

}
}

if(reserved==1){
	printf("\nTHE SEAT SELECTED IS RESERVED, PLEASE CHOOSE ANOTHER SEAT WITHOUT A VALUE OF 1\n");
	reserved=0;
}else{

printf("\nThe reservation has been successful, your seat is %d-%d, thank you for your \nreservation and have a nice trip!\n\n",row_seat,column_seat);
}
}

if(opciones>user_reservations &&  remaining_seats2!=0 ){/*the initial reserve has been done and there is seats available*/

exit_opt1=0;
printf("Do you want to do another reservation? Please type 1 for Yes and 0 for No: ");
scanf("%d",&more_reservations);
printf("\n\n");	


while(more_reservations < 0 || more_reservations > 1){
		printf("\n\nOption not valid, do you want to do another reservation? Please type 1 for Yes and 0 for No: ");
		scanf("%d",&more_reservations);
		printf("\n\n");		
	}

if(more_reservations==1){
	opciones=1;
	additional_reservation=1;
	printf("How many additional reservations would you like to do ? ");
	printf("\n\n***NOTE: Seats remaining in Economy class: %d\n\n",remaining_seats2);
	printf("Additional reservation: ");
	scanf("%d",&user_reservations);
	exit_opt1=0;

	printf("\n");

	
	while(user_reservations > remaining_seats2){
    printf("\n\nWe are sorry, the number of reservations that you entered are greater than the \nnumber of seats available, you can reserve a maximum of %d seats due to seats \navailability.\n\n",remaining_seats);
	printf("How many additional reservations would you like to do ? ");
	printf("\n\nAdditional reservation: ");
	scanf("%d",&user_reservations);
	printf("\n");
		
	}
	
}else{
	exit_opt1=1;

}
}


if(opciones>final_reservation || exit_opt1==1){
	printf("\n************************ FINAL OF RESERVATION **************************\n\n");

}
}	

break;

/*--------------------------------------------------------------------------------------OPTION3---------------------------------------------------------------------------------------------------*/

case 3:

printf("For cancel a seat please enter the next information\n\n");
printf("Enter the row of the seat that you want to cancel, that is between 0 and 3: ");
scanf("%d",&row_seat);
printf("Enter the column of the seat that you want to cancel, that is between 0 and 9: ");
scanf("%d",&column_seat);

while (column_seat < 0 || column_seat > 9 || row_seat < 0 || row_seat > 3){
	
printf("\n\nThe seat that you have entered doesn't exist\n\n");
printf("Please enter the seat row that is between 0 and 3: ");
scanf("%d",&row_seat);
printf("Please enter the seat column, that is between 0 and 9: ");
scanf("%d",&column_seat);
}

printf("\n\nARE YOU SURE THAT WOULD YOU LIKE TO CANCEL YOUR RESERVATION OF SEAT %d-%d ? \n\nPLEASE ENTER 1 FOR YES AND 0 FOR NO: ",row_seat,column_seat);
scanf("%d",&cancellation);
printf("\n\n");

while(cancellation < 0 || cancellation > 1){
		printf("\n\nOption not valid. ARE YOU SURE THAT WOULD YOU LIKE TO CANCEL YOUR RESERVATION OF SEAT %d-%d ?\n\n ",row_seat,column_seat);
		printf("Please type 1 for Yes and 0 for No: ");
		scanf("%d",&more_reservations);
		printf("\n\n");		
	}
cancel=0;
if (cancellation==1){

	for(i=0; i < 4 ; i++){
	for(j=0; j < 10; j++){
		
		if(row_seat == i && column_seat == j){
			if(seats[i][j]==1){
				seats[i][j]=0;
				found=1;
			}
			
	

				}
				printf("%d-%d(%d)\t",i,j,seats[i][j]);

}
count++;
}
	


if(count==4 && found==0){
			
			    printf("\n\nThe seat you have entered does not appear as reserved,the problem may be due to: \n\n"); 
			    printf("\t-You don't have a seat reserved; or\n\n");
			    printf("\t-You have entered the wrong seat.\n\n");
			    printf("Please check\n\n");
			    
			
}else{

					printf("\n\nThe cancellation of the seat %d-%d has been done successfully.\n\n",row_seat,column_seat); 
					found=0;
					cancel=1;

}
}
	break;
	
case 4:

if(cancel==0){

	if(ticket==1){/*that means that we did a reserve and therefor we have the right to print a ticket*/
	
	
	printf("\nPlease enter your name: ");
	scanf("%s",&name);
	printf("\nPlease enter your surname: ");
	scanf("%s",&surname);
	printf("\n\n\n\n\n");
	printf("Your ticket is the next:\n\n");
	printf("\n\n****************************** TRAIN TICKET ******************************");
	printf("\n\nName and surname: %s %s",name, surname);
	printf("\nOrigin: %s",origin);
	printf("\nDestination: %s",destination);
	printf("\nSeat: %d-%d (Seat Row %d Column %d).",row_seat,column_seat,row_seat,column_seat);
	printf("\nTravel date: %d/%d/%d ",day,month,year);
	printf("\nTime and date of reservation : %s",ctime(&t));
	printf("\n********************* THANK YOU FOR YOUR RESERVE ******************************\n\n");

}
else{
	printf("\nWe are sorry, you don't have any reservation, so you can't print a ticket.\n\n");
}
}else{
	printf("\nWe are sorry, you don't have any reservation, so you can't print a ticket.\n\n");
}
	break;
	
case 5:
	
		printf("\n\nHERE IS THE PLACE OF CSA ALGORITHM, FOR COMPILATION REASONS I CAN'T INTEGRATE IT WITH MY EXTENSION AND THERE FOR I DIDN'T PUT IT HERE\n\n");

	break;

case 6:
	
		printf("\n\nTHANK YOU FOR USING THE TRAIN RESERVATION SYSTEM, SEE YOU SOON! :D\n\n");

	break;
}	
}while(option!=6);

/*if(option==3){
}*/

		return 0;

}
