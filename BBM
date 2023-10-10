//mbed-os-6
#include "mbed.h"

static BufferedSerial pc(USBTX,USBRX);//main - pc USB
static BufferedSerial im920(PA_9,PA_10);//main im - PC im//mainのUart tx,rxピンにつなぐ

Ticker status;
char str[1000];

int getmode();
void sendstatus();

int main()
{
    //設定
    pc.set_baud(9600);
    pc.set_format(8,BufferedSerial::None,1);
    
    im920.set_baud(9600);
    im920.set_format(8,BufferedSerial::None,1);

    wait_us(5000000);//5秒
    status.attach(sendstatus,5);//これちゃんと5秒毎になってる？

    //センサの割込み..一定時間ごとにの設定

    //ループさせて、pcと送受信し続ける
    while(1){
        int mode = getmode();
        sendstatus();
    }

}

int germode(){
    char temp;
    int i;
    while(temp != '\n'){//1サイクル目でwhileに入って改行までループ
    //これimが読み込めるようになるまで、mainでループし続ける気がする.割り込むからいいのか？
        if(im920.readable()){
            temp=im920.getc();
            str[i]=temp;
            i++
            if((str[i-2]==0)&&(str[i-1]==1)){
                return 1;//1モードへ変更の指示
            }
        }
    }

    return 0;//0モードへの変更指示
}

void sendstatus(){
    im920.printf("TXDA %d",mode);
    im920.printf("\r\n")
}
