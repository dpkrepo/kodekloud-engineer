## Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, create a security group under default VPC with the following requirements:

Name of the security group is nautilus-sg.

The description must be Security group for Nautilus App Servers

Add the inbound rule of type HTTP, with port range of 80. Enter the source CIDR range of 0.0.0.0/0.

Add another inbound rule of type SSH, with port range of 22. Enter the source CIDR range of 0.0.0.0/0.

## Solution

1. Login to the AWS Console.
2. Go to the EC2 Dashboard.
3. On the left panel there is a "Network & Security" section where we can find "Security Groups".
4. Go to "Security Groups".
5. Click "Create security group"
![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/61c65eac-36ec-466a-a2d4-671b584baf67)
6. In the wizard we have to provide below information as per task:
   - security group name
   - description
   - inbound rules

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/c4b10a44-7ed2-4523-a720-1abe0cc10c9c)

![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/75059677-8aba-4ce4-b63a-d0b40d223135)


7. Click "Create security group".
8. Security group has been created.


 
## References

[Work with security groups](https://docs.aws.amazon.com/vpc/latest/userguide/working-with-security-groups.html)
