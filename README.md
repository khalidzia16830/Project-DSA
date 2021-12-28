# Project-DSA
=======================
#include <iostream>
  // which tells the compiler to include header file, named as string
#include <string>
  //  Vector is a template class in STL (Standard Template Library)
#include <vector>
  // ss means 'Stringstreams' which can be used to both read strings and write data into strings
#include <sstream>

using namespace std;


  // <int>-----> The string to convert into an integer and the base you want your data to be represented in
void Partition(long int no, vector <int> &vectPart)
{
	while (no>=1000) {
		int t=no%1000;
		vectPart.push_back(t);
		no/=1000;
	}
  // push_back() function is used to push elements into a vector from the back, and vect here represents vector
	vectPart.push_back(no);
}
// here we read the numbers from 0 till 19
string Read0_19(int no)
{
	if (no>=0 && no<=19) {
		vector<string> reading={
			"","one","two","three","four","five",
			"six","seven","eight","nine","ten",
			"eleven","twelve","thirteen","fourteen","fifteen",
			"sixteen","seventeen","eighteen","nineteen"};
		return reading[no];
	}
	else
		return "";
}
// read the numbers which are on tens position
string ReadTens(int loop)
{
	if (loop >=2 && loop <=9) {
		vector<string> reading={
			"","","twenty","thirty","fouty",
			"fifty","sixty", "seventy","eighty","ninety"};
		return reading[loop];
	}
	else
		return "";
}
// read of three means to read the number whose are on 100th position 
string ReadThreeDigits(int no)
{
  // stringstream which can be used to both read strings and write data into strings
	stringstream ss;
	int digit1=no/100;
	int digit2=(no%100)/10;
	int digit3=no%10;
// several conditions are gathered to work here like on hunderedth position and vice versa 
	if (digit1>0) ss << Read0_19(digit1) << " " << "hundred" << " ";
	if (digit2>0) {
		if (digit2==1) ss << Read0_19(digit2*10+digit3);
		else ss << ReadTens(digit2) << "-" << Read0_19(digit3);
	}
	if (digit2==0 && digit3!=0) ss << " " << Read0_19(digit3);

	return ss.str();
}
// in this function your number's are on thousand, million or billion's poistions positoned are convert here
string ReadNumber(long int num)
{
	vector<int> vectPart;
	vector<string> vectUnit={"","thousand","million","billion"};
	stringstream ss;
	Partition(num,vectPart);
	for (int i=vectPart.size()-1;i>=0;--i)
		ss << ReadThreeDigits(vectPart[i]) << " " << vectUnit[i] << " ";
	return ss.str();
}

// the main function
int main()
{
  // long means we can take an integer but having 64 bits means a large number **it can be in billions**
	long int number;
	cout << "Enter your number here in digits and you get in words: ";
	cin >> number;

	cout << ReadNumber(number);
}
  ============
  
