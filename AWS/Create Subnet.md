## Task
The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition.

For this task, create one subnet named xfusion-subnet under default VPC.

## Solution
1. Login to the AWS Console.
2. Go to the VPC Dashboard.
3. Go to "Subnets" and click "Create subnet".
   ![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/18c1e2be-9c37-477c-81f7-1c535191a08c)
4. Choose a VPC and type a name for this subnet.
   ![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/97e172f0-1a2a-4cd0-a126-73443e1414aa)
5. Choose IPv4 subnet CIDR block that don't overlaps with existings subnets.
   ![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/1bbc7382-12fc-499e-ac79-1e05e281366e)

7. Click "Create subnet".
8. Subnet has been created.

## References

[Create a subnet](https://docs.aws.amazon.com/vpc/latest/userguide/create-subnets.html)
