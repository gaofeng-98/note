+ echo 2 > /proc/irq/62/smp_affinity
+ echo 3 > /proc/irq/63/smp_affinity

# TCP_TX_MTU1500
```
#commands in a_test_eth.sh
echo "SERVER_IP is 192.168.1.2"
iperf3 -c 192.168.1.2 -p 5201 -i 60 -t 60 -b 2500M -Z -T 5201 -A 2 &
iperf3 -c 192.168.1.2 -p 5202 -i 60 -t 60 -b 2500M -Z -T 5202 -A 3 &
mpstat -P ALL 1 40
```
<details>
<summary>terminal log</summary>

```
./a_test_eth.sh  
SERVER_IP is 192.168.1.2
5201:  Connecting to host 192.168.1.2, port 5201
5202:  Connecting to host 192.168.1.2, port 5202
5202:  [  5] local 192.168.1.10 port 48816 connected to 192.168.1.2 port 5202
5201:  [  5] local 192.168.1.10 port 45190 connected to 192.168.1.2 port 5201
```
</details>


<details>
<summary>cpu load</summary>

```
Average:     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest   %idle
Average:     all    0.19    0.00   26.42    0.00    0.00    9.73    0.00    0.00   63.65
Average:       0    0.00    0.00    0.00    0.00    0.00   10.82    0.00    0.00   89.18
Average:       1    0.04    0.00    0.14    0.00    0.00   12.77    0.00    0.00   87.06
Average:       2    0.36    0.00   47.35    0.00    0.00    7.54    0.00    0.00   44.76
Average:       3    0.28    0.00   43.56    0.00    0.00    8.96    0.00    0.00   47.20  
```
</details>
 
<details>
<summary>performance</summary>

```
5202:  [ ID] Interval           Transfer     Bitrate         Retr  Cwnd
5202:  [  5]   0.00-60.00  sec  6.38 GBytes   914 Mbits/sec    3   2.77 MBytes       
5202:  - - - - - - - - - - - - - - - - - - - - - - - - -
5202:  [ ID] Interval           Transfer     Bitrate         Retr
5202:  [  5]   0.00-60.00  sec  6.38 GBytes   914 Mbits/sec    3             sender
5202:  [  5]   0.00-60.00  sec  6.38 GBytes   914 Mbits/sec                  receiver
5202:  
5202:  iperf Done.

5201:  [ ID] Interval           Transfer     Bitrate         Retr  Cwnd
5201:  [  5]   0.00-60.01  sec  7.99 GBytes  1.14 Gbits/sec    2   2.92 MBytes       
5201:  - - - - - - - - - - - - - - - - - - - - - - - - -
5201:  [ ID] Interval           Transfer     Bitrate         Retr
5201:  [  5]   0.00-60.01  sec  7.99 GBytes  1.14 Gbits/sec    2             sender
5201:  [  5]   0.00-60.01  sec  7.99 GBytes  1.14 Gbits/sec                  receiver
5201:  
5201:  iperf Done.  
```
</details>


 












# UDP_TX_MTU_1500
```
#commands in a_test_eth.sh
echo "SERVER_IP is 192.168.1.2"
iperf3 -u -P 2 -c 192.168.1.2 -p 5201 -i 60 -t 60 -b 2500M -Z -T 5201 -A 0 &
sleep 1s
iperf3 -u -P 2 -c 192.168.1.2 -p 5202 -i 60 -t 60 -b 2500M -Z -T 5202 -A 1 &
sleep 1s
iperf3 -u -P 2 -c 192.168.1.2 -p 5203 -i 60 -t 60 -b 2500M -Z -T 5203 -A 2 &
sleep 1s
iperf3 -u -P 2 -c 192.168.1.2 -p 5204 -i 60 -t 60 -b 2500M -Z -T 5204 -A 3 &
sleep 1s
mpstat -P ALL 1 40
```

<details>
<summary>terminal log</summary>

```
./a_test_eth.sh 
SERVER_IP is 192.168.1.2
5201:  Connecting to host 192.168.1.2, port 5201
5201:  [  5] local 192.168.1.10 port 54417 connected to 192.168.1.2 port 5201
5201:  [  7] local 192.168.1.10 port 50678 connected to 192.168.1.2 port 5201
5202:  Connecting to host 192.168.1.2, port 5202
5202:  [  5] local 192.168.1.10 port 50488 connected to 192.168.1.2 port 5202
5202:  [  7] local 192.168.1.10 port 56364 connected to 192.168.1.2 port 5202
5203:  Connecting to host 192.168.1.2, port 5203
5203:  [  5] local 192.168.1.10 port 55263 connected to 192.168.1.2 port 5203
5203:  [  7] local 192.168.1.10 port 42296 connected to 192.168.1.2 port 5203
5204:  Connecting to host 192.168.1.2, port 5204
5204:  [  5] local 192.168.1.10 port 60722 connected to 192.168.1.2 port 5204
5204:  [  7] local 192.168.1.10 port 44425 connected to 192.168.1.2 port 5204  
```
</details>

