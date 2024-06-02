![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/80a6999b-98e9-4ee8-bc07-782e81b3c35d)## Task

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks into smaller, more manageable units. This granular approach enables the team to execute the migration in gradual phases, ensuring smoother implementation and minimizing disruption to ongoing operations. By breaking down the migration into smaller tasks, the Nautilus DevOps team can systematically progress through each stage, allowing for better control, risk mitigation, and optimization of resources throughout the migration process.

Create a volume with the following requirements:

Name of the volume should be datacenter-volume.

Volume type must be gp3.

Volume size must be 2 GiB.

## Solution 

1. Login into the AWS Console.
2. Go to the EC2 console.
3. Go to "Elstic Block Store" and click "Volumes".
4. Hit the "Create volume" button.
   ![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/79a3fe68-e3d3-41c2-a396-367d70e23d90)
5. In the wizard choose "General Purpose SSD (gp3)" and change a size of volume to 2GiB as per task.
   ![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/208926cb-3f4e-40ab-b829-55d47d9bcebc)
6. Add a tag "name" with value "datacenter-volume".
   ![image](https://github.com/AdamLisicki/kodekloud-engineer/assets/96197101/a4a26d65-a119-4d49-8678-c6ec0fff401e)
7. Click "Create volume"
8. The EBS volume has been created.
## References

[Create an Amazon EBS volume](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-creating-volume.html)
