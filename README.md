//Basic Calculator
#include <iostream>
#include <cstdlib>
#include <stack>
#include <cctype>
using namespace std;
double evaluate(& ins)
{
const char DECIMAL = '.';
const char RIGHT_PARENTHESIS = ')';
stack <double> numbers; //Stack that holds digits
stack <char> operations; //Stack that holds parenthesis and operators
char symbols;
double digits;
while (ins && ins.peek() !='n') //While next item in stack is not a space
{
	if (isdigit(ins.peek()) or (ins.peek() == DECIMAL)) //Checks if next input is a digit or decimal
	{
		ins >> digits; 
		numbers.push(digits); //Pushing number or decimal onto the numbers stack
	}
	else if (strchr("+-*/", ins.peek()) != NULL) // Searches for operators 
	{
		ins >> symbols;
		operations.push(symbols); // Push operator onto operations stack
	}
	else if (ins.peek() == RIGHT_PARENTHESIS)
	{
		ins.ignore()
		evaluatestack(numbers, operations);
	}
}
void evaluatestack(stack <double> & numbers, stack <char> & operations)//Receives numbers and characters by reference that are in the stack
{
double operand1, operand2;
operand2 = numbers.top();
numbers.pop(); //Display and pop the first element in numbers stack
operand1 = numbers.top(); 
numbers.pop(); // Display and pop the second element in numbers stack
switch (operations.top()) //Switch statement with selection variable being the operation stored in the operations stack
{	
	case '+': numbers.push(operand1 + operand2); // If addition, push the summation onto the numbers stack
		break;
	case '-': numbers.push(operand1 - operand2); // If subtraction, push the difference of the numbers onto the numbers stack 
		break;
	case '*': numbers.push(operand1 * operand2); // If multiplication, push the product of the operands onto the numbers stack
		break;
	case '/': numbers.push(operand1 / operand2); //If division, push the quotient of the operands onto the numbers stack !!!SHOULD THROW EXCEPTION IF DIVISION BY ZERO!!!
		break;
}
operations.pop(); //Display operation and pop the operation from the stack
}
int main()
{
	double answer;
cout << "Entered expression with balanced parenthesis";
cin >> input;
answer = evaluate(input);
cout << answer;
}
