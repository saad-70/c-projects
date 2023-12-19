#include <iostream>

using namespace std;

int main(){
double total =0.0;
int price=1000.0;


	int agy;
	cout<<"How old:";
	cin>>agy;

	int  Driving ;
	cout<<"How years Driving Experience: ";
	cin>>Driving;
	
	int Record;
	cout<<"Hwo Driving Record:" ;
	cin>>Record;

	if (agy< 25){
  total=(price)+ (price*(20.0/100));
	}else if (25<=agy && agy<=40){
		}else if (40<agy){ total=(price)-(price*(5.0/100));
	}
	
 if (Driving<3){
 	total=(total)+(total*(15.0/100));
 
 }else if (Driving>=3){
 	total=(total)+(total*(5.0/100));
 }
 
if(Record>=3){
 	total=total+(total)*(25.0/100);
	  }
 	else if(Record=1){
 		total=(total+total*(10.0/100));
	 } else (Record=0);
 
 cout<<total;
 }
 