<details>
<summary>cpu load</summary>

```
Average:     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest   %idle
Average:     all   10.49    0.00   79.30    0.00    0.00   10.20    0.00    0.00    0.00
Average:       0   12.97    0.00   86.78    0.00    0.00    0.25    0.00    0.00    0.00
Average:       1    3.22    0.00   56.49    0.00    0.00   40.29    0.00    0.00    0.00
Average:       2   12.68    0.00   87.15    0.00    0.00    0.18    0.00    0.00    0.00
Average:       3   13.12    0.00   86.78    0.00    0.00    0.10    0.00    0.00    0.00  
```
</details>

<details>
<summary>performance</summary>

```
5201:  [ ID] Interval           Transfer     Bitrate         Total Datagrams
5201:  [  5]   0.00-60.00  sec  3.30 GBytes   472 Mbits/sec  2445197  
5201:  [  7]   0.00-60.00  sec  3.30 GBytes   472 Mbits/sec  2445197  
5201:  [SUM]   0.00-60.00  sec  6.59 GBytes   944 Mbits/sec  4890394  
5201:  - - - - - - - - - - - - - - - - - - - - - - - - -
5201:  [ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
5201:  [  5]   0.00-60.00  sec  3.30 GBytes   472 Mbits/sec  0.000 ms  0/2445197 (0%)  sender
5201:  [  5]   0.00-60.00  sec  3.30 GBytes   472 Mbits/sec  0.018 ms  1569/2445197 (0.064%)  receiver
5201:  [  7]   0.00-60.00  sec  3.30 GBytes   472 Mbits/sec  0.000 ms  0/2445197 (0%)  sender
5201:  [  7]   0.00-60.00  sec  3.30 GBytes   472 Mbits/sec  0.018 ms  1559/2445197 (0.064%)  receiver
5201:  [SUM]   0.00-60.00  sec  6.59 GBytes   944 Mbits/sec  0.000 ms  0/4890394 (0%)  sender
5201:  [SUM]   0.00-60.00  sec  6.59 GBytes   944 Mbits/sec  0.018 ms  3128/4890394 (0.064%)  receiver
5201:  
5201:  iperf Done.

5202:  [ ID] Interval           Transfer     Bitrate         Total Datagrams
5202:  [  5]   0.00-60.00  sec   818 MBytes   114 Mbits/sec  592697  
5202:  [  7]   0.00-60.00  sec   818 MBytes   114 Mbits/sec  592697  
5202:  [SUM]   0.00-60.00  sec  1.60 GBytes   229 Mbits/sec  1185394  
5202:  - - - - - - - - - - - - - - - - - - - - - - - - -
5202:  [ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
5202:  [  5]   0.00-60.00  sec   818 MBytes   114 Mbits/sec  0.000 ms  0/592697 (0%)  sender
5202:  [  5]   0.00-60.00  sec   818 MBytes   114 Mbits/sec  0.022 ms  44/592697 (0.0074%)  receiver
5202:  [  7]   0.00-60.00  sec   818 MBytes   114 Mbits/sec  0.000 ms  0/592697 (0%)  sender
5202:  [  7]   0.00-60.00  sec   818 MBytes   114 Mbits/sec  0.022 ms  40/592697 (0.0067%)  receiver
5202:  [SUM]   0.00-60.00  sec  1.60 GBytes   229 Mbits/sec  0.000 ms  0/1185394 (0%)  sender
5202:  [SUM]   0.00-60.00  sec  1.60 GBytes   229 Mbits/sec  0.022 ms  84/1185394 (0.0071%)  receiver
5202:  
5202:  iperf Done.

5203:  [ ID] Interval           Transfer     Bitrate         Total Datagrams
5203:  [  5]   0.00-60.00  sec  3.37 GBytes   483 Mbits/sec  2501539  
5203:  [  7]   0.00-60.00  sec  3.37 GBytes   483 Mbits/sec  2501539  
5203:  [SUM]   0.00-60.00  sec  6.75 GBytes   966 Mbits/sec  5003078  
5203:  - - - - - - - - - - - - - - - - - - - - - - - - -
5203:  [ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
5203:  [  5]   0.00-60.00  sec  3.37 GBytes   483 Mbits/sec  0.000 ms  0/2501539 (0%)  sender
5203:  [  5]   0.00-60.00  sec  3.37 GBytes   483 Mbits/sec  0.024 ms  1751/2501539 (0.07%)  receiver
5203:  [  7]   0.00-60.00  sec  3.37 GBytes   483 Mbits/sec  0.000 ms  0/2501539 (0%)  sender
5203:  [  7]   0.00-60.00  sec  3.37 GBytes   483 Mbits/sec  0.024 ms  1772/2501539 (0.071%)  receiver
5203:  [SUM]   0.00-60.00  sec  6.75 GBytes   966 Mbits/sec  0.000 ms  0/5003078 (0%)  sender
5203:  [SUM]   0.00-60.00  sec  6.74 GBytes   965 Mbits/sec  0.024 ms  3523/5003078 (0.07%)  receiver
5203:  
5203:  iperf Done.

5204:  [ ID] Interval           Transfer     Bitrate         Total Datagrams
5204:  [  5]   0.00-60.00  sec  3.32 GBytes   476 Mbits/sec  2463250  
5204:  [  7]   0.00-60.00  sec  3.32 GBytes   476 Mbits/sec  2463250  
5204:  [SUM]   0.00-60.00  sec  6.64 GBytes   951 Mbits/sec  4926500  
5204:  - - - - - - - - - - - - - - - - - - - - - - - - -
5204:  [ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
5204:  [  5]   0.00-60.00  sec  3.32 GBytes   476 Mbits/sec  0.000 ms  0/2463250 (0%)  sender
5204:  [  5]   0.00-60.00  sec  3.32 GBytes   475 Mbits/sec  0.027 ms  1200/2463250 (0.049%)  receiver
5204:  [  7]   0.00-60.00  sec  3.32 GBytes   476 Mbits/sec  0.000 ms  0/2463250 (0%)  sender
5204:  [  7]   0.00-60.00  sec  3.32 GBytes   475 Mbits/sec  0.027 ms  1230/2463250 (0.05%)  receiver
5204:  [SUM]   0.00-60.00  sec  6.64 GBytes   951 Mbits/sec  0.000 ms  0/4926500 (0%)  sender
5204:  [SUM]   0.00-60.00  sec  6.64 GBytes   951 Mbits/sec  0.027 ms  2430/4926500 (0.049%)  receiver
5204:  
5204:  iperf Done.  
```
</details>




























