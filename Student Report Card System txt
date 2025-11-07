#include <iostream>
#include <fstream>
#include <iomanip>
using namespace std;

string subjectNames[6],name,ID;  
int subjectMarks[6],num_subjects;
string allsubject[10]={"MATH", "PHYSICS", "CHEMISTRY", "BIOLOGY","ENGLISH", "GEOGRAPHY", "HISTORY", "ECONOMICS","BUSINESS", "ACCOUNTING"};

float getTotal()
{
    float total = 0;
    for(int i = 0; i < num_subjects; i++)
    {
        total += subjectMarks[i];
    }
    return total;
}

float getAvg(float total)
{
    return total / num_subjects;
}

char getGrade(float avg)
{
    if (avg >= 80) return 'A';
    else if (avg >= 60) return 'B';
    else if (avg >= 40) return 'C';
    else if (avg >= 35) return 'D';
    else return 'E';
}
//Check IDduplicate
bool idExists(string idToCheck)
{
    fstream file("StudentRecords.txt", ios::in);
    string tempName, tempID;
    int tempSubCount;

    while (file >> tempName >> tempID >> tempSubCount)
    {
    	
        if (tempID == idToCheck)
        {
            file.close();
            return true;
        }
        //reads the rest on the file content
        for (int i = 0; i < tempSubCount; i++)
        {
            string sub; int mark;
            file >> sub >> mark;
        }
    }
    file.close();
    return false;
}

//Insert Student Record Function
void insert()
{
	fstream file;

    
    system("cls");
	cout<<"-------------------------\n | Add Student Details | \n-------------------------\n";
	cout<<"Enter Student Name (No Spacing)"<<endl;
	cin>>name;
	cout<<"Enter Student ID"<<endl;
	cin>>ID;
	// ID duplicate check
	if (idExists(ID))
	{
	    cout << "This Student ID already exists. Enter a different ID.\n";
	    return;
	}

	cout << "\nAvailable Courses:\n";
	for (int i = 0; i < 10; i++)
	{
	    cout << i+1 << ". " << allsubject[i] << endl;
	}
	
    cout << "Enter number of subjects you would like to enroll (Maximum 6): ";
    cin >> num_subjects;
    cout<<endl;

	//When users inputs wrong 
	    if (cin.fail()||num_subjects > 6)
		{
//			system("cls");
			cin.clear();
        	cin.ignore();
	        cout << "Invalid Input! Number of subjects cannot be more than 6." << endl;
	        return; 
	    }

	
	for (int i = 0; i < num_subjects; i++)
{
    int courseChoice;
    cout << "\nEnter Course Number " << i+1 << " (choose ONE from 1-10): ";
    cin >> courseChoice;

    if (cin.fail()||courseChoice < 1 || courseChoice > 10)
    {
    	cin.clear();
        cin.ignore();
        cout << "Course number doesnt exist \n";
        i--;
        continue;
    }

    //Duplicate check
	bool duplicate = false;
	for (int j = 0; j < i; j++)
	{
	    if (allsubject[courseChoice - 1] == subjectNames[j])
	    {
	        duplicate = true;
	        break;
	    }
	}
	
	if (duplicate)
	{
	    cout << "Course already selected. Choose a different subject.\n";
	    i--; 
	    continue;
	}

    subjectNames[i] = allsubject[courseChoice - 1];

    cout << "Enter Marks for " << subjectNames[i] << ": ";
    cin >> subjectMarks[i];

    if (cin.fail()||subjectMarks[i] < 0 || subjectMarks[i] > 100)
    {
    	cin.clear();
        cin.ignore();
        cout << "Marks must be between 0-100.\n";
        i--;
    }
}

	//File Savings
	file.open("StudentRecords.txt",ios::app|ios::out); //append or writing
	if (!file)
	{
		cout<<"Error Opening File! Sorry!\n";
		return;
	}
	
	 file << name << " " << ID << " " << num_subjects << " ";
    for (int i = 0; i < num_subjects; i++)
    {
        file << subjectNames[i] << " " << subjectMarks[i]<<" ";
        if (i != num_subjects - 1)
            file << "";
    }
    file << "\n";

    file.close();

	
	cout<<endl;
}

