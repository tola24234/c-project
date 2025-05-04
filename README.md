#include<iostream>
#include<fstream>
#include<string.h>
#include<iomanip>
using namespace std;

void registeraPatient();
void displayPatient();
void sreachPatient();
void menu();
struct eroll{
    char name[20];
    int age;
    int id;
    char department[30];

};
eroll x;


int main()
{


cout<<"\t WELCOME TO OUR HARAMAYA UNIVERSITY GENERAL HOSPITAL:"<<endl;
cout<<"\t #######################:"<<endl;
cout<<"\t\t Haramaya university  Hospital:"<<endl;
    menu();


    return 0;

}
void menu()
{
    cout<<"\t #######################:"<<endl;
    cout<<" menu list enter your choice:"<<endl;
    cout<<"\t 1. for register new student :"<<endl;
    cout<<"\t 2.for student registered before now :"<<endl;
    cout<<"\t 3.for all list :"<<endl;
    cout<<"\t 4. system exit  :"<<endl;

    int choice;
    do
    {
    cout<<"\t\tEnter your choice="<<endl;
    cin>>choice;
    switch(choice)
    {
        case 1:registeraPatient();
        break;
        case 2:sreachPatient();
        break;
        case 3:displayPatient();
        break;
        case 4:exit(0);
        break;
        default:cout<<"your choice is wrong try again"<<endl;
    }
    }while(choice!=4);
    cout<<"#######################:"<<endl;

}
void registeraPatient()
{
    cout<<"#######################:"<<endl;

   ofstream myfile;
    myfile.open("eroll.txt",ios::app);

        cin.ignore();
        cout<<"enter patient name:"<<endl;
        cin.getline(x.name,20);
        cout<<"enter patient age:"<<endl;
        cin>>x.age;
        cin.ignore();
        cout << "Enter patient Id: "<<endl;
        cin >> x.id;
        cin.ignore();
        cout << "Enter patient department: "<<endl;
        cin.getline(x.department, 30);
       myfile.write((char*)&x,sizeof(eroll));
    myfile.close();
    menu();
    }
  void sreachPatient()
  {
      cout<<"##############:"<<endl;
      int idToSearch;
      ifstream myfile;
    myfile.open("eroll.txt",ios::in);
    bool nofound=false;
    cout << "Enter the patient ID to search: "<<endl;
    cin >> idToSearch;
while(myfile.read((char*)&x,sizeof(eroll)))

   {
       if(x.id==idToSearch)
       {
           cout<<"name of patient: "<<x.name<<endl;
           cout<<"id of patient: "<<x.id<<endl;
           cout<<"age of patient: "<<x.age<<endl;
           cout<<"department of patient: "<<x.department<<endl;
           nofound=true;
       }

   }

        myfile.close();

    if(!nofound)
    {

            cout<<"this Patient not registered"<<endl;
    }
            menu();

  }
void displayPatient()
{
    cout<<"#######################23"<<endl;


     ifstream myfile;
    myfile.open("eroll.txt",ios::in);
    if(!myfile)
    {
        cout<<"error opening file"<<endl;
    }
    cout<<"================================================================="<<endl;
    cout<<"NAME OF PATIENT         ID OF PATIENT       DEPARTMENT      AGE  "<<endl;
    cout<<"================================================================="<<endl;
    while(myfile.read((char*)&x,sizeof(eroll)))
    {
        cout<<x.name<<setw(17)<<x.id<<setw(15)<<x.department<<setw(15)<<x.age<<endl;
    }
      myfile.close();
      menu();
}
