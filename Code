#include "L138_LCDK_aic3106_init.h"
#include "evmomapl138_gpio.h"
#include <stdio.h>
#include <math.h>
#include <string.h>
#define threshold 70000000000 

double left_sample = 0;
int j;
int i = 0;
int bincount = 0;
int ditdahcount = 0;
double input[320];
int binary[10];
int ditdah[25];
long long energy = 0;
int start = 0;
int flag = 0;
int onecount = 0;
int zerocount = 0;
int ddst = 0;
int length = 0;
int sinend = 0;
int sinst = 0;
char sentence[200];
int sentcount = 0;

interrupt void interrupt4(void) // interrupt service routine
{
	if (i > 20000){
		left_sample = input_left_sample() - 600;
		energy += (pow(left_sample, 2) - pow(input[i%320], 2));
		input[i % 320] = left_sample;
		if (input[i%320] < -20000){
			if (input[(i-6)%320] > 16000 && input[(i-12)%320] < -17000){
				sinend = 1;
			}
			if (input[(i-286)%320] < -17000 && input[(i-292)%320] > 16000){
				sinst = 1;
			}
		}
		if ((energy > threshold) && flag == 0 && sinend == 1 && sinst == 1){
			start = i - 320;
			flag = 1;
		}
		if (flag == 1 && sentcount == 0){
			for (j = 0; j < 200; j++){
				sentence[j] = '\0';
			}
		}
		if (flag == 1 && (i-start)%320 == 0){
			if (energy > threshold){
				binary[bincount%10] = 1;
				zerocount = 0;
				onecount++;
			}
			else{
				binary[bincount%10] = 0;
				onecount = 0;
				zerocount++;
			}
			if (onecount == 3){
				ditdah[(ditdahcount-1)%25] = 2;
			}
			else if (onecount == 1){
				ditdah[ditdahcount%25] = 1;
				ditdahcount++;
			}
			else if (zerocount == 7){
				ditdah[(ditdahcount-1)%25] = 4;
			}
			else if (zerocount == 3){
				ditdah[ditdahcount%25] = 3;
				ditdahcount++;
			}
			else if (zerocount > 7){
				ditdah[ditdahcount%25] = 5;
			}

			if (ditdah[(ditdahcount-1)%25] == 4){
				sentence[sentcount] = ' ';
				sentcount++;
			}
if((ditdah[(ditdahcount-1)%25] == 3) && (zerocount != 4 && zerocount != 5 && zerocount != 6 && zerocount != 7)){
				if (ddst != ditdahcount){
					length = ditdahcount - ddst - 1;
				}
				if (length == 1){
					if (ditdah[(ditdahcount-2)%25] == 1){
						sentence[sentcount] = 'e';
						sentcount++;
					}
					else{
						sentence[sentcount] = 't';
						sentcount++;
					}
				}
				else if (length == 2){
					if (ditdah[(ditdahcount-3)%25] == 1){
						if (ditdah[(ditdahcount-2)%25] == 1){
							sentence[sentcount] = 'i';
							sentcount++;
						}
						else{
							sentence[sentcount] = 'a';
							sentcount++;
						}
					}
					else{
						if (ditdah[(ditdahcount-2)%25] == 1){
							sentence[sentcount] = 'n';
							sentcount++;
						}
						else{
							sentence[sentcount] = 'm';
							sentcount++;
						}
					}
				}
				else if (length == 3){
					if (ditdah[(ditdahcount-4)%25] == 1){
						if (ditdah[(ditdahcount-3)%25] == 1){
							if (ditdah[(ditdahcount-2)%25] == 1){
								sentence[sentcount] = 's';
								sentcount++;
							}
							else{
								sentence[sentcount] = 'u';
								sentcount++;
							}
						}
						else{
							if (ditdah[(ditdahcount-2)%25] == 1){
								sentence[sentcount] = 'r';
								sentcount++;
							}
							else{
								sentence[sentcount] = 'w';
								sentcount++;
							}
						}
					}
					else{
						if (ditdah[(ditdahcount-3)%25] == 1){
							if (ditdah[(ditdahcount-2)%25] == 1){
								sentence[sentcount] = 'd';
								sentcount++;
							}
							else{
								sentence[sentcount] = 'k';
								sentcount++;
							}
						}
						else{
							if (ditdah[(ditdahcount-2)%25] == 1){
								sentence[sentcount] = 'g';
								sentcount++;
							}
							else{
								sentence[sentcount] = 'o';
								sentcount++;
							}
						}
					}
				}
				else if (length == 4){
					if (ditdah[(ditdahcount-5)%25] == 1){
						if (ditdah[(ditdahcount-4)%25] == 1){
							if (ditdah[(ditdahcount-3)%25] == 1){
								if (ditdah[(ditdahcount-2)%25] == 1){
									sentence[sentcount] = 'h';
									sentcount++;
								}
								else{
									sentence[sentcount] = 'v';
									sentcount++;
								}
							}
							else{
								sentence[sentcount] = 'f';
								sentcount++;
							}
						}
						else{
							if (ditdah[(ditdahcount-3)%25] == 1){
								sentence[sentcount] = 'l';
								sentcount++;
							}
							else{
								if (ditdah[(ditdahcount-2)%25] == 1){
									sentence[sentcount] = 'p';
									sentcount++;
								}
								else{
									sentence[sentcount] = 'j';
									sentcount++;
								}
							}
						}
					}
					else{
						if (ditdah[(ditdahcount-4)%25] == 1){
							if (ditdah[(ditdahcount-3)%25] == 1){
								if (ditdah[(ditdahcount-2)%25] == 1){
									sentence[sentcount] = 'b';
									sentcount++;
								}
								else{
									sentence[sentcount] = 'x';
									sentcount++;
								}
							}
							else{
								if (ditdah[(ditdahcount-2)%25] == 1){
									sentence[sentcount] = 'c';
									sentcount++;
								}
								else{
									sentence[sentcount] = 'y';
									sentcount++;
								}
							}
						}
						else{
							if (ditdah[(ditdahcount-2)%25] == 1){
								sentence[sentcount] = 'z';
								sentcount++;
							}
							else{
								sentence[sentcount] = 'q';
								sentcount++;
							}
						}
					}
				}
				ddst = ditdahcount;
			}
			bincount++;
		}
		if (ditdah[ditdahcount%25] == 5){
			ditdah[ditdahcount%25] = 0;
			energy = 0;
			sinst = 0;
			sinend = 0;
			flag = 0;
			sentcount = 0;
			length = 0;
			ddst = 0;
			onecount = 0;
			zerocount = 0;
			start = 0;
			i = 0;
			ditdahcount = 0;
			bincount = 0;
			for (j = 0; j < 10; j++){
				binary[j] = 0;
			}
			for (j = 0; j < 25; j++){
				ditdah[j] = 0;
			}
		}
	}
	i++;
	output_left_sample(0);
	return;
}
int main(void)
{
	for(j = 0; j < 320; j++){
		input[j] = 0;
	}
	for(j = 0; j < 10; j++){
		binary[j] = 0;
	}
	for(j = 0; j < 100; j++){
		ditdah[j] = 0;
	}
	for(j = 0; j < 200; j++){
		sentence[j] = '\0';
	}
	L138_initialise_intr(FS_8000_HZ,ADC_GAIN_12DB,DAC_ATTEN_0DB,LCDK_MIC_INPUT);
	while(1){}
}
