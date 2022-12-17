

#define _CRT_SECURE_NO_WARNINGS

#include <iostream>

#include <string>
#include <cstring>
#include <cstdlib>

#include "Windows.h"

using namespace std;

class MyString {
public:
	MyString();
	MyString(char* new_str);

	~MyString();

	void set(char* new_str);

	void update();

	void print();

protected:
	char* str;
};

int main() {
	SetConsoleCP(1251);
	SetConsoleOutputCP(1251);

	char input[1024];
	cout << "Введите строку ниже:\n";
	cin >> input;

	MyString S(input);

	S.update();
	S.print();
	return 0;
}

MyString::MyString() {
	str = new char[1];
	str[0] = '\0';
}

MyString::MyString(char* new_str) {
	str = new char[strlen(new_str) + 1];
	strcpy(str, new_str);
}

MyString::~MyString() {
	delete[] str;
}

void MyString::set(char* new_str) {
	delete[] str;
	str = new char[strlen(new_str) + 1];
	strcpy(str, new_str);
}

void MyString::update() {
	if (strlen(str) % 3 == 0) {
		int count = 0;
		for (int i = 0; i < strlen(str); i++) {
			if ((str[i] == '0') || (str[i] == '3') || (str[i] == '6') || (str[i] == '9')) {
				count++;
			}
		}

		char* new_str = new char[strlen(str) + 1 - count];

		int delta = 0;
		for (int i = 0; i <= strlen(str); i++) {
			while ((str[i + delta] == '0') || (str[i + delta] == '3') || (str[i + delta] == '6') || (str[i + delta] == '9')) {
				delta++;
			}
			new_str[i] = str[i + delta];
		}

		delete[] str;
		str = new_str;
	}
}

void MyString::print() {
	cout << str << endl;
}
