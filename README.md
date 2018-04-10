//# DES-by-sun
//This consists of DES algorithm implementation

#include<stdio.h>
#include<math.h>
unsigned char plt[8]={0x02,0x46,0x8a,0xce,0xec,0xa8,0x64,0x20};
unsigned char key[8]={0x0f,0x15,0x71,0xc9,0x47,0xd9,0xe8,0x59};
int pt[64]={
    58, 50, 42, 34, 26, 18, 10,  2,
    60, 52, 44, 36, 28, 20, 12,  4,
    62, 54, 46, 38, 30, 22, 14,  6,
    64, 56, 48, 40, 32, 24, 16,  8,
    57, 49, 41, 33, 25, 17,  9,  1,
    59, 51, 43, 35, 27, 19, 11,  3,
    61, 53, 45, 37, 29, 21, 13,  5,
    63, 55, 47, 39, 31, 23, 15,  7
};
unsigned char permuted[8]={0xff,0xff,0xff,0xff,0xff,0xff,0xff,0xff};
unsigned char left[4];
unsigned char right[4];

//methods--------------------------------------------------------------------------------------------------
void initialPermutation()
{
	int i=0;
	int j=0;
	int count=0;
	unsigned char c;
	for(i=0;i<8;i++)
	{
		for(j=0;j<8;j++)
		{
			int row=pt[count]/8;
			if(pt[count]%8==0)
			row=row-1;
			int col=(pt[count]%8);
			if(col!=0)
			col=col-1;
			else
			col=7;
			if(col==0)
			c=0x08&plt[row];
			if(col==1)
			c=0x40&plt[row];
			if(col==2)
			c=0x20&plt[row];
			if(col==3)
			c=0x10&plt[row];
			if(col==4)
			c=0x08&plt[row];
			if(col==5)
			c=0x04&plt[row];
			if(col==6)
			c=0x02&plt[row];
			if(col==7)
			c=0x01&plt[row];
			
			if(c==0x00)
			{
				if(j==0)
				permuted[i]=permuted[i]&0x7f;
				if(j==1)
				permuted[i]=permuted[i]&0xbf;
				if(j==2)
				permuted[i]=permuted[i]&0xdf;
				if(j==3)
				permuted[i]=permuted[i]&0xef;
				if(j==4)
				permuted[i]=permuted[i]&0xf7;
				if(j==5)
				permuted[i]=permuted[i]&0xfb;
				if(j==6)
				permuted[i]=permuted[i]&0xfd;
				if(j==7)
				permuted[i]=permuted[i]&0xfe;
			}
			count++;
		}
		printf(" %.02x ",permuted[i]);
	}
}
void leftRight()
{
	int i=0;
	for(i=0;i<4;i++)
	{
		left[i]=permuted[i];
	//	printf("%.02x ",left[i]);	
	}
	for(i=4;i<8;i++)
	{
		right[i]=permuted[i];
	//	printf("%.02x ",right[i]);
	}
}

int main()
{
	int i=0;
	initialPermutation();
	leftRight();	
}
