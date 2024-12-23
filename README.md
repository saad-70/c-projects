#include"HospitalMember4.h"
#include <iostream>
#include <fstream>

using namespace std;

HospitalMember::HospitalMember(string iD, string name, string address, string contactNumber)

    : ID(iD), Name(name), Address(address), ContactNumber(contactNumber) {
}

string HospitalMember::getID() const
{
    return ID;
}

void HospitalMember::setID(const string& id)
{
    ID = id;
}


string HospitalMember::getName() const
{
    return Name;
}

void HospitalMember::setName(const string& name)
{
    Name = name;
}

string HospitalMember::getAddress() const
{
    return Address;
}

void HospitalMember::setAddress(const string& address)
{
    Address = address;
}

string HospitalMember::getContactNumber() const
{
    return ContactNumber;
}

void HospitalMember::setContactNumber(const string& contactNumber)
{
    ContactNumber = contactNumber;
}

bool HospitalMember::operator==(const HospitalMember& comp) const
{

    return ID == comp.ID;
}

bool HospitalMember::operator!=(const HospitalMember& comp) const
{
    return ID != comp.ID;
}

bool HospitalMember::operator>(const HospitalMember& comp) const
{
    return ID > comp.ID;
}

bool HospitalMember::operator<(const HospitalMember& comp) const
{
    return ID < comp.ID;
}

void HospitalMember::display(const string& HospitalMembers_dat) const {

    ofstream outFile(HospitalMembers_dat, ios::app);
    if (!outFile) {
        cout << "Error opening file for writing!" << endl;
        return;
    }
    outFile << *this;
    outFile.close();

        ifstream inFile(HospitalMembers_dat);
    if (!inFile) {
        cout << "Error opening file for reading!" << endl;
        return;
    }
}


    ostream& operator<<(ostream &os, const HospitalMember &member)
{
    os << "ID: " << member.ID << "\n"
        << "Name: " << member.Name <<"\n"
        << "Address: " << member.Address << "/n"
        << "Contact Number: " << member.ContactNumber << "\n";
    return os;
}




istream& operator>>(istream& is, HospitalMember& member) {
    cout << "enter ID : ";
    is >> member.ID;
    cout << "enter Name: " ;
    is >> member.Name;
    cout << "enter Address: " ;
    is >> member.Address;
    cout << "enter ContactNumber: " ;
    is >> member.ContactNumber;
    return is;
}



Doctor::Doctor(string iD, string name, string address, string contactNumber, string specialization, double salary)
    : HospitalMember(iD, name, address, contactNumber), Specialization(specialization), Salary(salary) {
}

string Doctor::getSpecialization() const
{
    return Specialization;
}

void Doctor::setSpecialization(const string& specialization)
{
    Specialization = specialization;
}

double Doctor::getSalary() const
{
    return Salary;
}

void Doctor::setSalary(double salary)
{
    Salary = salary;
}

Doctor& Doctor::operator++() {
    Salary *= 1.1;
    return *this;
}

Doctor& Doctor::operator--() {
    Salary *= 0.9;
    return *this;
}

ostream& operator<<(ostream& os, const Doctor& doctor) {

    os << static_cast<const HospitalMember&>(doctor);


    os << "Specialization: " << doctor.Specialization << endl
        << "Salary: " << doctor.Salary << endl;
    return os;
}
istream& operator>>(istream& is, Doctor& doctor) {
    is >> static_cast<HospitalMember&>(doctor);
    cout << "Enter Specialization: ";
    is.ignore(); 
    getline (is, doctor.Specialization);
    cout << "Enter Salary: ";
    is >> doctor.Salary;
    return is;
}




Surgeon::Surgeon(string iD, string name, string address, string contactNumber,
    string specialization, double salary, string suType, int years)
    : Doctor(iD, name, address, contactNumber, specialization, salary),
    SurgeryType(suType), YearsOfExperience(years) {
}




string Surgeon::getSurgeryType() const
{
    return SurgeryType;
}

void Surgeon::setSurgeryType(const string& surgeryType)
{

    SurgeryType = surgeryType;
}

int Surgeon::getYearsOfExperience() const
{
    return YearsOfExperience;
}

void Surgeon::setYearsOfExperience(int years)
{
    YearsOfExperience = years;
}
ostream& operator<<(ostream& os, const Surgeon& surgeon)
{

    os << static_cast<const Doctor&>(surgeon);
    os << endl << "Surgery Type : " << surgeon.SurgeryType << endl << "Years of Experience : "
        << surgeon.YearsOfExperience;
    return os;

}

istream& operator>>(istream& is, Surgeon& surgeon)
{

    is >> static_cast<Doctor&>(surgeon);
    cout << "Enter Surgery Type: ";
    is.ignore();
    getline(is, surgeon.SurgeryType);
    cout << "Enter Years of Experience: ";
    is >> surgeon.YearsOfExperience;
    return is;
}