# TCP_TX_9000
```
#commands in a_test_eth.sh
echo "SERVER_IP is 192.168.1.2"
#sudo ifconfig eth1 down
#sudo ifconfig eth1 mtu 9000
#sudo ifconfig eth1 inet 192.168.1.10
#sudo ifconfig eth1 up
iperf3 -c 192.168.1.2 -p 5201 -i 60 -t 60 -b 2500M -T 5201 -A 2 &
sleep 1s
iperf3 -c 192.168.1.2 -p 5202 -i 60 -t 60 -b 2500M -T 5202 -A 3 &
sleep 1s
mpstat -P ALL 1 40
```
<details>
<summary>terminal log</summary>

```
  
```
</details>

<details>
<summary>cpu load</summary>

```
Average:     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest   %idle
Average:     all    0.51    0.00   38.15    0.00    0.00    1.18    0.00    0.00   60.16
Average:       0    0.00    0.00    0.00    0.00    0.00    3.30    0.00    0.00   96.70
Average:       1    0.03    0.00    0.10    0.00    0.00    2.27    0.00    0.00   97.60
Average:       2    0.93    0.00   67.22    0.00    0.00    0.03    0.00    0.00   31.83
Average:       3    0.82    0.00   65.90    0.00    0.00    0.00    0.00    0.00   33.28  
```
</details>

<details>
<summary>performance</summary>

```
5201:  [ ID] Interval           Transfer     Bitrate         Retr  Cwnd
5201:  [  5]   0.00-60.00  sec  17.5 GBytes  2.50 Gbits/sec  247   1.17 MBytes       
5201:  - - - - - - - - - - - - - - - - - - - - - - - - -
5201:  [ ID] Interval           Transfer     Bitrate         Retr
5201:  [  5]   0.00-60.00  sec  17.5 GBytes  2.50 Gbits/sec  247             sender
5201:  [  5]   0.00-60.00  sec  17.5 GBytes  2.50 Gbits/sec                  receiver
5201:  
5201:  iperf Done.


5202:  [ ID] Interval           Transfer     Bitrate         Retr  Cwnd
5202:  [  5]   0.00-60.00  sec  17.5 GBytes  2.50 Gbits/sec  369    909 KBytes       
5202:  - - - - - - - - - - - - - - - - - - - - - - - - -
5202:  [ ID] Interval           Transfer     Bitrate         Retr
5202:  [  5]   0.00-60.00  sec  17.5 GBytes  2.50 Gbits/sec  369             sender
5202:  [  5]   0.00-60.00  sec  17.5 GBytes  2.50 Gbits/sec                  receiver
5202:  
5202:  iperf Done.  
```
</details>



























