# Week 6 – Stress Testing and Performance Analysis

## 1. Stress Testing Tools

<img width="804" height="239" alt="Screenshot 2025-12-22 070355" src="https://github.com/user-attachments/assets/7ba26988-ec9f-41f9-b5ac-61f3a2c851d2" />

Stress testing tools were installed and verified on the Ubuntu Server to enable controlled
CPU, memory, disk, and network performance testing.

## 2. CPU Stress Test

<img width="916" height="228" alt="Screenshot 2025-12-22 072050" src="https://github.com/user-attachments/assets/6cb61828-c898-450b-81ad-bab3fc466d48" />
<img width="733" height="176" alt="Screenshot 2025-12-22 071040" src="https://github.com/user-attachments/assets/6ffcaa60-65a2-4cd5-a331-7c57f59263fd" />

A CPU stress test was performed using stress-ng to fully utilise available processor
cores. Real-time monitoring showed sustained 100% CPU utilisation across all cores and
increased system load during the test period.


## 3. Memory Stress Test

<img width="747" height="173" alt="Screenshot 2025-12-22 072359" src="https://github.com/user-attachments/assets/b6763282-24a7-428a-98fb-cc3cb6ebda47" />
<img width="941" height="223" alt="Screenshot 2025-12-22 072317" src="https://github.com/user-attachments/assets/7db0065d-bcf2-4167-ab0f-399d4c265ac0" />

A memory stress test was conducted using stress-ng to apply memory pressure. Monitoring
showed increased memory utilisation and minor swap usage during the test, while the
system remained stable.

## 4. Disk I/O Stress Test

<img width="709" height="43" alt="Screenshot 2025-12-22 073055" src="https://github.com/user-attachments/assets/b0eafa99-8a50-45a5-84eb-e78a9cecba85" />
<img width="1160" height="611" alt="Screenshot 2025-12-22 073127" src="https://github.com/user-attachments/assets/f1a16c03-4f74-4f2a-82c5-3af5bdc80363" />

Disk I/O performance was evaluated using fio to generate sustained write operations.
Monitoring showed increased disk activity and elevated I/O utilisation during the test,
while the system remained stable.


## 5. Network Stress Test

<img width="631" height="341" alt="Screenshot 2025-12-22 074111" src="https://github.com/user-attachments/assets/d1480610-1338-49a9-ab4c-3753c3cf9bc6" />
<img width="789" height="467" alt="Screenshot 2025-12-22 074201" src="https://github.com/user-attachments/assets/3712332c-2ec2-4a55-a119-14549513e7be" />

Network performance was tested using iperf3 to generate sustained traffic between the
workstation and server. The results showed high network throughput throughout the test,
demonstrating the system’s ability to handle network load under stress.

## 6. Performance Analysis

Compared to baseline measurements collected in Week 5, stress testing resulted in
significantly increased CPU utilisation, higher memory usage with minor swap activity,
elevated disk I/O load, and substantially increased network throughput. Despite the
increased demand on system resources, the server remained stable and responsive
throughout all tests, indicating effective resource management under load.

## 7. Week 6 Reflection


Week 6 focused on evaluating system performance under controlled stress conditions.
Applying targeted stress to CPU, memory, disk, and network resources provided clear
insight into how system behaviour changes under load compared to baseline conditions.

This week highlighted the importance of baseline measurements for meaningful
performance analysis and demonstrated how real-time monitoring tools support the
identification of potential performance bottlenecks and system limitations.