//Display Students
void display()
{
    system("cls");
    fstream file;
    int recordCount = 0,mark;

    cout << "-------------------------\n | Student Record Table | \n-------------------------\n";

    file.open("StudentRecords.txt", ios::in); // open for reading
    if (!file)
    {
        cout << "No Records Found!" << endl;
        return;
    }
	else
        {
        // Reading formatted line-by-line
        while (file >> name >> ID >> num_subjects)
        {
        	cout << "---------------" <<endl;
            cout << "Record No. " << ++recordCount << endl;
            cout << "---------------" <<endl;
            cout << "Name: " << name << endl;
            cout << "Student ID: " << ID << endl;
            cout << "Subjects & Marks:\n";

            for (int i=0;i<num_subjects;i++)
            {
                file>> subjectNames[i]>>subjectMarks[i];
                cout<< subjectNames[i]<<": "<<subjectMarks[i]<<endl;
            }
            cout<<endl;
        }
    if (recordCount == 0)
    {
        cout << "No Data Present..." << endl;
    }

    file.close();
		}
}

//Modify Student
void modify()
{
    system("cls");
    fstream file, file1;
    string IDmodify; 
    int found = 0,option;

    cout << "----------------------------\n | Student Modify Details | \n----------------------------\n";
    
    file.open("StudentRecords.txt", ios::in); // open for reading
    if (!file)
    {
        cout << "No Records Found!" << endl;
        return;
    }
	else
	{
    cout << "Enter ID of Student you want to Modify: ";
    cin >> IDmodify;
	cout<<endl;
    file1.open("record.txt", ios::out); // temporary file

    while (file >> name >> ID >> num_subjects)
    {
        string subjectNames[6];
        for (int i = 0; i < num_subjects; i++)
            file >> subjectNames[i] >> subjectMarks[i];

        if (ID == IDmodify)
        {
            found = 1;
            cout<<"===============\n";
            cout<<"Student Record\n";
            cout<<"===============\n";
            cout << "Name: " << name << endl;
            cout << "Student ID: " << ID << endl;
            cout << "Subjects & Marks:\n";

            for (int i=0;i<num_subjects;i++)
            {
                cout<< subjectNames[i]<<": "<<subjectMarks[i]<<endl;
            }
            cout<<endl;
            cout << "\nWhat would you like to modify?\n\n";
            cout<<"1.Name\n2.Student ID\n3.Subject & Marks\n4.Cancel\n\n";
            cout<<".......................\n";
            cout<<"Choose Option [1/2/3/4]\n";
            cout<<".......................\n";
			cin>>option;
			cin.clear();
			cin.ignore();
			
			switch(option){
				case 1:
					{
					cout<<"Enter Student Name (No Spacing)"<<endl;
					cin>>name;
					break;
					}
				case 2:
					{
					cout<<"Enter Student ID"<<endl;
					cin>>ID;
					//ID duplicate check
					if (ID!=IDmodify && idExists(ID))
					{
					    cout << "This Student ID already exists. Enter a different ID.\n";
					    file.close();
				        file1.close();
				        remove("record.txt");
					    return;
					}
					break;
					}
				case 3:
					{
					cout << "\nAvailable Courses:\n";
					for (int i = 0; i < 10; i++)
					{
					    cout << i+1 << ". " << allsubject[i] << endl;
					}
					
				    cout << "Enter number of subjects you would like to enroll (Maximum 6): ";
				    cin >> num_subjects;
				    cout<<endl;
					    if (cin.fail()||num_subjects > 6) 
						{
				//			system("cls");
							cin.clear();
				        	cin.ignore();
					        cout << "Invalid Input! Number of subjects cannot be more than 6." << endl;
				 			file.close();
				        file1.close();
				        remove("record.txt");
				
					        return; 
					    }
				
					for (int i = 0; i < num_subjects; i++)
				{
				    int courseChoice;
				    cout << "\nSelect Course " << i+1 << " (1-10): ";
				    cin >> courseChoice;
				
				    if (cin.fail()||courseChoice < 1 || courseChoice > 10)
				    {
				    	cin.clear();
				        cin.ignore();
				        cout << "Invalid choice. Try again.\n";
				        i--;
				        continue;
				    }
				
				    //Duplicate check
					bool duplicate = false;
					for (int j = 0; j < i; j++)
					{
					    if (allsubject[courseChoice - 1] == subjectNames[j])
					    {
					        duplicate = true;
					        break;
					    }
					}
					
					if (duplicate)
					{
					    cout << "Course already selected. Choose a different subject.\n";
					    i--; 
					    continue;
					}
				
				    subjectNames[i] = allsubject[courseChoice - 1];
				
				    cout << "Enter Marks for " << subjectNames[i] << ": ";
				    cin >> subjectMarks[i];
				
				    if (cin.fail()||subjectMarks[i] < 0 || subjectMarks[i] > 100)
				    {
				    	cin.clear();
				        cin.ignore();
				        cout << "Marks must be between 0-100.\n";
				        i--;                   
				
				    }
				}
				break;
							}
					case 4:
						{
							cout<<"Modify Cancelled.\n\n";
							break;
						}
					default:
						{
							cout<<"Sorry! Option Doesnt Exist!\n\n";
						}
					}
	


            // Write updated record
            file1 << name << " " << ID << " " << num_subjects << " ";
            for (int i = 0; i < num_subjects; i++)
                file1 << subjectNames[i] << " " << subjectMarks[i] << " ";
            file1 << "\n";

            cout << "\nRecord updated successfully.\n";
        }
        else
        {
            // Copy old record unchanged
            file1 << name << " " << ID << " " << num_subjects << " ";
            for (int i = 0; i < num_subjects; i++)
                file1 << subjectNames[i] << " " << subjectMarks[i] << " ";
            file1 << "\n";
        }
    }
	}	
	
    if (found == 0)
    {
    	system("cls");
        cout << "Student ID not found..." << endl;
    }
    
    file.close();
    file1.close();

    remove("StudentRecords.txt");
    rename("record.txt", "StudentRecords.txt");


}