# UDP_TX_MTU_9000 
```
#commands
echo "SERVER_IP is 192.168.1.2"
#sudo ifconfig eth1 down
#sudo ifconfig eth1 mtu 9000
#sudo ifconfig eth1 inet 192.168.1.10
#sudo ifconfig eth1 up
iperf3 -u -P 2 -c 192.168.1.2 -p 5201 -i 60 -t 60 -b 2500M -Z -T 5201 -A 0 &
sleep 1s
iperf3 -u -P 2 -c 192.168.1.2 -p 5202 -i 60 -t 60 -b 2500M -Z -T 5202 -A 1 &
sleep 1s
iperf3 -u -P 2 -c 192.168.1.2 -p 5203 -i 60 -t 60 -b 2500M -Z -T 5203 -A 2 &
sleep 1s
iperf3 -u -P 2 -c 192.168.1.2 -p 5204 -i 60 -t 60 -b 2500M -Z -T 5204 -A 3 &
sleep 1s
mpstat -P ALL 1 40
```

<details>
<summary>terminal log</summary>

```
./a_test_eth.sh 
SERVER_IP is 192.168.1.2
5201:  Connecting to host 192.168.1.2, port 5201
5201:  [  5] local 192.168.1.10 port 54308 connected to 192.168.1.2 port 5201
5201:  [  7] local 192.168.1.10 port 34007 connected to 192.168.1.2 port 5201
5202:  Connecting to host 192.168.1.2, port 5202
5202:  [  5] local 192.168.1.10 port 48463 connected to 192.168.1.2 port 5202
5202:  [  7] local 192.168.1.10 port 45824 connected to 192.168.1.2 port 5202
5203:  Connecting to host 192.168.1.2, port 5203
5203:  [  5] local 192.168.1.10 port 55994 connected to 192.168.1.2 port 5203
5203:  [  7] local 192.168.1.10 port 54990 connected to 192.168.1.2 port 5203
5204:  Connecting to host 192.168.1.2, port 5204
5204:  [  5] local 192.168.1.10 port 38335 connected to 192.168.1.2 port 5204
5204:  [  7] local 192.168.1.10 port 39157 connected to 192.168.1.2 port 5204  
```
</details>

<details>
<summary>cpu load</summary>

```
Average:     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest   %idle
Average:     all    7.27    0.00   77.73    0.00    0.00   12.31    0.00    0.00    2.69
Average:       0    7.68    0.00   84.19    0.00    0.00    4.09    0.00    0.00    4.04
Average:       1    6.02    0.00   60.45    0.00    0.00   33.52    0.00    0.00    0.00
Average:       2    7.77    0.00   83.21    0.00    0.00    5.59    0.00    0.00    3.43
Average:       3    7.62    0.00   83.42    0.00    0.00    5.61    0.00    0.00    3.35  
```
</details>

<details>
<summary>performance</summary>

