## Task
The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

For this task, allocate an Elastic IP address, name it as xfusion-eip.
## Solution
1. Login to the AWS Console.
2. Go to the VPC Dashboard.
3. Click on "Elastic IPs".
4. Click on "Allocate Elastic IP address"
   ![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/25dbf38f-f6dd-46f4-8e85-1739960f3438)
5. Add a tag "name" with value "xfusion-eip" and click allocate.

   ![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/f48eba89-6a6c-41b2-8ac6-03257af306c2)

6. The Elastic IP addess has been allocated.

## References

[Elastic IP addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html#using-instance-addressing-eips-allocating)
