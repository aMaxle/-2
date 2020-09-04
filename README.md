# -2
#include <iostream>
#include <cstring>

using namespace std;

int bi[32]={0};
int octal[11] = {0};
char hexa[8] = {0};


int Power(int a,int b){      // a的b次方
    if(b==0)
        return 1;
    int sum=a;
    for (int i = 1; i < b;i++){
        sum = a * sum;
    }
    return sum;
}

void printBinary(int a){     // 输出二进制值
    int j=1;
    int cmpNum;
    if(a<0){
        int leap=1;
        a = abs(a);
        bi[0] = 1;
        for (int i = 30; i >=0;i--){
            cmpNum = Power(2, i);
            if(a>=cmpNum){
                bi[j]= 1;
                a = a - cmpNum;
                j++;
            }
            else if(a<cmpNum&&a>=0){
                bi[j] = 0;
                j++;
            }
        }
        for(int i=31;i>0;i--){
            if(leap){
                if(bi[i]==0)
                    continue;
                else {
                    leap = 0;
                    continue;
                }
            }
            else{
                if(bi[i] == 1)
                    bi[i] = 0;
                else 
                    bi[i] = 1;
            }
        }
    }
    else if(a>=0){
        bi[0] = 0;
        for (int i = 30; i >=0;i--){
            cmpNum = Power(2, i);
            if(a>=cmpNum){
                bi[j] = 1;
                a = a - cmpNum;
                j++;
            }
            else if(a<cmpNum&&a>=0){
                bi[j] = 0;
                j++;
            }
        }
    }
    cout << "二进制值：";
    if(bi[0]==1){
        for(int i=0;i<32;i++){
            cout<<bi[i];
            if(i==7||i==15||i==23)
                cout<<' ';
        }
    }
    else{
        int leap = 1;
        for(int i=0;i<32;i++){
            if(bi[i]==0&&leap){
                leap = 1;
                continue;
            }
            else{
                leap = 0;
                cout<<bi[i];
            }
        }
    }
    cout<<endl;
}

void printOct(int x[]){
    int m = 10, sum = 0, k = 0;
    for(int i=31;i>=0;i--){
        sum += x[i] * Power(2, k);
        if(i==0)
            octal[m] = sum;
        k++;
        if(k==3){
            k = 0;
            octal[m] = sum;
            m--;
            sum = 0;
        }
    }
    cout << "八进制值：";
    if(x[0]==1){
        for (int i = 0; i < 11;i++){
            cout << octal[i];
        }
    }
    else{
        for (int i = 0; i < 11;i++){
            if(octal[i]==0)
                continue;
            else
                cout << octal[i];
        }
    }
    cout << endl;
}

int getDec(char x[]){     // 十六进制转十进制的值
    int num=0;
    int j = 0;
    for (int i = 10; i >= 2;i--){
        if(x[i]>'9'){
            switch(x[i]){
                case 'a':
                    num += 10 * Power(16,j);
                    break;
                case 'A':
                    num += 10 * Power(16,j);
                    break;
                case 'b':
                    num += 11 * Power(16,j);
                    break;
                    num += 11 * Power(16,j);
                    break;
                case 'c':
                    num += 12 * Power(16,j);
                    break;
                case 'C':
                    num += 12 * Power(16,j);
                    break;
                case 'd':
                    num += 13 * Power(16,j);
                    break;
                case 'D':
                    num += 13 * Power(16,j);
                    break;
                case 'e':
                    num += 14 * Power(16,j);
                    break;
                case 'E':
                    num += 14 * Power(16,j);
                    break;
                case 'f':
                    num += 15 * Power(16,j);
                    break;
                case 'F':
                    num += 15 * Power(16,j);
                    break;
            }
            j++;
        }
        else if(x[i]>='0'&&x[i]<='9'){
            num += (x[i] - '0') * Power(16,j);
            j++;
        }
    }
    return num;
}

void printDec(int a){
    cout << "十进制值：" << a << endl;
}

void printHex(int x[]){
    memset(hexa, '0', sizeof(hexa));
	int m = 7, sum = 0, k = 0;
    for(int i=31;i>=0;i--){
        sum += bi[i] * Power(2, k);
        k++;
        if(k==4){
            k = 0;
            if(sum>9){
                switch(sum){
                    case 10:hexa[m]='A';
                    break;
                    case 11:hexa[m]='B';
                    break;
                    case 12:hexa[m]='C';
                    break;
                    case 13:hexa[m]='D';
                    break;
                    case 14:hexa[m]='E';
                    break;
                    case 15:hexa[m]='F';
                }
            }
            else
                hexa[m] = sum+'0';
            m--;
            sum = 0;
        }
    }
    cout << "十六进制值：0x";
    if(x[0]==1){
        for (int i = 0; i < 8;i++){
            cout << hexa[i];
        }
    }
    else if(x[0]==0){
        for (int i = 0; i < 8;i++){
            if(hexa[i]=='0')
                continue;
            cout << hexa[i];
        }
    }
    cout << endl;
} 

int main(){
    char x[100]={0};
    
    int y,bot,numDec=0,count=0;
    //while(1){
        cout <<"                       请选择功能" << endl;
        cout << "1.进制转换" << "     " << "2.进制四则运算" << "     " << "3.科学计算器" << "     " <<"0.退出程序"<< endl;
        cin >> y;
        if (y == 1){
    //        while(1){
    //            if(bot==2)
    //                break;
                cout << "请输入数字：";
                cin >> x;
                if ((x[0] == '0' && x[1] == 'x')||(x[0] == '0' && x[1] == 'X')){    // 十六进制
                    cout << "此数字是十六进制值" << endl;
                    int j = getDec(x);
                    printBinary(j);
                    printOct(bi);
                    printDec(j);
                    memset(bi, 0 , sizeof(bi));
                    memset(octal, 0 , sizeof(octal));
                }
                else{
                    int leap = 0;
                    if(x[0]=='-'){
                        leap = 1;
                    }
                    for (int i = 99; i >= 0;i--){
                        if(x[i]=='-')
                            continue;
                        if(x[i]){
                            numDec += (x[i] - '0') * Power(10, count);
                            count++;
                        }
                    }
                    if(leap)
                        numDec = - numDec;
                    cout << "此数字是十进制值" << endl;
                    printBinary(numDec);
                    printOct(bi);
                    printHex(bi);
                    memset(bi, 0 , sizeof(bi));
                    memset(hexa, 0, sizeof(hexa));
                }
    //          cout << "是否继续计算？ 1. 是            2.返回" << endl;
    //            cin >> bot;
            
        }
        else if (y == 2){
        }
        else if (y == 3){
        }
        else if(y==0)
    //        break;
    

    return 0;
}
