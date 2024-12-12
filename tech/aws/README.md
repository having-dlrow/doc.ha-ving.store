---
icon: aws
---

# AWS

다중 AZ 서브넷 설계

|                                   | A subnet                          | B subnet                          |                |
| --------------------------------- | --------------------------------- | --------------------------------- | -------------- |
| presentation                      | 10.0.0.0/24                       | 10.0.1.0/24                       | ELB            |
| <p>Application<br>( private )</p> | 10.0.2.0/24                       | 10.0.3.0/24                       | Front, Backend |
| <p>Database<br>( private )</p>    | <p>10.0.4.0/24<br>( primary )</p> | <p>10.0.5.0/24<br>( Replica )</p> | Database       |

* Internet Gateway
* Nat Gateway