//Search Student
void search()
{
	system("cls");
	fstream file;
	string IDsearch;
	int found = 0;
	cout << "-------------------------\n | Student Search Data | \n-------------------------\n";
	file.open("StudentRecords.txt", ios::in); // open for reading
    if (!file)
    {
        cout << "No Records Found!" << endl;
        return;
    }
    else
    {
    cout << "Enter ID of Student you want to Search: ";
    cin >> IDsearch;
    cout<<endl;
    while (file >> name >> ID >> num_subjects)
    {
        for (int i = 0; i < num_subjects; i++)
            file >> subjectNames[i] >> subjectMarks[i];

        if (ID == IDsearch)
        {
        	found=1;
        	cout << "Name: " << name << endl;
            cout << "Student ID: " << ID << endl;
            cout << "Subjects & Marks:\n";

            for (int i=0;i<num_subjects;i++)
            {
                cout<< subjectNames[i]<<": "<<subjectMarks[i]<<endl;
            }
            cout<<endl;
        }
	}
    
	if (found == 0)
    {
        cout << "No Student Found..." << endl;
    }

    file.close();

	}
}

//Delete
void deleted()
{
	system("cls");
	fstream file,file1;
	int found=0;
	string IDdeleted;
	cout<<"----------------------------\n | Delete Student Details | \n----------------------------\n";
	file.open("StudentRecords.txt",ios::in);
	if (!file)
    {
        cout << "No Records Found!" << endl;
        return;
    }
    else
    {
    	cout<<"Enter ID of Student which you want to Delete \n";
    	cin>>IDdeleted;
		cout<<endl;
    	file1.open("record.txt",ios::app | ios::out);
    while (file >> name >> ID >> num_subjects)
    {
        for (int i = 0; i < num_subjects; i++)
            file >> subjectNames[i] >> subjectMarks[i];
        if (ID != IDdeleted)
        {
        	// Write the record to file1 if it is NOT the one to delete
        	file1 << name << " " << ID << " " << num_subjects << " ";
		    for (int i = 0; i < num_subjects; i++)
		    {
		        file1 << subjectNames[i] << " " << subjectMarks[i]<<" ";
		        if (i != num_subjects - 1)
		            file1 << "";
		    }
		    file1 << "\n";
        }
        else
        {
        	found=1;
        	cout<<"Successfully Delete Student Record Data\n";
		}

	}
    
	if (found == 0)
    {
        cout << "No Student Found..." << endl;
    }
    file.close();
    file1.close();

    remove("StudentRecords.txt");
    rename("record.txt", "StudentRecords.txt");

	}
}
	
