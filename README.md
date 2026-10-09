# SignalsMatlab1

# Enter your code here

# Time Invariance Tests
close all;

% Step function input (shift = 2s)
fs = 1000;
t = 0:1/fs:10;              

x = zeros(size(t));          
x(t >= 2) = 1;               

y = balancesim(x, fs, 40);   

x2 = zeros(size(t));
x2(t>=4) = 1;
y2 = balancesim(x2,fs,40);

figure;
plot(t, y,"r","LineWidth",1.5); hold on;
plot((t-2), y2,"b--","LineWidth",2);
title("Output Overlap (2s Shift)");
legend("y(t)","y2(t)");
xlabel('Time(s)');
ylabel('Angle(degrees');

% Step function input (shift = 6s)

x3 = zeros(size(t));
x3(t >= 8) = 1;
y3 = balancesim(x3, fs, 40);

figure;
plot(t, y,"r","LineWidth",1.5); hold on; 
plot((t-6),y3, "b--","LineWidth",2);
title('Output Overlap (6s Shift)');
legend('y(t)', 'y3(t)');
xlabel('Time(s)');
ylabel('Angle(degrees');

% Sin function input (shift = -1s, f = 0.5Hz)

x_sin = sin(2*pi*0.5*t);
y_sin = balancesim(x_sin,fs,40);

x_sinshift = sin(2*pi*0.5*(t+1));
y_sinshift = balancesim(x_sinshift,fs,40);

figure;
plot(t, y_sin,"r","LineWidth",1.5); hold on; 
plot((t+1), y_sinshift,"b--","LineWidth",2);
title("Output Overlap (-1s Shift)");
legend("ysin(t)","ysinshift(t)");
xlabel('Time(s)');
ylabel('Angle(degrees');

% Cosine function input (shift = -1s, f = 0.1Hz)\

xcos = cos(2*pi*0.1*t);
ycos = balancesim(xcos,fs,40);

xcosshift = cos(2*pi*0.1*(t+1));
ycosshift = balancesim(xcosshift,fs,40);

figure;
plot(t, ycos,"r","LineWidth",1.5); hold on; 
plot((t+1),ycosshift,"b--","LineWidth",2);
title("Output Overlap (-1s Shift)");
legend("ycos(t)","ycosshift(t)");
xlabel('Time(s)');
ylabel('Angle(degrees');

% Longer time scale TI test with sin function
% Ages: 20, 50, and 80

x = sin(2*pi*0.5*t);
y20 = balancesim(x,fs,20);
y50 = balancesim(x,fs,50);
y80 = balancesim(x,fs,80);

figure;
plot(t,y20,"m","LineWidth",1.5); hold on;
plot(t,y50,"b--","LineWidth",1.5);
plot(t,y80,"r:","LineWidth",1.5);
legend("Age 20","Age 50","Age 80");
title("Output Overlap (Ages 20, 50 , 80)");
xlabel('Time(s)');
ylabel('Angle(degrees');