```
5201:  [ ID] Interval           Transfer     Bitrate         Total Datagrams
5201:  [  5]   0.00-60.00  sec  9.51 GBytes  1.36 Gbits/sec  1140583  
5201:  [  7]   0.00-60.00  sec  9.20 GBytes  1.32 Gbits/sec  1103575  
5201:  [SUM]   0.00-60.00  sec  18.7 GBytes  2.68 Gbits/sec  2244158  
5201:  - - - - - - - - - - - - - - - - - - - - - - - - -
5201:  [ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
5201:  [  5]   0.00-60.00  sec  9.51 GBytes  1.36 Gbits/sec  0.000 ms  0/1140583 (0%)  sender
5201:  [  5]   0.00-60.00  sec  9.50 GBytes  1.36 Gbits/sec  0.024 ms  18/1140583 (0.0016%)  receiver
5201:  [  7]   0.00-60.00  sec  9.20 GBytes  1.32 Gbits/sec  0.000 ms  0/1103575 (0%)  sender
5201:  [  7]   0.00-60.00  sec  9.20 GBytes  1.32 Gbits/sec  0.017 ms  20/1103575 (0.0018%)  receiver
5201:  [SUM]   0.00-60.00  sec  18.7 GBytes  2.68 Gbits/sec  0.000 ms  0/2244158 (0%)  sender
5201:  [SUM]   0.00-60.00  sec  18.7 GBytes  2.68 Gbits/sec  0.021 ms  38/2244158 (0.0017%)  receiver
5201:  
5201:  iperf Done.

5202:  [ ID] Interval           Transfer     Bitrate         Total Datagrams
5202:  [  5]   0.00-60.00  sec  7.29 GBytes  1.04 Gbits/sec  874692  
5202:  [  7]   0.00-60.00  sec  7.29 GBytes  1.04 Gbits/sec  874691  
5202:  [SUM]   0.00-60.00  sec  14.6 GBytes  2.09 Gbits/sec  1749383  
5202:  - - - - - - - - - - - - - - - - - - - - - - - - -
5202:  [ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
5202:  [  5]   0.00-60.00  sec  7.29 GBytes  1.04 Gbits/sec  0.000 ms  0/874692 (0%)  sender
5202:  [  5]   0.00-60.00  sec  7.29 GBytes  1.04 Gbits/sec  0.032 ms  68/874692 (0.0078%)  receiver
5202:  [  7]   0.00-60.00  sec  7.29 GBytes  1.04 Gbits/sec  0.000 ms  0/874691 (0%)  sender
5202:  [  7]   0.00-60.00  sec  7.29 GBytes  1.04 Gbits/sec  0.034 ms  67/874691 (0.0077%)  receiver
5202:  [SUM]   0.00-60.00  sec  14.6 GBytes  2.09 Gbits/sec  0.000 ms  0/1749383 (0%)  sender
5202:  [SUM]   0.00-60.00  sec  14.6 GBytes  2.09 Gbits/sec  0.033 ms  135/1749383 (0.0077%)  receiver
5202:  
5202:  iperf Done.

5203:  [ ID] Interval           Transfer     Bitrate         Total Datagrams
5203:  [  5]   0.00-60.00  sec  8.92 GBytes  1.28 Gbits/sec  1070678  
5203:  [  7]   0.00-60.00  sec  8.64 GBytes  1.24 Gbits/sec  1037152  
5203:  [SUM]   0.00-60.00  sec  17.6 GBytes  2.51 Gbits/sec  2107830  
5203:  - - - - - - - - - - - - - - - - - - - - - - - - -
5203:  [ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
5203:  [  5]   0.00-60.00  sec  8.92 GBytes  1.28 Gbits/sec  0.000 ms  0/1070678 (0%)  sender
5203:  [  5]   0.00-60.00  sec  8.92 GBytes  1.28 Gbits/sec  0.037 ms  75/1070678 (0.007%)  receiver
5203:  [  7]   0.00-60.00  sec  8.64 GBytes  1.24 Gbits/sec  0.000 ms  0/1037152 (0%)  sender
5203:  [  7]   0.00-60.00  sec  8.64 GBytes  1.24 Gbits/sec  0.041 ms  80/1037151 (0.0077%)  receiver
5203:  [SUM]   0.00-60.00  sec  17.6 GBytes  2.51 Gbits/sec  0.000 ms  0/2107830 (0%)  sender
5203:  [SUM]   0.00-60.00  sec  17.6 GBytes  2.51 Gbits/sec  0.039 ms  155/2107829 (0.0074%)  receiver
5203:  
5203:  iperf Done.

5204:  [ ID] Interval           Transfer     Bitrate         Total Datagrams
5204:  [  5]   0.00-60.00  sec  9.05 GBytes  1.29 Gbits/sec  1085424  
5204:  [  7]   0.00-60.00  sec  8.77 GBytes  1.26 Gbits/sec  1052239  
5204:  [SUM]   0.00-60.00  sec  17.8 GBytes  2.55 Gbits/sec  2137663  
5204:  - - - - - - - - - - - - - - - - - - - - - - - - -
5204:  [ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
5204:  [  5]   0.00-60.00  sec  9.05 GBytes  1.29 Gbits/sec  0.000 ms  0/1085424 (0%)  sender
5204:  [  5]   0.00-60.00  sec  9.04 GBytes  1.29 Gbits/sec  0.022 ms  85/1085424 (0.0078%)  receiver
5204:  [  7]   0.00-60.00  sec  8.77 GBytes  1.26 Gbits/sec  0.000 ms  0/1052239 (0%)  sender
5204:  [  7]   0.00-60.00  sec  8.77 GBytes  1.26 Gbits/sec  0.028 ms  75/1052239 (0.0071%)  receiver
5204:  [SUM]   0.00-60.00  sec  17.8 GBytes  2.55 Gbits/sec  0.000 ms  0/2137663 (0%)  sender
5204:  [SUM]   0.00-60.00  sec  17.8 GBytes  2.55 Gbits/sec  0.025 ms  160/2137663 (0.0075%)  receiver
5204:  
5204:  iperf Done.  
```
</details>
















# TCP_RX_MTU_9000
```
#commands
echo "SERVER_IP is 192.168.1.10"
#sudo ifconfig enp179s0f0 down
#sudo ifconfig enp179s0f0 mtu 9000
#sudo ifconfig enp179s0f0 inet 192.168.1.2
#sudo ifconfig enp179s0f0 up
iperf3 -c 192.168.1.10 -p 5201 -i 60 -t 60 -b 4000M -Z -T 5201 &
sleep 1s
iperf3 -c 192.168.1.10 -p 5202 -i 60 -t 60 -b 4000M -Z -T 5202 &
```

<details>
<summary>terminal log</summary>