//Generate Repot
void generate_report()
{
	system("cls");
	fstream file;
	int found=0;
	string IDsearch;
	cout << "-------------------------------\n | Student Generate Report Card | \n-------------------------------\n";
	file.open("StudentRecords.txt",ios::in);
	if (!file)
    {
        cout << "No Records Found!" << endl;
        return;
    }
    else
    {
    cout << "Enter ID of Student you want to Generate Report Card: ";
    cin >> IDsearch;
    cout<<endl;
    system("cls");
    while (file >> name >> ID >> num_subjects)
    {
        for (int i = 0; i < num_subjects; i++)
            file >> subjectNames[i] >> subjectMarks[i];

        if (ID == IDsearch)
        {
        	found=1;
			float total = getTotal();
			float avg = getAvg(total);
			char grade = getGrade(avg);	
        	cout << "--------------------------------------------------------------------------------------------"<<endl;
        	cout<<"\t\t\t   INTI INTERNATIONAL COLLEGE PENANG"<<endl<<endl;
        	cout << "\t\t\t\t  STUDENT REPORT CARD "<<endl;
        	cout << "--------------------------------------------------------------------------------------------"<<endl;
        	cout<<"\t\t\t       --------------------------"<<endl;
        	cout<<"\t\t\t            PERSONAL DETAILS"<<endl;
        	cout<<"\t\t\t       --------------------------"<<endl<<endl;
        	cout << "\t\t\t   Name: " << name <<"\t\t";
            cout << "Student ID: " << ID << endl<<endl<<endl;
            cout<<"\t\t\t       --------------------------"<<endl;
        	cout<<"\t\t\t          ACADEMIC PERFORMANCE"<<endl;
        	cout<<"\t\t\t       --------------------------"<<endl<<endl;
            cout<<"\t\t    -------------------------------------------------"<<endl;
        	cout<<"\t\t                         MARKS"<<endl;
        	cout<<"\t\t    -------------------------------------------------"<<endl;

            for (int i=0;i<num_subjects;i++)
            {
                // cout<<"\t\t\t\t      " <<subjectNames[i]<<": "<<subjectMarks[i]<<endl;
                cout <<"\t\t\t "<<setw(20)<<subjectNames[i]<<": "<<subjectMarks[i]<<endl;
            }
            cout<<"\t\t\t\t -------------------\n    ";
			cout<<"\t\t\t\t      TOTAL: "<<total<<endl;
			cout<<"\t\t\t\t ------------------- \n ";  
            cout<<endl;
            
            cout<<"\t                -------------------        ------------\n";
            cout<<"\t                 PERCENTAGE: "<<fixed<< setprecision(0) <<avg<<"%"<<"           ";
            cout<<"  GRADE: "<<grade<<"\n";
            cout<<"\t                -------------------        ------------\n\n";


        }
	}
    
	if (found == 0)
    {
        cout << "No Student Found..." << endl;
    }

    file.close();
	}
	
}

//Main Functions
int main()
{

	int option;
	char answer;
	
	menu:
	{
		system("cls");
		cout<<"--------------------------------\n | Student Report Card System | \n--------------------------------\n";
		cout<<"1.Enter New Student Record\n2.Display All Student Record\n3.Modify Student Record\n4.Search Student Record"<<endl;
		cout<<"5.Delete Student Record\n6.Generate Student Report Card\n7.Exit"<<endl<<endl;
		cout<<".............................\nChoose Option:[1/2/3/4/5/6/7]\n............................."<<endl<<endl;
		cout<<"Enter Option: ";
		cin>>option;
		cin.clear();
		cin.ignore();
		system("cls");
		switch (option)
		{
			case 1: //Enter New Student Record
				{
					do
					{
						insert();
						cout<<"\nAdd Another Student Record? (Y/N): ";
						cin>>answer;
						cout<<endl;
					}while(answer=='Y'||answer=='y');
					break;
				}
			case 2: //Display All Student Record
				{
					
					display();
					break;
				}
			case 3: //Modify Student Record
				{
				 	do
					{
						modify();
						cout<<"\nModify Another Student Record? (Y/N): ";
						cin>>answer;
						cout<<endl;
					}while(answer=='Y'||answer=='y');	
					break;
				}
			case 4: //Search Student Record
				{
					do
					{
						search();
						cout<<"\nSearch Another Student Record? (Y/N): ";
						cin>>answer;
						cout<<endl;
					}while(answer=='Y'||answer=='y');
					
					break;
				}
			case 5: //Delete Student Record
				{
					do
					{
						deleted();
						cout<<"\nDelete Another Student Record? (Y/N): ";
						cin>>answer;
						cout<<endl;
					}while(answer=='Y'||answer=='y');
					break;
				}
			case 6: //Generate Student Report Card
				{
					do
					{
						generate_report();
						cout<<"\nGenerate Report for Another Student? (Y/N): ";
						cin>>answer;
						cout<<endl;
					}while(answer=='Y'||answer=='y');
					break;
				}
			case 7:
				{
					cout<<"Exiting Student Report Card System..."<<endl;
					return 0;
				}
			default:
				cout<<"Sorry! Option Doesn't Exist!"<<endl;
			
		}
		cout<<endl;
		system("pause");
	}
goto menu;
}

