# Формируется матрица F следующим образом: если в С количество нулей в нечетных столбцах в области 1 больше, чем произведение чисел по периметру области 4, то поменять в С симметрично области 1 и 3 местами, иначе В и Е поменять местами несимметрично. При этом матрица А не меняется. После чего вычисляется выражение: ((К*Aт)*(F+А-F). Выводятся по мере формирования А, F и все матричные операции последовательно.

from random import randint
print('Введите N не меньше 6:', end=' ')
n = int(int(input()))
print('Введите K:', end=' ')
k = int(int(input()))
A = []
Atrans = []
Proizv = []
nul=0
proizv = 1
colich = 0
nado = 0
if n >= 6:
    for i in range(n):
        A.append([0]*n)
        Atrans.append([0] * n)
        Proizv.append([0] * n)
    print('Основная матрица')
    for i in range(len(A)):
        for j in range(len(A)):
            A[i][j] = randint(-10,10)
            print("{:4d}".format(A[i][j]), end = "")
        print()
    print()
    F = A
    if (n//2) % 2 != 0:
        for j in range(n//2, ((n//2)+n//4)+1):
            for i in range(0,n//4+1):
                if j % 2 != 0 and (i == (j- n//2) or i > (j- n//2)):
                    if F[i][j] == 0:
                        nul += 1
        for j in range(n//2, ((n//2)+n//4)):
            for i in range(n//4+1,n//2):
                if j % 2 != 0 and (i == ((n//2)-(j - (n // 2))) or i < ((n//2)-(j - (n // 2)))):
                    if F[i][j] == 0:
                        nul += 1
        for i in range((n // 4) + 1, n // 2):
            for j in range(n // 2, n):
                if i == j - (n // 2):
                    proizv = proizv * F[i][j]
        for i in range((n // 4), n // 2):
            for j in range(n // 2, n):
                if i == ((n // 2) - (j - (n // 2) + 1)):
                    proizv = proizv * F[i][j]
        for j in range((n // 2 + 1), n - 1):
            proizv = proizv * F[i][j]
    else:
        for j in range((n // 2), ((n // 2) + n // 4)):
            for i in range(1, (n // 4)+1):
                if j % 2 != 0 and (i == (j - (n // 2)) or i > (j - (n // 2))):
                    if F[i][j] == 0:
                        nul += 1
        print('')
        for j in range((n // 2)+1, ((n // 2) + n // 4)-1):
            for i in range((n // 4)+1 , (n // 2)-1):
                if j % 2 != 0 and (i == ((n // 2) - (j - (n // 2))) or i < ((n // 2) - (j - (n // 2)))):
                    if F[i][j] == 0:
                        nul += 1
        for i in range((n // 4), n // 2):
            for j in range(n // 2, n):
                if i == j - (n // 2):
                    proizv = proizv * F[i][j]
        for i in range((n // 4), n // 2):
            for j in range(n // 2, n):
                if i == ((n // 2) - (j - (n // 2) + 1)):
                    proizv = proizv * F[i][j]
        for j in range((n // 2 + 1), n - 1):
            proizv = proizv * F[i][j]
    print("Кол-во нулей:", nul)
    print("Произведение чисел:", proizv)
    print('')
    if nul > proizv:
        print("Меняем местами элементы в зависимости от результата сравнения:")
        for i in range(0,n//4+1):
            for j in range(0,n//4):
                if i == j or i > j:
                    F[i][j], F[i][((n//2)-1) - j] = F[i][((n//2)-1) - j],F[i][j]
        for i in range(n // 4 + 1,n//2):
            for j in range(0, n // 4):
                if i == (-(j - (n // 2))) or i < (-(j - (n // 2))):
                    F[i][j], F[i][-(j - (n // 2)+1)] = F[i][-(j - (n // 2)+1)], F[i][j]
        for i in range(len(F)):
            for j in range(len(F)):
                print("{:4d}".format(F[i][j]), end = "")
            print()
        print()
    elif nul < proizv and n % 2 == 0:
        print("Меняем местами элементы в зависимости от результата сравнения:")
        for i in range(0,n//2):
            for j in range(0, n // 2):
                F[i][j],F[i + n//2][j + n//2] = F[i + n//2][j + n//2],F[i][j]
        for i in range(len(F)):
            for j in range(len(F)):
                print("{:4d}".format(F[i][j]), end="")
            print()
        print()
    elif nul < proizv and n % 2 !=0:
        for i in range(0,n//2):
            for j in range(0, n // 2):
                F[i][j],F[i + n//2+1][j + n//2+1] = F[i + n//2+1][j + n//2+1],F[i][j]
        for i in range(len(F)):
            for j in range(len(F)):
                print("{:4d}".format(F[i][j]), end="")
            print()
        print()
    elif nul == proizv:
        colich +=1
        print("Кол-во нулей и произведение чисел равны")
    if colich == 0:
        print("K * A транспонированная")
        for i in range(len(F)):
            for j in range(len(F)):
                Atrans[i][j] = k * A[j][i]
                print("{:4d}".format(Atrans[i][j]), end="")
            print()
        print()
        print("(F + A - F)")
        for i in range(len(F)):
            for j in range(len(F)):
                print("{:4d}".format(A[i][j]), end="")
            print()
        print()
        for ch1 in range(n):
            for ch2 in range(n):
                for ch3 in range(n):
                    nado = nado + (A[ch1][ch3] * Atrans[ch3][ch2])
                Proizv[ch1][ch2] = nado
                nado = 0
        print("(К*Aт)*(F+А)")
        for i in range(len(F)):
            for j in range(len(F)):
                print("{:4d}".format(Proizv[i][j]), end="")
            print()
else:
    print("Введённое N некорректно")