```
./a_test_eth.sh 
SERVER_IP is 192.168.1.10
5201:  Connecting to host 192.168.1.10, port 5201
5202:  Connecting to host 192.168.1.10, port 5202  
```
</details>

<details>
<summary>cpu load</summary>

```
Average:     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest   %idle
Average:     all    1.37    0.00   20.02    0.00    0.00   26.02    0.00    0.00   52.59
Average:       0    0.00    0.00    0.00    0.00    0.00  100.00    0.00    0.00    0.00
Average:       1    0.00    0.00    0.00    0.00    0.00    0.16    0.00    0.00   99.84
Average:       2    2.70    0.00   41.39    0.00    0.00    0.00    0.00    0.00   55.91
Average:       3    2.89    0.00   40.15    0.00    0.00    0.00    0.00    0.00   56.97  
```
</details>

<details>
<summary>performance</summary>

```
5201:  [ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
5201:  [  4]   0.00-60.00  sec  11.8 GBytes  1.68 Gbits/sec  5673    481 KBytes       
5201:  - - - - - - - - - - - - - - - - - - - - - - - - -
5201:  [ ID] Interval           Transfer     Bandwidth       Retr
5201:  [  4]   0.00-60.00  sec  11.8 GBytes  1.68 Gbits/sec  5673             sender
5201:  [  4]   0.00-60.00  sec  11.8 GBytes  1.68 Gbits/sec                  receiver
5201:  
5201:  iperf Done.


5202:  [ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
5202:  [  4]   0.00-60.00  sec  11.3 GBytes  1.62 Gbits/sec  5650    830 KBytes       
5202:  - - - - - - - - - - - - - - - - - - - - - - - - -
5202:  [ ID] Interval           Transfer     Bandwidth       Retr
5202:  [  4]   0.00-60.00  sec  11.3 GBytes  1.62 Gbits/sec  5650             sender
5202:  [  4]   0.00-60.00  sec  11.3 GBytes  1.62 Gbits/sec                  receiver
5202:  
5202:  iperf Done.  
```
</details>







# UDP_RX_MTU_9000
```
#commands
echo "SERVER_IP is 192.168.1.10"
#sudo ifconfig enp179s0f0 down
#sudo ifconfig enp179s0f0 mtu 9000
#sudo ifconfig enp179s0f0 inet 192.168.1.2
#sudo ifconfig enp179s0f0 up
iperf3 -u -c 192.168.1.10 -p 5201 -i 60 -t 60 -b 4000M -Z -T 5201 -l 8972 &
sleep 1s
iperf3 -u -c 192.168.1.10 -p 5202 -i 60 -t 60 -b 4000M -Z -T 5202 -l 8972 &
```

<details>
<summary>terminal log</summary>

```
./a_test_eth.sh 
SERVER_IP is 192.168.1.10
5201:  Connecting to host 192.168.1.10, port 5201
5201:  [  4] local 192.168.1.2 port 52847 connected to 192.168.1.10 port 5201
5202:  Connecting to host 192.168.1.10, port 5202
5202:  [  4] local 192.168.1.2 port 41079 connected to 192.168.1.10 port 5202  
```
</details>

<details>
<summary>cpu load</summary>

```
Average:     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest   %idle
Average:     all    1.41    0.00   14.07    0.00    0.00   25.74    0.00    0.00   58.78
Average:       0    0.00    0.00    0.00    0.00    0.00  100.00    0.00    0.00    0.00
Average:       1    0.00    0.00    0.03    0.00    0.00    0.00    0.00    0.00   99.97
Average:       2    3.48    0.00   34.95    0.00    0.00    0.00    0.00    0.00   61.58
Average:       3    2.34    0.00   23.09    0.00    0.00    0.00    0.00    0.00   74.57  
```
</details>

<details>
<summary>performance</summary>

```
5201:  [ ID] Interval           Transfer     Bandwidth       Total Datagrams
5201:  [  4]   0.00-60.00  sec  27.1 GBytes  3.88 Gbits/sec  3245182  
5201:  - - - - - - - - - - - - - - - - - - - - - - - - -
5201:  [ ID] Interval           Transfer     Bandwidth       Jitter    Lost/Total Datagrams
5201:  [  4]   0.00-60.00  sec  27.1 GBytes  3.88 Gbits/sec  0.036 ms  2176964/3245182 (67%)  
5201:  [  4] Sent 3245182 datagrams
5201:  
5201:  iperf Done.

5202:  [ ID] Interval           Transfer     Bandwidth       Total Datagrams
5202:  [  4]   0.00-60.00  sec  27.1 GBytes  3.88 Gbits/sec  3244178  
5202:  - - - - - - - - - - - - - - - - - - - - - - - - -
5202:  [ ID] Interval           Transfer     Bandwidth       Jitter    Lost/Total Datagrams
5202:  [  4]   0.00-60.00  sec  27.1 GBytes  3.88 Gbits/sec  0.012 ms  2781195/3244178 (86%)  
5202:  [  4] Sent 3244178 datagrams
5202:  
5202:  iperf Done. 
  
#board log
[ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
[  5]   0.00-60.00  sec  8.93 GBytes  1.28 Gbits/sec  0.036 ms  2176964/3245182 (67%)  receiver

[ ID] Interval           Transfer     Bitrate         Jitter    Lost/Total Datagrams
[  5]   0.00-59.99  sec  3.87 GBytes   554 Mbits/sec  0.012 ms  2781195/3244178 (86%)  receiver
```
</details>











