# Lab_2.2
Lab_2.2 Радецький Ре-22


```ruby

#include <Windows.h>
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

double integral_l_re(double left_boundary_a, double right_boundary_b, unsigned int intervals);
double integral_r_re(double left_boundary_a, double right_boundary_b,  unsigned int intervals);
double integral_trapecia(double left_boundary_a, double right_boundary_b,  unsigned int intervals);
double integral_Simps (double left_boundary_a, double right_boundary_b, unsigned int intervals);
double integrand( double x );


int main() {

    int left_boundary_a = 0, right_boundary_b = 1;
    double measurement_error = 0, i1 = 0, i2 = 0;
    int intervals, var, i;
    double integral_s = 0;

  SetConsoleOutputCP(1251);
  SetConsoleCP(1251);
  while (1) {

    printf("\n ліва границя = ");
    scanf("%d", &left_boundary_a);
    printf("\n права границя = ");
    scanf("%d", &right_boundary_b);

    do {
      printf("\n Введіть кількість інтервалів розділення (N>0) N= ");
      scanf("%u", &intervals);
    } while (intervals <= 0);


    do {
      printf("\n Виберіть спосіб розрахунку:\n");
      printf("\t1. метод лівих трикутників:\n");
      printf("\t2. метод правих трикутників:\n");
      printf("\t3. метод трапеції :\n");
      printf("\t4. метод параболи :\n");
      scanf("%u", &var);
      if (var != 1 && var != 2 && var != 3 && var != 4){
        printf("\n помилка введення данних \n");
      }
    } while (var != 1 && var != 2 && var != 3 && var != 4);

    system("cls");

    switch (var) {
      case 1:
        integral_s = integral_l_re(left_boundary_a, right_boundary_b, intervals);
        printf("\n\n\t*метод лівих трикутників*\n");
        printf("\n\ta = %d \n\tb = %d \n\tIntegral = %.8lf \n\tN = %d \n\n", left_boundary_a, right_boundary_b, integral_s, intervals);
        break;
      case 2:
        integral_s = integral_r_re(left_boundary_a, right_boundary_b, intervals);
        printf("\n\n\t======*метод правих трикутників*======\n");
        printf("\n\ta = %d \n\tb = %d \n\tIntegral = %.8lf \n\tN = %d \n\n", left_boundary_a, right_boundary_b , integral_s, intervals);
        break;
      case 3:
        integral_s = integral_trapecia(left_boundary_a, right_boundary_b, intervals);
        printf("\n\n\t======*метод трапеції *======\n");
        printf("\n\ta = %d \n\tb = %d \n\tIntegral = %.8lf \n\tN = %d \n\n", left_boundary_a, right_boundary_b, integral_s, intervals);
        break;
      case 4:
        integral_s = integral_Simps(left_boundary_a, right_boundary_b, intervals);
        printf("\n\n\t======*метод параболи *======\n");
        printf("\n\ta = %d \n\tb = %d \n\tIntegral = %.8lf \n\tN = %d \n\n", left_boundary_a, right_boundary_b, integral_s, intervals);
        break;
    }

    return 0;
  }
}
double integral_l_re(double left_boundary_a, double right_boundary_b, unsigned int intervals) {
  double integral_s = 0, x = 0, y;
  unsigned int i;
  y = (right_boundary_b - left_boundary_a) / intervals;
  x = left_boundary_a;
  for (i = 0; i <= (intervals - 1); i++) {
    integral_s += integrand(x);
    x += y;
  }
  return integral_s * y;
}
double integral_r_re(double left_boundary_a, double right_boundary_b, unsigned int intervals) {
  double integral_s = 0, x = 0, y;
  unsigned int i;
  y = (right_boundary_b - left_boundary_a) / intervals;
  x = left_boundary_a + y;
  for (i = 0; i <= intervals; i++) {
    integral_s += integrand(x);
    x += y;
  }
  return integral_s * y;
}
double integral_trapecia(double left_boundary_a, double right_boundary_b, unsigned int intervals) {
  double integral_s = 0, x = 0, y;
  unsigned int i;
  y = (right_boundary_b - left_boundary_a) / intervals;
  x = left_boundary_a + y;
  for (i = 0; i <= (intervals - 1); i++) {
    integral_s += (integrand(x) + integrand(x + y)) / 2;
    x += y;
  }
  return integral_s * y;
}
double integral_Simps(double left_boundary_a, double right_boundary_b, unsigned int intervals) {
  double integral_s = 0, sum1 = 0, sum2 = 0, y = 0;
  y = (right_boundary_b - left_boundary_a) / intervals;
  for (int i = 1; i <= (intervals - 1); i++) {
    if (i % 2 != 0) {
      sum1 += integrand(left_boundary_a + y * i);
    }
    else {
      sum2 += integrand(left_boundary_a + y * i);
    }
  }
  return (integrand(left_boundary_a) + integrand(right_boundary_b) + 4 * sum1 + 2 * sum2) * y / 3;
}
double integrand(double x ) {
  return (pow(x,3)/20)- 5 * pow(x,2) + 1000;
}


```
