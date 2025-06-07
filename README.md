# Store-Computer-
#include<iostream>
#include<conio.h>
#include<iomanip>
#include<string>
#include<limits>
using namespace std;

const int MAX = 100;

class Computer {
private:
    string brand;
    string model;
    string description;
    int modelYear;
    double price;

public:
    void setData(string b, string m, string d, int y, double p) {
        brand = b;
        model = m;
        description = d;
        modelYear = y;
        price = p;
    }

    string getModel() { return model; }
    double getPrice() { return price; }
    string getBrand() { return brand; }
    string getDescription() { return description; }
    int getYear() { return modelYear; }

    void displayTableRow() {
        cout << "\t\t|" << left << setw(15) << brand
             << "|" << setw(15) << model
             << "|" << setw(25) << description
             << "|" << setw(10) << modelYear
             << "|" << right << fixed << setprecision(2) << "$" << setw(8) << price << "   |" << endl;
    }
};

void clearScreen();
void displayMenu();
void inputComputers(Computer[], int&);
void displayAll(Computer[], int);
void searchByModel(Computer[], int);
void editByModel(Computer[], int);
void deleteByModel(Computer[], int&);
void sortByPrice(Computer[], int);
void displayTableHeader();

int main() {
    Computer computers[MAX];
    int count = 0;
    int choice;

    do {
        clearScreen();
        displayMenu();
        cin >> choice;
        cin.ignore(numeric_limits<streamsize>::max(), '\n');

        switch (choice) {
            case 1:
                inputComputers(computers, count);
                clearScreen();
                cout << "\n\t\tCurrent list of computers after input:\n";
                displayAll(computers, count);
                cout << "\n\t\tPress Enter to continue...";
                cin.ignore();
                break;
            case 2:
                clearScreen();
                displayAll(computers, count);
                cout << "\n\t\tPress Enter to continue...";
                cin.ignore();
                break;
            case 3:
                clearScreen();
                searchByModel(computers, count);
                cout<<"\n\t\tPress Enter to continue...";
                cin.ignore();
                break;
            case 4:
                clearScreen();
                editByModel(computers, count);
                cout<<"\n\t\tPress Enter to continue...";
                cin.ignore();
                break;
            case 5:
                clearScreen();
                deleteByModel(computers, count);
                cout<<"\n\t\tPress Enter to continue...";
                cin.ignore();
                break;
            case 6:
                clearScreen();
                sortByPrice(computers, count);
                cout<<"\n\t\tPress Enter to continue...";
                cin.ignore();
                break;
            case 7:
                cout<<"\t\tExiting program.\n";
                break;
            default:
                cout<<"\t\tInvalid option. Try again.\n";
                cout<<"\n\t\tPress Enter to continue...";
                cin.ignore();
                break;
        }

    } while (choice != 7);

    return 0;
}

void clearScreen() {
    system("cls");
}

void displayMenu() {
    cout<<"\n\t\t===== Computer Menu ====="<< endl;
    cout<<"\t\t1. Input computer data"<<endl;
    cout<<"\t\t2. Display all computers"<<endl;
    cout<<"\t\t3. Search by model"<<endl;
    cout<< "\t\t4. Edit by model"<<endl;
    cout<< "\t\t5. Delete by model"<<endl;
    cout<< "\t\t6. Sort by price"<<endl;
    cout<< "\t\t7. Exit" <<endl;
    cout<< "\t\tChoose an option: ";
}

void displayTableHeader() {
    system("color 0A");
    cout << "\t\t+" << string(15, '-') << "+" << string(15, '-') << "+" << string(25, '-') << "+" << string(10, '-') << "+" << string(9, '-') << "+" << endl;
    cout << "\t\t|" << left << setw(15) << "Brand"
         << "|" << setw(15) << "Model"
         << "|" << setw(25) << "Description"
         << "|" << setw(10) << "Year"
         << "|" << "Price" << " |" << endl;
    cout << "\t\t+" << string(15, '-') << "+" << string(15, '-') << "+" << string(25, '-') << "+" << string(10, '-') << "+" << string(9, '-') << "+" << endl;
}