# UDP_RX_MTU_1500
```
#commands
#echo "SERVER_IP is 192.168.1.10"
#sudo ifconfig enp179s0f0 down
#sudo ifconfig enp179s0f0 mtu 1500
#sudo ifconfig enp179s0f0 inet 192.168.1.2
#sudo ifconfig enp179s0f0 up
iperf3 -u -c 192.168.1.10 -p 5201 -i 60 -t 60 -b 4000M -Z -T 5201 -l 1472 &
sleep 1s
iperf3 -u -c 192.168.1.10 -p 5202 -i 60 -t 60 -b 4000M -Z -T 5202 -l 1472 &
```

<details>
<summary>terminal log</summary>

```
./a_test_eth.sh 
5201:  Connecting to host 192.168.1.10, port 5201
5201:  [  4] local 192.168.1.2 port 33907 connected to 192.168.1.10 port 5201
5202:  Connecting to host 192.168.1.10, port 5202
5202:  [  4] local 192.168.1.2 port 35162 connected to 192.168.1.10 port 5202  
```
</details>

<details>
<summary>cpu load</summary>

```
Average:     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest   %idle
Average:     all    2.45    0.00   14.71    0.00    0.00   25.68    0.00    0.00   57.17
Average:       0    0.00    0.00    0.03    0.00    0.00   99.40    0.00    0.00    0.58
Average:       1    0.03    0.00    0.03    0.00    0.00    0.00    0.00    0.00   99.95
Average:       2    4.83    0.00   29.66    0.00    0.00    0.00    0.00    0.00   65.50
Average:       3    5.30    0.00   31.13    0.00    0.00    0.00    0.00    0.00   63.57  
```
</details>

<details>
<summary>performance</summary>

```
5202:  [  4] local 192.168.1.2 port 36237 connected to 192.168.1.10 port 5202
5201:  [ ID] Interval           Transfer     Bandwidth       Total Datagrams
5201:  [  4]   0.00-60.00  sec  27.9 GBytes  4.00 Gbits/sec  20367388  
5201:  - - - - - - - - - - - - - - - - - - - - - - - - -
5201:  [ ID] Interval           Transfer     Bandwidth       Jitter    Lost/Total Datagrams
5201:  [  4]   0.00-60.00  sec  27.9 GBytes  4.00 Gbits/sec  0.068 ms  19154852/20367335 (94%)  
5201:  [  4] Sent 20367335 datagrams
5201:  
5201:  iperf Done.
5202:  [ ID] Interval           Transfer     Bandwidth       Total Datagrams
5202:  [  4]   0.00-60.00  sec  27.9 GBytes  4.00 Gbits/sec  20363788  
5202:  - - - - - - - - - - - - - - - - - - - - - - - - -
5202:  [ ID] Interval           Transfer     Bandwidth       Jitter    Lost/Total Datagrams
5202:  [  4]   0.00-60.00  sec  27.9 GBytes  4.00 Gbits/sec  0.009 ms  19262633/20363589 (95%)  
5202:  [  4] Sent 20363589 datagrams
5202:  
5202:  iperf Done.  
```
</details>








# TCP_RX_MTU_1500
```
#commands
#---------------used on board--------------------
#echo 32768 > /proc/sys/net/core/rps_sock_flow_entries
#echo 2048 > /sys/class/net/eth0/queues/rx-0/rps_flow_cnt
#echo 2048 >  /sys/class/net/eth0/queues/rx-1/rps_flow_cnt
#---------------used on server-------------------
echo "SERVER_IP is 192.168.1.10"
#sudo ifconfig enp179s0f0 down
#sudo ifconfig enp179s0f0 mtu 1500
#sudo ifconfig enp179s0f0 inet 192.168.1.2
#sudo ifconfig enp179s0f0 up
iperf3 -c 192.168.1.10 -p 5201 -i 60 -t 60 -b 4000M -Z -T 5201 &
sleep 1s
iperf3 -c 192.168.1.10 -p 5202 -i 60 -t 60 -b 4000M -Z -T 5202 &
```

<details>
<summary>terminal log</summary>

