# Learn Computer Science

## convert binary to decimal  

write binary value from right 
1, 2, 4, 8, 16, 32, 64...  

### example
101101  

101101 = 32, 16, 8, 4, 2, 1  

check "1" and plus them  

101101 = 32 + 8 + 4 + 1 = 45 

## convert decimal to binary

write binary value from right

512, 256, 128, 64, 32, 16, 8, 4, 2, 1  

### example
45  

decimal value 45  

sub decimal value by binary value from left  

if decimal value - binary value is negative value, write "0"    
if decimal value - binary value is positive value, write "1" and get decimal value - binary value

45 - 512 = negative  
45 - 256 = negative  
45 - 128 = negative  
45 - 64 = negative  
45 - 32 = positive  13 left  
13 - 16 = negative  
13 - 8 = positive left 5  
5 - 4 = positive 1 left  
1 - 2 = negative  
1 - 1 = positive 0 left  

that is  
512 = 0  
256 = 0  
128 = 0  
64 = 0  
32 = 1  
16 = 0  
8 = 1  
4 = 1  
2 = 0  
1 = 1  

convert decimal value 45 to binary value is 101101
