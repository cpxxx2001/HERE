#include<reg51.h>
sbit e=P2^7;
sbit rs=P2^6;
sbit rw=P2^5;
unsigned char m;
unsigned char code tab[8]={0x10,0x06,0x09,0x08,0x08,0x09,0x06,0x00};

void delayms(unsigned int ms)
{	
	unsigned int i,j;
	for(j=0;j<ms;j++)
	for(i=0;i<300;i++);
}

bit check_busy()
{	
	bit stat;
	rs=0;
	rw=1;
	e=0;
	delayms(1);
	e=1;
	delayms(1);
	stat=P0&0X80;
	e=0;
	delayms(1);
	return stat;	
}

	void lcdcom(unsigned char com)
	{
		while(check_busy());
		rs=0;//写指令和地址
		rw=0;//写
		e=0;
		delayms(1);
		P0=com;
		e=1;
		delayms(1);
		e=0;
		delayms(1);	
	}
	void lcddat(unsigned char dat)
	{
		while(check_busy());
		rs=1;//数据
		rw=0;//写
		e=0;
		delayms(1);
		P0=dat;
		e=1;
		delayms(1);
		e=0;
		delayms(1);	
	}



void main()
{	
	lcdcom(0x01);//清屏
	lcdcom(0x01);//光标右移，显存地址加一
	lcdcom(0x0e);//显示打开，有光标，光标不闪烁
	lcdcom(0x38);//8位数据总线，2行显示，5*7字符

	lcdcom(0x40);  //CGRAM地址，自定义字符的第一个地址
	for(m=0;m<8;m++)
	lcddat(tab[m]);
	
	lcdcom(0x80);
	lcddat('2');
	lcddat('0');
	lcddat('.');
	lcddat('5');
	lcddat(0x00);//温度c在CGROM中的地址
	while(1);	
}
