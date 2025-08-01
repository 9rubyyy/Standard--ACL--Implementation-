# 🔐 ACL Standard - Packet Tracer Lab (CCNA Practice)

This is a simple hands-on project I created while studying for the **CCNA certification**. It demonstrates how to configure **Standard ACLs** using Cisco Packet Tracer.

## 🧠 Project Overview
The project simulates a real-world scenario where a "ACL" is implemented to control communication between multiple subnets.

## 🖥️ Devices Used
- 1 × Multilayer Switch (3560)
- 2 × Switches (2960)
- 5 × PCs

## 🌐 Subnet Details

| Subnet        | Connected Devices | Subnet Mask         |
|---------------|-------------------|---------------------|
| 10.1.1.0/24   | PC0 , PC1         | 255.255.255.0       |
| 10.1.2.0/27   | PC4               | 255.255.255.224     |
| 10.1.3.0/28   | PC2, PC3          | 255.255.255.240     |

## 🔒 Project Goals
- Apply **Standard ACLs** to control or restrict access between subnets.
- Understand how ACLs affect traffic flow.
- Reinforce theoretical concepts from the CCNA curriculum through practical application.

## 📸 Network Topology

<img width="413" height="244" alt="image" src="https://github.com/user-attachments/assets/df8ae48f-5257-48a1-a5e0-81d4a44d859b" />



## 💡 Additional Info
- Software used: Cisco Packet Tracer 8.2

---

## 🔧 Key Commands Used

### Initial Config ###

| PC            | IP                | Subnet Mask         | Gateway          |
|---------------|-------------------|---------------------|------------------|
| PC0           | 10.1.1.10         | 255.255.255.0       | 10.1.1.1         |
| PC1           | 10.1.1.11         | 255.255.255.0       | 10.1.1.1         |
| PC2           | 10.1.3.10         | 255.255.255.240     | 10.1.3.1         |
| PC3           | 10.1.3.11         | 255.255.255.240     | 10.1.3.1         |
| PC4           | 10.1.2.10         | 255.255.255.224     | 10.1.2.1         |

###  Multilayer Switch Config ###
````
ip routing 
int fa 0/1 
no swi 
ip add 10.1.1.1  255.255.255.0
exit 
int fa 0/2 
no swi 
ip add 10.1.2.1  255.255.255.224
exit 
int fa 0/3
no swi 
ip add 10.1.3.1  255.255.255.240
exit 

router ospf5
net 10.1.1.0   0.0.0.255  area 0
net 10.1.2.0   0.0.0.31   area 0
net 10.1.3.0   0.0.0.15   area 0
exit 

### ACL Config ###

access-list 10 deny 10.1.1.0  0.0.0.255 

access-list 10 permit any 
int fa 0/3 
ip access-group 10 out 
end 
````

## 📌 Notes
- When applying a Standard ACL on a **Multilayer Switch**, remember that the direction (`in` or `out`) is based on how the traffic flows **relative to the interface**.
- For example:  
  If you apply an ACL on `FastEthernet0/3` in the **out** direction, it will **filter traffic exiting through that interface** — such as traffic going from another subnet to **PC4**.
- The ACL will not affect traffic **entering** through `Fa0/3`, only traffic **leaving** it.





