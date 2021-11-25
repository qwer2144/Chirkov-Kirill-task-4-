# Chirkov-Kirill-task-4-

#include <math.h>
#include <curses.h>
#include <locale>
#include <iostream>

using namespace std;

double X()
{
    double x;
    cout << "Введите значение аргумента : ";
    cin >> x;
    return x;
}

int N()
{
    int n;
    cout << "Введите число слагаемых : ";
    cin >> n;
    return n;
}

double E()
{
    double e;
    cout << "Введите точность вычислений : ";
    cin >> e;
    return e;
}

int Factorial(int n)
{
    int fac = 1;
    for (int i = 2; i <= n; fac *= i++);
    return fac;
}

double expression(int n, double x)
{
    return pow(-1, n + 1) * Factorial(2 * n) / ((2 * n - 1) * pow(Factorial(n), 2) * pow(4, n)) * pow(x, n);
}


int getN(double x, double e)
{
    int n = 0;
    int i = 0;
    while (abs(expression(i++, x)) > e) n++;
    return n;
}


double Sum(int n, double x, double e)
{
    double sum = 0;
    for (int i = 0; i <= n; i++) if (abs(expression(i, x)) > e) sum += expression(i,x);
    return sum;
}

double Last(int n, double x)
{
    double last = 1;
    for (int i = 0; i <= n; i++)
        last *= expression(i, x);
    return last;
}

double Numbererror(int n, double x, double e)
{
    return abs(Sum(n, x, e) - sqrt(x + 1));
}

double func(double x)
{
    return sqrt(x + 1);
}

void answer()
{
    double x;
    int n;
    cout << "Вычисление значений функции √(x+1)" << endl;
    cout << "Задание 1" << endl;
    x = X();
    n = N();
    cout << "Точное значение функции равно  " << func(x) << endl;
    cout << "Частичная сумма ряда равна " << Sum(n, x, 0) << endl;
    cout << "Aбсолютная погрешность равна " << Numbererror(n, x, 0) << endl;
    cout << "Последнее слагаемое равно " << Last(n, x) << endl;
    
    
    
    double e;
    cout << "Задание 2" << endl;
    x = X();
    e = E();
    cout << "Точное значение функции равно " << func(x) << endl;
    cout << "Частичная сумма ряда с заданной точностью равна " << Sum(getN(x, e), x, e) << endl;
    cout << "Учтено " << getN(x, e) << " членов ряда " << endl;
    cout << "Частичная сумма ряда с точностью, большей в  Е/10, равна " << Sum(getN(x, e/10), x, e/10) << endl;
    cout << "Учтено " << getN(x, e/10) << " членов ряда " << endl;
    
}

void menu()
{
    while (true)
    {
        double check;
        cout << "Выберите действие (1 - расчет, 0 - выход):";
        cin >> check;

        if (check == 0) break;
        else if (check == 1) answer();
    }
}


int main()
{
    setlocale(0,"");
    menu();
}
