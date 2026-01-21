# Performance-Testing
# 🧪 Apache JMeter Performance Testing Report   
   
## 📘 Project Overview  
This project demonstrates **API Load Testing**, **Endurance Testing**, and **Spike Testing** using **Apache JMeter (CLI Mode)**.  
The target system used for testing was the [OrangeHRM Demo Application](https://opensource-demo.orangehrmlive.com).

The purpose of this test was to analyze: 
- API performance under increasing load  
- Error rate and response time behavior  
- Server stability under prolonged stress and sudden spikes

---

## ⚙️ Test Environment 
| Parameter | Description |
|------------|-------------|
| **Tool** | Apache JMeter (Non-GUI Mode) |
| **Target Application** | OrangeHRM Demo |
| **Test Duration** | 3 minutes |
| **Total Requests** | 16,000 |
| **Threads (Users)** | Variable (Load Increased Gradually) |
| **Report Generated** | HTML Dashboard & PDF Summary |

---

## 🧾 Test Summary
| Metric | Result |
|---------|--------|
| **Total Requests** | 16,000 |
| **Passed Requests** | 13,746 (85.91%) |
| **Failed Requests** | 2,254 (14.09%) |
| **Error Rate** | 14.09% |
| **APDEX Score** | 0.011 (Very Poor) |

---

## 📊 Error Breakdown
| Error Type | Count | Percentage | Description |
|-------------|--------|-------------|--------------|
| NoHttpResponseException | 1165 | 51.7% | Server failed to respond (likely overload) |
| 500 Internal Server Error | 382 | 16.9% | Internal backend issue or crash |
| 502 Bad Gateway | 313 | 13.9% | Gateway/load balancer issue |
| SSLHandshakeException | 312 | 13.8% | SSL handshake failed due to traffic overload |
| SocketException: Connection reset | 82 | 3.6% | Server abruptly closed connection |

---

## 🧠 Analysis
- The system **failed under high load** (14% error rate).  
- Most failures were **network or SSL related**, indicating server capacity issues.  
- The **APDEX score of 0.011** shows very poor user experience under stress conditions.  
- Sudden load increases triggered **spike failures** and inconsistent responses.

---

## 🛠️ Recommendations
1. **Gradually increase user load** until the error rate remains below 1%.  
2. **Increase ramp-up time** (e.g., 30–60 seconds) for smoother load application.  
3. **Enable Keep-Alive** and **tune connection timeout** to reduce SSL and socket errors.  
4. Review backend logs to identify causes of **500/502 errors**.  
5. Perform a **10-minute endurance test** after tuning the server configuration.  
6. Consider **resource scaling or load balancing improvements**.

---

## 📁 Files Included
| File | Description |
|------|--------------|
| `testplan.jmx` | JMeter Test Plan |
| `results.jtl` | Test Result Log File |
| `JMeter_Test_Report_Fuzayel.pdf` | Performance Test Summary Report (PDF) |
| `README.md` | Documentation File |

---

## 🚀 How to Run the Test (CLI Mode)
You can run the JMeter test in **Non-GUI Mode** using the command below:

```bash
jmeter -n -t testplan.jmx -l results.jtl -e -o Reports/