GeneralPractitioner::GeneralPractitioner(string iD, string name, string address, string contactNumber,
    string specialization, double salary, int clinicHours, int patientLoad) :Doctor(iD, name, address, contactNumber, specialization, salary),
    ClinicHours(clinicHours), PatientLoad(patientLoad)
{
}

int GeneralPractitioner::getClinicHours() const
{
    return ClinicHours;
}

void GeneralPractitioner::setClinicHours(int hours)
{
    ClinicHours = hours;
}

int GeneralPractitioner::getPatientLoad() const
{
    return PatientLoad;
}

void GeneralPractitioner::setPatientLoad(int load)
{
    PatientLoad = load;
}

ostream& operator<<(ostream& os, const GeneralPractitioner& obj)
{
    os << static_cast<const Doctor&>(obj);
    os << "Clinic Hours: " << obj.ClinicHours << endl
        << "Patient Load: " << obj.PatientLoad << endl;
    return os;

}
istream& operator>>(istream& is, GeneralPractitioner& obj) {
    is >> static_cast<Doctor&>(obj);
    cout << "Enter Clinic Hours: ";
    is >> obj.ClinicHours;
    cout << "Enter Patient Load: ";
    is >> obj.PatientLoad;
    return is;
}

Nurse::Nurse(string iD, string name, string address, string contactNumber,
    string department,  double nurseSalary)

    : Doctor(iD, name, address, contactNumber), Department(department),
    NurseSalary(nurseSalary) {
}

string Nurse::getDepartment() const
{
    return Department;
}

void Nurse::setDepartment(const string& department)
{
    Department = department;

}

double Nurse::getNurseSalary() const
{
    return NurseSalary;
}

void Nurse::setNurseSalary(double& nurseSalary)
{
    NurseSalary = nurseSalary;
}


ostream& operator<<(ostream& os, const Nurse& nurse) {
    os << "ID: " << nurse.getID() << "\n"
        << "Name: " << nurse.getName() << "\n"
        << "Address: " << nurse.getAddress() << "\n"
        << "Contact Number: " << nurse.getContactNumber() << "\n";

    os << "Department: " << nurse.getDepartment() << "\n"
        << "Nurse Salary: " << nurse.getNurseSalary() << "\n";
    return os;
}


istream& operator>>(istream& is, Nurse& nurse) {
    is >> static_cast<Doctor&>(nurse);
    cout << "Enter Department: ";
    is >> nurse.Department;
    cout << "enter nurse Salary: ";
    is >> nurse.NurseSalary;
    return is;
}
void Nurse::display(const string& HospitalMembers_dat) const
{
    ofstream outFile(HospitalMembers_dat, ios::app);
    if (!outFile) {
        cout << "Error opening file for writing!" << endl;
        return;
    }
    outFile << *this;
    outFile.close();
}
Patient::Patient(string medicalRecordNumber, string illnessDescription, Doctor doctor)
    : MedicalRecordNumber(medicalRecordNumber), IllnessDescription(illnessDescription),
    doctorInCharge(doctor) {
}

string Patient::getMedicalRecordNumber() const
{
    return MedicalRecordNumber;
}

void Patient::setMedicalRecordNumber(const string& recordNumber)
{
    MedicalRecordNumber = recordNumber;
}

string Patient::getIllnessDescription() const
{
    return IllnessDescription;
}

void Patient::setIllnessDescription(const string& description)
{
    IllnessDescription = description;
}

Doctor Patient::getDoctorInCharge() const
{
    return doctorInCharge;;
}

void Patient::setDoctorInCharge(const Doctor& doctor)
{
    doctorInCharge = doctor;
}



ostream& operator<<(ostream& os, const Patient& patient) {
    os << "Medical Record Number: " << patient.MedicalRecordNumber << endl;
    os << "Illness Description: " << patient.IllnessDescription << endl;
    os << "Doctor in Charge: " << patient.doctorInCharge.getID() << " - " << patient.doctorInCharge.getName() << endl;
    return os;
}

istream& operator>>(istream& is, Patient& patient) {
    cout << "Enter Medical Record Number: ";
    is >> patient.MedicalRecordNumber;
    cout << "Enter Illness Description: ";
    is.ignore();
    getline(is, patient.IllnessDescription);
    cout << "Enter Doctor In Charge ID: ";
    string docID;
    is >> docID;
    patient.doctorInCharge.setID(docID);
    cout << "Enter Doctor In Charge Name: ";
    string docName;
    is.ignore();
    getline(is, docName);
    patient.doctorInCharge.setName(docName);
    return is;
}


void Doctor::display(const string& HospitalMembers_dat) const {
    ofstream outFile(HospitalMembers_dat, ios::app);
    if (!outFile) {
        cout << "Error opening file for writing!" << endl;
        return;
    }

    outFile << *this;  
    outFile.close();
};
void Patient::display(const string& HospitalMembers_dat) const {
    ofstream outFile(HospitalMembers_dat, ios::app);
    if (!outFile) {
        cout << "Error opening file for writing!" << endl;
        return;
    }
    outFile << *this;
    outFile.close();
}