void inputComputers(Computer computers[], int &count) {
     system("color 9");
    int n;
    cout<<"\t\tHow many computers to add? " ;
    cin>>n;
    cin.ignore(numeric_limits<streamsize>::max(),'\n') ;

    for (int i = 0; i < n && count<MAX;i++,count++){
        string brand, model, description;
        int year;
        double price;

        cout<<"\n\t\t+-------------------------------+"<<endl;
        cout<<"\t\t|       Enter details for       |"<<endl;
        cout<<"\t\t|      Computer #" << count + 1 << "              |"<< endl;
        cout<<"\t\t+-------------------------------+"<<endl;

        cout<<"\t\t| Brand        : ";
        getline(cin,brand);fflush(stdin);cin.clear();
        cout<<"\t\t| Model        : ";
        getline(cin,model);fflush(stdin);cin.clear();
        cout<<"\t\t| Description  : ";
        getline(cin,description);fflush(stdin);cin.clear();
        cout<<"\t\t| Model Year   : ";
        cin>>year;fflush(stdin);cin.clear();
        cout<<"\t\t| Price ($)    : ";
        cin>>price;
        cin.ignore(numeric_limits<streamsize>::max(), '\n');
        cout<<"\t\t+-------------------------------+\n";

        computers[count].setData(brand, model, description, year, price);
    }
}

void displayAll(Computer computers[], int count) {
    if (count == 0) {
        cout << "\t\tNo computers to display.\n";
        return;
    }
    displayTableHeader();
    for (int i = 0; i < count; i++) {
        computers[i].displayTableRow();
    }
    cout<<"\t\t+"<<string(15, '-') <<"+" <<string(15, '-') <<"+"<<string(25,'-')<<"+"<<string(10, '-')<<"+"<<string(9, '-')<< "+"<<endl;
}

void searchByModel(Computer computers[], int count) {
     system("color 0B");
    string model;
    cout << "\t\tEnter model to search: ";
    getline(cin, model);
    bool found = false;
    displayTableHeader();
    for (int i = 0; i < count; i++) {
        if (computers[i].getModel() == model) {
            computers[i].displayTableRow();
            found = true;
        }
    }
    if (!found) {
        cout << "\t\tNo computers found with model: " << model << endl;
    }
    cout << "\t\t+" << string(15, '-') << "+" << string(15, '-') << "+" << string(25, '-') << "+" << string(10, '-') << "+" << string(9, '-') << "+" << endl;
}

void editByModel(Computer computers[], int count) {
    string model;
    cout << "\t\tEnter model to edit: ";
    getline(cin, model);
    bool found = false;
    for (int i = 0; i < count; i++) {
        if (computers[i].getModel() == model) {
            found = true;
            string brand, desc;
            int year;
            double price;
            cout<<"\t\tNew Brand: ";
			getline(cin, brand);fflush(stdin);cin.clear();
            cout<<"\t\tNew Description: ";
			getline(cin, desc);fflush(stdin);cin.clear();
            cout<<"\t\tNew Year: ";
			cin >> year;fflush(stdin);cin.clear();
            cout<<"\t\tNew Price: $";
			cin >> price;
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            computers[i].setData(brand, model, desc, year, price);
            cout << "\t\tUpdated successfully.\n";
            displayTableHeader();
            computers[i].displayTableRow();
            cout << "\t\t+" << string(15, '-') << "+" << string(15, '-') << "+" << string(25, '-') << "+" << string(10, '-') << "+" << string(9, '-') << "+" << endl;
            break;
        }
    }
    if (!found) {
        cout << "\t\tModel not found.\n";
    }
}

void deleteByModel(Computer computers[], int &count) {
     system("color 4");
    string model;
    cout << "\t\tEnter model to delete: ";
    getline(cin, model);
    for (int i = 0; i < count; i++) {
        if (computers[i].getModel() == model) {
            for (int j = i; j < count - 1; j++) {
                computers[j] = computers[j + 1];
            }
            count--;
            cout<<"\t\tDeleted successfully.\n";
            displayAll(computers, count);
            return ;
        }
    }
    cout<<"\t\tModel not found.\n";
}

void sortByPrice(Computer computers[], int count) {
    for (int i = 0; i < count - 1; i++) {
        for (int j = 0; j < count - i - 1; j++) {
            if (computers[j].getPrice() > computers[j + 1].getPrice()) {
                swap(computers[j], computers[j + 1]);
            }
        }
    }
    cout<<"\t\tSorted by price.\n";
    displayAll(computers, count);
}
