# MC
cdma 1:

import numpy as np
c1=[1,1,1,1]
c2=[1,-1,1,-1]
c3=[1,1,-1,-1]
c4=[1,-1,-1,1]
rc=[]
print("Enter the data bits :")
d1=int(input("Enter D1 :"))
d2=int(input("Enter D2 :"))
d3=int(input("Enter D3 :"))
d4=int(input("Enter D4 :"))
r1=np.multiply(c1,d1)
r2=np.multiply(c2,d2)
r3=np.multiply(c3,d3)
r4=np.multiply(c4,d4)
resultant_channel=r1+r2+r3+r4;
print("Resultant Channel",resultant_channel)
Channel=int(input("Enter the station to listen for C1=1 ,C2=2, C3=3 C4=4 : "))
if Channel==1:
    rc=c1
elif Channel==2:
    rc=c2
elif Channel==3:
    rc=c3
elif Channel==4:
    rc=c4
inner_product=np.multiply(resultant_channel,rc)
print("Inner Product",inner_product)
res1=sum(inner_product)
data=res1/len(inner_product)
print("Data bit that was sent",data)
------------------------------------------------------------------------------------------------------------------------------------------
4. octave code

clear
N = 10^6 % number of bits or symbols 
rand('state',100); % initializing the rand() function 
randn('state',200); % initializing the randn() function
% Transmitter
ip = rand(1,N)>0.5; % generating 0,1 with equal probability
s= 2*ip-1; % BPSK modulation 0 -> -1; 1 -> 1
n = 1/sqrt(2)*[randn(1,N) + j*randn(1,N)]; % white gaussian noise, 0dB variance
Eb_N0_dB = [-3:10]; % multiple Eb/N0 values
for ii = 1:length(Eb_N0_dB)
% Noise addition
y = s + 10^(-Eb_N0_dB(ii)/20)*n; % additive white gaussian noise
% receiver - hard decision decoding
ipHat = real(y)>0;
% counting the errors
nErr(ii) = size(find([ip- ipHat]),2);
end
simBer = nErr/N; % simulated ber
theoryBer = 0.5*erfc(sqrt(10.^(Eb_N0_dB/10))); % theoretical ber
% plot
close all
figure
semilogy(Eb_N0_dB,theoryBer,'b.-');
hold on
semilogy(Eb_N0_dB,simBer,'mx-');
axis([-3 10 10^-5 0.5])
grid on
legend('theory', 'simulation');
xlabel('Eb/No, dB');
ylabel('Bit Error Rate');
title('Bit error probability curve for BPSK modulation');
----------------------------------------------------------------------------------------------
8.to perform file transfer in client and server using tcp/ip
#Code For Server
import socket
import sys
server=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
server_address=('localhost',10000)
server.bind(server_address)
server.listen(1)
connection, client_address=server.accept()
file_name="Text.txt"
connection.sendall(file_name.encode())
file=open("Text.txt","rb")
data=file.read()
connection.sendall(data)
file.close()
connection.close()
server.close()
#Code For Client
import socket
import sys
client=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
server_address=('localhost',10000)
client.connect(server_address)
file_name=client.recv(1000).decode()
file_name="hello"+file_name
file=open(file_name,"wb")
data=client.recv(4097)
file.write(data)
file.close()
client.close()
-------------------------------------------------------------------------------------------------------
