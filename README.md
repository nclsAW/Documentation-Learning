<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2E9EF7,100:0B1F3A&height=180&section=header&text=Portfolio&fontSize=36&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Manual%20Testing%20%E2%80%A2%20Test%20Automation%20%E2%80%A2%20Documentation&descAlignY=58&descSize=16" width="100%"/>

</div>

This repository was created to facilitate access to concise portfolio summaries and to ensure that test scenario formats are adjusted whenever possible. For now, it will be consolidated into a single repository; once it becomes large enough, it will be split into separate branches within that single repo.

<details>
<summary>Summary Detail</summary>

<details style="margin-left: 20px"><summary>ParaBank</summary>
  

### Test Environment
| Parameter | Detail |
|---|---|
| URL | [ParaBank \| Welcome \| Online Banking](https://parabank.parasoft.com/parabank/index.htm) |
| Browser | Google Chrome |
| OS | Windows 11 |
| Test Management Tool | Jira |
| Documentation Tool | Confluence |

### Execution Status
| Status | Jumlah Test Case | Persentase |
|---|---|---|
| Passed | 51 | 78.46% |
| Failed | 14 | 21.54% |
| Blocked | 0 | 0% |
| **Total** | **65** | **100%** |

### Defect Summary by Severity
| Severity | Open | Resolved/Closed |
|---|---|---|
| Critical/Blocker | 3 | 0 |
| High | 8 | 0 |
| Medium | 0 | 0 |
| Low/Minor | 3 | 0 |
| **Total** | **14** | **0** |

### Key Defect Log
| Jira Key | Bug Summary | Severity | Status | Module |
|---|---|---|---|---|
| KAN-20 | Logout tidak clear browser cache (no Cache-Control header) | Critical | Open | User Logout |
| KAN-21 | Search kosong tidak nunjukin empty state | Low | Open | Find Transactions |
| KAN-22 | Registrasi bisa pakai spasi doang, tidak ada trim validation | High | Open | Register |
| KAN-23 | Update Contact Info bisa pakai spasi, tidak ada trim validation | High | Open | Update Contact Info |
| KAN-26 | Open New Account tidak validasi saldo cukup | High | Open | Open New Account |
| KAN-27 | Transfer Funds tidak validasi limit saldo (overdraft) | Critical | Open | Transfer Funds |
| KAN-28 | Transfer Funds terima nominal negatif | Critical | Open | Transfer Funds |
| KAN-29 | Transfer Funds bisa pilih akun sender = recipient | High | Open | Transfer Funds |
| KAN-30 | Bill Pay tidak validasi saldo cukup | High | Open | Bill Pay |
| KAN-31 | Request Loan crash (HTTP 500) kalau Down Payment kosong | High | Open | Request Loan |
| KAN-32 | Request Loan crash (HTTP 500) kalau input non-numeric | High | Open | Request Loan |
</details>

</details>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0B1F3A,100:2E9EF7&height=100&section=footer" width="100%"/>

</div>
