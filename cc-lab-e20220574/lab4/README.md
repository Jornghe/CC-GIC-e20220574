# Cloud Lab 4 Submission — Amazon VPC with Public and Private Subnets

**Student name:** Kuoch Chyhang
**Student ID:** e20220574
**Learner Lab user name:** voclabs/user5623073=KUOCH_CHYHANG
**Date completed:** 2026-11-06

---

## Task 1 — VPC

![lab4-vpc with CIDR 10.0.0.0/24](images/01-vpc.png)

---

## Task 2 — Internet Gateway

![lab4-internet-gateway Attached to lab4-vpc](images/02-internet-gateway.png)

---

## Task 3 — Public Subnet

![lab4-public-subnet with CIDR 10.0.0.0/25](images/03-public-subnet.png)

---

## Task 4 — Public Route Table

![Route 0.0.0.0/0 to lab4-internet-gateway](images/04-public-route-table.png)

---

## Task 5 — EC2 Instance in Public Subnet

![lab4-ec2-01 running in lab4-public-subnet](images/05-ec2-public.png)

---

## Task 6 — Test Internet Access (Public)

![Run Command Success for lab4-ec2-01](images/06-test-public.png)

---

## Task 7 — Private Subnet

![lab4-private-subnet with CIDR 10.0.0.128/25](images/07-private-subnet.png)

---

## Task 8 — NAT Gateway

![lab4-nat-gateway Available in lab4-public-subnet](images/08-nat-gateway.png)

---

## Task 9 — Private Route Table

![lab4-custom-route-table with 0.0.0.0/0 to lab4-nat-gateway](images/09-private-route-table.png)

---

## Task 10 — EC2 Instance in Private Subnet

![lab4-ec2-02 running in lab4-private-subnet, no public IP](images/10-ec2-private.png)

---

## Task 11 — Test Internet Access (Private)

![Run Command Success for lab4-ec2-02](images/11-test-private.png)

---

## Questions

1. **What is the difference between a public subnet and a private subnet in this lab?**

   The public subnet has a route to the internet gateway, so instances in it can send and receive traffic directly from the internet. The private subnet has no route to the internet gateway — its traffic goes to the NAT gateway instead, which forwards it to the internet gateway. Instances in the private subnet can reach the internet but cannot be reached from it directly.

2. **Why does the private instance have no public IP address, and how does it still reach the internet?**

   The private instance has Auto-assign public IP disabled because it should not be directly accessible from the internet. It reaches the internet through the NAT gateway, which is in the public subnet. The NAT gateway has an Elastic IP and acts as an intermediary — it sends the private instance's outbound traffic to the internet and returns the response.

3. **What does the LabInstanceProfile do, and why is it needed?**

   The LabInstanceProfile attaches the LabRole IAM role to the instance. This allows AWS Systems Manager (SSM) to connect to and run commands on the instance without needing SSH or a key pair. Without it, SSM cannot authenticate with the instance.

4. **Why is a NAT gateway placed in the public subnet rather than the private subnet?**

   The NAT gateway needs internet access itself to forward traffic on behalf of private instances. It must be in the public subnet so it can route traffic through the internet gateway. If it were in the private subnet, it would have no path to the internet.

---

## Clean up

- [ ] EC2 instances terminated.
- [ ] Routes deleted.
- [ ] NAT gateway deleted.
- [ ] Elastic IP released.
- [ ] Internet gateway detached and deleted.
- [ ] VPC deleted.
