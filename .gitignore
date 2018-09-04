#include <iostream>
#include <sstream>
#include <cmath>

using namespace std;

bool read(float ** &matrix, unsigned int &rows, unsigned int &columns)
{

bool result = true;
char op;
string string,string1;
getline(cin,string);
istringstream stream(string);
if(stream>>rows && stream>>op && op==',' && stream>>columns)
 {
	result = true;
 }
else return false;
matrix = new float*[rows];
for(unsigned int i =0; i<rows; i++)
 {
	matrix[i] = new float[columns];
	getline(cin,string1);
	istringstream stream(string1);
	for(unsigned int j=0; j<columns;j++)
	{
		if(!(stream>>matrix[i][j]))
		{
			result = false;
			break;
			
		}
	}
    
 }
  return result;
}

float ** sub(float ** matrix1, float ** matrix2, float ** &matrix, unsigned int rows, unsigned int columns) {
	matrix = new float *[rows];
	for (unsigned int i = 0; i < rows; i++) {
		matrix[i] = new float[columns];
		for (unsigned int j = 0; j < columns; j++) {
			matrix[i][j] = matrix1[i][j] - matrix2[i][j];
		}
	}
	return matrix;
}

float** add(float** matrix1, float** matrix2,float** &matrix, unsigned int rows, unsigned int columns)
{
 matrix= new float*[rows];
for(unsigned int i=0; i<rows; i++)
 {
 	matrix[i] = new float[columns];
 	for(unsigned int j=0; j<columns; j++)
 	{
 		matrix[i][j] = matrix1[i][j] + matrix2[i][j];
	 }
 }
 return matrix;
}

float ** trans(float ** matrix1, float ** &matrix, unsigned int rows, unsigned int columns) {
	matrix = new float *[columns];
	for (unsigned int i = 0; i < columns; i++) {
		matrix[i] = new float[rows];
		for (unsigned int j = 0; j < rows; j++) {
			matrix[i][j] = matrix1[j][i];
		}
	}
	return matrix;
}

float ** mult(float ** matrix1, float ** matrix2, float ** &matrix, unsigned int rows, unsigned int columns) {
	matrix = new float *[rows];
	for (unsigned int i = 0; i < rows; i++) {
		matrix[i] = new float[columns];
		for (unsigned int j = 0; j < columns; j++) {
			
			for (unsigned int k = 0; k< rows; k++) {
				matrix[i][j] += matrix1[i][k] * matrix2[k][j];
				 
			}
		}
	}
	return matrix;
}


void delete_memory(float ** matrix, unsigned int rows)
{
	for (unsigned int i = 0; i < rows; ++i) {
		delete[] matrix[i];
	}
	delete[] matrix;
}

void write(ostream & stream, float ** matrix, unsigned int rows, unsigned int columns) {
	stream << endl;
	for (unsigned int i = 0; i < rows; i++) {
		for (unsigned int j = 0; j < columns; j++) {
			if (matrix[i][j] == -0) {
				stream << 0 << " ";
			}
			else {
				stream << matrix[i][j] << " ";
			}
		}
		stream << endl;
	}
}

double determinant(float** array, unsigned int size) {
	unsigned int i, j;
	double opredelitel = 0;
	float** mat;
	if (size == 1) {
		opredelitel = array[0][0];
	}
	else if (size == 2) {
		opredelitel = array[0][0] * array[1][1] - array[0][1] * array[1][0];
	}
	else {
		mat = new float*[size - 1];
		for (i = 0; i<size; ++i) {
			for (j = 0; j<size - 1; ++j) {
				if (j<i)
					mat[j] = array[j];
				else
					mat[j] = array[j + 1];
			}
			opredelitel += pow((double)-1, (i + j))*determinant(mat, size - 1)*array[i][size - 1];
		}
		delete[] mat;
	}
	return opredelitel;
}

float ** gauss(float ** &matrix, float ** matrix1, int rows) {
	if (determinant(matrix1, rows) != 0) {
		float a, b, result;
		for (int i = 0; i < rows; i++) {
			matrix[i] = new float[rows];

			for (int j = 0; j < rows; j++) {
				matrix[i][j] = 0.0f;
				matrix[i][i] = 1.0f;
			}
		}
		for (int i = 0; i < rows; i++) {
			a = matrix1[i][i];
			for (int j = i + 1; j < rows; j++) {
				b = matrix1[j][i];
				for (int k = 0; k < rows; k++) {
					matrix1[j][k] = matrix1[i][k] * b - matrix1[j][k] * a;
					matrix[j][k] = matrix[i][k] * b - matrix[j][k] * a;
				}
			}
		}
		for (int i = 0; i < rows; i++) {
			for (int j = rows - 1; j > -1; j--) {
				result = 0.0f;
				for (int k = rows - 1; k > j; k--) {
					result += matrix1[j][k] * matrix[k][i];
					if (matrix1[j][j] == 0) {
						for (i = 0; i < rows; i++) {
							delete[] matrix[i];
						}
						delete[]matrix;
					}
				}
				matrix[j][i] = (matrix[j][i] - result) / matrix1[j][j];
			}
		}
		return matrix;
	}
	else {
		cout << "There is no reverse matrix" << endl;
		exit(0);
	}
}

int main() 
{
	unsigned int rows1 = 0, rows2 = 0, columns1 = 0, columns2 = 0;
	char op;
    float ** matrix1 = new float *[rows1];
	float ** matrix;
	if (read(matrix1, rows1, columns1))  
	{  
	    cin >> op;
		if (op == 'T') 
		{
			trans(matrix1, matrix, rows1, columns1);
			write(cout, matrix, columns1, rows1);
		}
	   else if (op == '+' && rows1==columns1)
	    {   cin.get();
		float ** matrix2 = new float *[rows2];
	    	read(matrix2,rows2,columns2);
	    	if( rows1==rows2 && columns2==columns1)
	    	 {
	    	 	add(matrix1,matrix2,matrix,rows1,columns1);
	    	 	write(cout, matrix, rows1,columns1);
	    	 	
			 }
			 else cout << "An error has occured while reading input data";
			 delete_memory(matrix2,rows1);
		}
		 
		  
		  else if (op == '-' && rows1==columns1)
	    {   cin.get();
		float ** matrix2 = new float *[rows2];
	    	read(matrix2,rows2,columns2);
	    	if( rows1==rows2 && columns2==columns1)
	    	 {
	    	 	sub(matrix1,matrix2,matrix,rows1,columns1);
	    	 	write(cout, matrix, rows1,columns1);
	    	 	
			 }
			 else cout << "An error has occured while reading input data";
			 delete_memory(matrix2,rows1);
		}

           
		   else if (op == '*' && rows1==columns1)
	    {   cin.get();
		float ** matrix2 = new float *[rows2];
	    	read(matrix2,rows2,columns2);
	    	if( rows1==rows2 && columns2==columns1)
	    	 {
	    	 	mult(matrix1,matrix2,matrix,rows1,columns1);
	    	 	write(cout, matrix, rows1,columns1);
	    	 	
			 }
			 else cout << "An error has occured while reading input data";
			 delete_memory(matrix2,rows1);
		}
		
		
		else if (rows1 == columns1 && op == 'R')
		 {  float **matrix3 = new float *[rows1];
		 	write(cout, gauss(matrix3, matrix1, rows1), rows1, columns1);
			 delete_memory(matrix3, rows1);
		 }	
		 else cout << "An error has occured while reading input data";
	
     
	
    }
	else cout << "An error has occured while reading input data";
    delete_memory(matrix1, rows1);	
}