```
  
```
</details>

<details>
<summary>cpu load</summary>

```
Average:     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest   %idle
Average:     all    1.21    0.00   24.33    0.00    0.00   25.72    0.00    0.00   48.74
Average:       0    0.00    0.00    0.00    0.00    0.00  100.00    0.00    0.00    0.00
Average:       1    0.00    0.00    0.11    0.00    0.00    0.67    0.00    0.00   99.22
Average:       2    2.29    0.00   46.66    0.00    0.00    0.00    0.00    0.00   51.04
Average:       3    2.51    0.00   49.33    0.00    0.00    0.00    0.00    0.00   48.17  
```
</details>

<details>
<summary>performance</summary>

```
5201:  [ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
5201:  [  4]   0.00-60.00  sec  4.48 GBytes   642 Mbits/sec  1527    187 KBytes       
5201:  - - - - - - - - - - - - - - - - - - - - - - - - -
5201:  [ ID] Interval           Transfer     Bandwidth       Retr
5201:  [  4]   0.00-60.00  sec  4.48 GBytes   642 Mbits/sec  1527             sender
5201:  [  4]   0.00-60.00  sec  4.48 GBytes   641 Mbits/sec                  receiver
5201:  
5201:  iperf Done.
5202:  [ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
5202:  [  4]   0.00-60.00  sec  4.53 GBytes   649 Mbits/sec  1619    325 KBytes       
5202:  - - - - - - - - - - - - - - - - - - - - - - - - -
5202:  [ ID] Interval           Transfer     Bandwidth       Retr
5202:  [  4]   0.00-60.00  sec  4.53 GBytes   649 Mbits/sec  1619             sender
5202:  [  4]   0.00-60.00  sec  4.53 GBytes   649 Mbits/sec                  receiver
5202:  
5202:  iperf Done.  
```
</details>




# 修改
```
4000M -> 2500M same
-P 2 same
```

<details>
<summary>performance</summary>

```
5201:  [ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
5201:  [  4]   0.00-60.00  sec  2.21 GBytes   316 Mbits/sec  2980   76.4 KBytes       
5201:  [  6]   0.00-60.00  sec  2.21 GBytes   317 Mbits/sec  2972   60.8 KBytes       
5201:  [SUM]   0.00-60.00  sec  4.42 GBytes   633 Mbits/sec  5952             
5201:  - - - - - - - - - - - - - - - - - - - - - - - - -
5201:  [ ID] Interval           Transfer     Bandwidth       Retr
5201:  [  4]   0.00-60.00  sec  2.21 GBytes   316 Mbits/sec  2980             sender
5201:  [  4]   0.00-60.00  sec  2.21 GBytes   316 Mbits/sec                  receiver
5201:  [  6]   0.00-60.00  sec  2.21 GBytes   317 Mbits/sec  2972             sender
5201:  [  6]   0.00-60.00  sec  2.21 GBytes   317 Mbits/sec                  receiver
5201:  [SUM]   0.00-60.00  sec  4.42 GBytes   633 Mbits/sec  5952             sender
5201:  [SUM]   0.00-60.00  sec  4.42 GBytes   632 Mbits/sec                  receiver
5201:  
5201:  iperf Done.
5202:  [ ID] Interval           Transfer     Bandwidth       Retr  Cwnd
5202:  [  4]   0.00-60.00  sec  2.24 GBytes   321 Mbits/sec  3032    139 KBytes       
5202:  [  6]   0.00-60.00  sec  2.21 GBytes   316 Mbits/sec  3146    233 KBytes       
5202:  [SUM]   0.00-60.00  sec  4.45 GBytes   637 Mbits/sec  6178             
5202:  - - - - - - - - - - - - - - - - - - - - - - - - -
5202:  [ ID] Interval           Transfer     Bandwidth       Retr
5202:  [  4]   0.00-60.00  sec  2.24 GBytes   321 Mbits/sec  3032             sender
5202:  [  4]   0.00-60.00  sec  2.24 GBytes   321 Mbits/sec                  receiver
5202:  [  6]   0.00-60.00  sec  2.21 GBytes   316 Mbits/sec  3146             sender
5202:  [  6]   0.00-60.00  sec  2.20 GBytes   316 Mbits/sec                  receiver
5202:  [SUM]   0.00-60.00  sec  4.45 GBytes   637 Mbits/sec  6178             sender
5202:  [SUM]   0.00-60.00  sec  4.45 GBytes   637 Mbits/sec                  receiver
5202:  
5202:  iperf Done.  
```
  
  
  
  
  
  
  
  
  
  
  
</details>



<details>
<summary>terminal log</summary>

```
  
```
</details>

<details>
<summary>cpu load</summary>

```
  
```
</details>

<details>
<summary>performance</summary>

```
  
```
</details>







































































