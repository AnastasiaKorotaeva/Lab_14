# Lab_14

#include "stdafx.h"
#include <iostream>
#include <fstream>
#include <stdlib.h>
#include <time.h>

using namespace std;

void setData(char*, double*, int);
void getData(char*, double*, int);
void setRandomValue(double*, int);
int Compare(char*, char*, int);

int main()
{
	srand(time(0));

	char* path1 = "text1.txt";
	char* path2 = "text2.txt";

	const int Length = 10;
	double arr1[Length];
	double arr2[Length];

	setRandomValue(arr1, Length);
	setRandomValue(arr2, Length);

	setData(path1, arr1, sizeof(arr1));
	setData(path2, arr2, sizeof(arr2));

	Compare(path1, path2, Length);

	system("pause");
	return 0;
}

void setRandomValue(double* arr, int len)
{
	for (double* i = arr; i < arr + len; i++)
	{
		*i = (double)rand() / rand();
	}
}

void setData(char* path, double* data, int size)
{
	ofstream outfile(path, ios::binary | ios::out);
	outfile.write((char*)data, size);
	outfile.close();
}

void getData(char* path, double* data, int size)
{
	ifstream infile(path, ios::binary | ios::in);
	infile.read((char*)data, size);
	infile.close();
}

int Compare(char* path1, char* path2, int len)
{
	double* arr1 = new double[len];
	double* arr2 = new double[len];

	int size = sizeof(double) * len;
	getData(path1, arr1, size);
	getData(path2, arr2, size);

	double sum1 = 0;
	double sum2 = 0;

	cout << "-----file1-----" << endl;
	for (double* i = arr1; i < arr1 + len; i++)
	{
		sum1 += *i;
		cout << *i << endl;
	}
	cout<< "sum1 = " << sum1 << endl << "---------------" << endl << endl;
	cout << "-----file2-----" << endl;
	for (double* i = arr2; i < arr2 + len; i++)
	{
		sum2 += *i;
		cout<< *i << endl;
	}
	cout<< "sum1 = " << sum2 << endl << "---------------" << endl << endl;

	if (sum1 == sum2)
	{
		cout << "file1 = file2" << endl;
		return 0;
	}
	else if (sum1 > sum2)
	{
		cout << "file1 > file2" << endl;
		return 0;
	}
	else
	{
		cout << "file1 < file2" << endl;
		return 0;
	}
}

