Lister tout les VPCs

$ aws ec2 describe-vpcs --profile devopsteam07 --region eu-centrale-1 --output table


Output :
-----------------------------------------------------------
|                      DescribeVpcs                       |
+---------------------------------------------------------+
||                         Vpcs                          ||
|+----------------------+--------------------------------+|
||  CidrBlock           |  10.0.0.0/16                   ||
||  DhcpOptionsId       |  dopt-05854b009a610ac91        ||
||  InstanceTenancy     |  default                       ||
||  IsDefault           |  False                         ||
||  OwnerId             |  709024702237                  ||
||  State               |  available                     ||
||  VpcId               |  vpc-0a22d771f16ae549d         ||
|+----------------------+--------------------------------+|
|||               BlockPublicAccessStates               |||
||+------------------------------------------+----------+||
|||  InternetGatewayBlockMode                |  off     |||
||+------------------------------------------+----------+||
|||               CidrBlockAssociationSet               |||
||+----------------+------------------------------------+||
|||  AssociationId |  vpc-cidr-assoc-0fad6e9a11ccae331  |||
|||  CidrBlock     |  10.0.0.0/16                       |||
||+----------------+------------------------------------+||
||||                  CidrBlockState                   ||||
|||+-------------------+-------------------------------+|||
||||  State            |  associated                   ||||
|||+-------------------+-------------------------------+|||
|||                        Tags                         |||
||+----------------------+------------------------------+||
|||  Key                 |  Name                        |||
|||  Value               |  vpc-i346                    |||
||+----------------------+------------------------------+||


Créer une route table :

aws ec2 create-route-table --vpc-id vpc-0a22d771f16ae549d --profile devopsteam07 --region eu-central-1 --output table

output :

-------------------------------------------------------------------------
|                           CreateRouteTable                            |
+------------------+----------------------------------------------------+
|  ClientToken     |  e13cb7f7-87b6-4a92-b667-2d28d2255cc9              |
+------------------+----------------------------------------------------+
||                             RouteTable                              ||
|+---------------+--------------------------+--------------------------+|
||    OwnerId    |      RouteTableId        |          VpcId           ||
|+---------------+--------------------------+--------------------------+|
||  709024702237 |  rtb-0b68177540d710b1a   |  vpc-0a22d771f16ae549d   ||
|+---------------+--------------------------+--------------------------+|
|||                              Routes                               |||
||+-----------------------+------------+--------------------+---------+||
||| DestinationCidrBlock  | GatewayId  |      Origin        |  State  |||
||+-----------------------+------------+--------------------+---------+||
|||  10.0.0.0/16          |  local     |  CreateRouteTable  |  active |||
||+-----------------------+------------+--------------------+---------+||


Lister tout les sous-réseaux :

aws ec2 describe-subnets --profile devopsteam07 --region eu-central-1 --output table

Output :

------------------------------------------------------------------------------------------------------------
|                                              DescribeSubnets                                             |
+----------------------------------------------------------------------------------------------------------+
||                                                 Subnets                                                ||
|+------------------------------+-------------------------------------------------------------------------+|
||  AssignIpv6AddressOnCreation |  False                                                                  ||
||  AvailabilityZone            |  eu-central-1c                                                          ||
||  AvailabilityZoneId          |  euc1-az1                                                               ||
||  AvailableIpAddressCount     |  11                                                                     ||
||  CidrBlock                   |  10.0.10.0/28                                                           ||
||  DefaultForAz                |  False                                                                  ||
||  EnableDns64                 |  False                                                                  ||
||  Ipv6Native                  |  False                                                                  ||
||  MapCustomerOwnedIpOnLaunch  |  False                                                                  ||
||  MapPublicIpOnLaunch         |  False                                                                  ||
||  OwnerId                     |  709024702237                                                           ||
||  State                       |  available                                                              ||
||  SubnetArn                   |  arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-0c409522b892fc4bf  ||
||  SubnetId                    |  subnet-0c409522b892fc4bf                                               ||
||  VpcId                       |  vpc-0a22d771f16ae549d                                                  ||
|+------------------------------+-------------------------------------------------------------------------+|
|||                                        BlockPublicAccessStates                                       |||
||+---------------------------------------------------------------------------------+--------------------+||
|||  InternetGatewayBlockMode                                                       |  off               |||
||+---------------------------------------------------------------------------------+--------------------+||
|||                                     PrivateDnsNameOptionsOnLaunch                                    |||
||+-----------------------------------------------------------------------------+------------------------+||
|||  EnableResourceNameDnsAAAARecord                                            |  False                 |||
|||  EnableResourceNameDnsARecord                                               |  False                 |||
|||  HostnameType                                                               |  ip-name               |||
||+-----------------------------------------------------------------------------+------------------------+||
|||                                                 Tags                                                 |||
||+---------------------------+--------------------------------------------------------------------------+||
|||  Key                      |  Name                                                                    |||
|||  Value                    |  subnet-10.0.10.0/28                                                     |||
||+---------------------------+--------------------------------------------------------------------------+||
 
 (Il y en a encore de la suite mais beaucoup trop long)


Commande pour créer une route

 aws ec2 create-route --route-table-id rtb-0a9293aaf3c30b82c --destination-cidr-block 10.0.7.0/28 --gateway-id igw-059306bf876cf19f6 --profile devopsteam07 --region eu-central-1 --output table

Ouput :

An error occurred (UnauthorizedOperation) when calling the CreateRoute operation: You are not authorized to perform this operation. User: arn:aws:iam::709024702237:user/devopsteam07-i346 is not authorized to perform: ec2:CreateRoute on resource: arn:aws:ec2:eu-central-1:709024702237:route-table/rtb-0a9293aaf3c30b82c because no identity-based policy allows the ec2:CreateRoute action. Encoded authorization failure message: V0OPYL67Z_jKv0k4DLblo8n9CCvR2YRp9XL5FJmtBzufbE5CFm0ncTH-vhu_FNehoAI9dmiHUZglcwVJNYGbAImuGMlT_c9Oev2cAVTIFohfmhwu-nO3mbsjMs5RsrUAcXi1CVQ1GE7RL77lkNKDmu6Z9f-ya8nhuXYSp3JMoUy-luC0JPWNxFwqj8NWQ7UrCJrEnprEUQs09wQexGdENXLdQE9TFQ2eIRjAKtZn1i-m1_yUb-vD1FWD9LbZScJ7H8BtGcrEQuvzlWl6Z2pR7tyJO95gKu44lqt1TExAStRK7BXgDINqCoRYouZa_6K53ogIX5S3JKY-vvLiXN71ZqjsT4e308yULE6lZquFrIqcFWVkTAL7qgCrTgaIxOwGIvJwkctjbUHGBBez6pZc4rsLQqbhwpFwCLqANuy0UODAuy1FCjohEOjpc0SO5KE0bxKLV9LTDXwK_aah4xMI7QZl1Tqf12ljBysRNK2MDj2-x3sxcBqlZYghnAHBs2Yw7rakrbbvdiGKN4S269cNJQ6vL4_ntJYDUhvoQqq57qq1_SNtgntq9GEeB508i5TWctoZPPd1YU0CWlWYoTPx2cYdT6Fj

Impossible de créer une route car nous avons pas les accès



commande pour ajouter un tag à un element deja crée:
 
$ aws ec2 create-tags --resources rtb-0a9293aaf3c30b82c --tags Key=Environment,Value=Production --region eu-central-1 --profil devopsteam07

Output :

An error occurred (UnauthorizedOperation) when calling the CreateTags operation: You are not authorized to perform this operation. User: arn:aws:iam::709024702237:user/devopsteam07-i346 is not authorized to perform: ec2:CreateTags on resource: arn:aws:ec2:eu-central-1:709024702237:route-table/rtb-0a9293aaf3c30b82c because no identity-based policy allows the ec2:CreateTags action. Encoded authorization failure message: s9kLF877EFcutHwhgwKxPNuMkBcOv5UQTexodMqo1iqRlQXXYS1iinLN9j1YHpg0nuf_FxUK-oo4jvxrVeCbPPpCYu83Zmn-Q9ysYxeV065PkZoSs6l_uJ1PAUQDw_GaNEqrd7DE3J6SJJKjSZljaiunaTbK6HS5oyve4QSmupT7gWsZULY6JPNTrPWL8q53uiLhLvQAoEdgokLTWTKu4AKphbQtfGsgz2mRX0iRf7HEwWKOj6UWCXkBxGmRBLDwC0PnoGmr8ISjJPvVyoZPL2FvkVF2JlE4i7JTsxe2YNb1TEDV2J743_6UQNjVu1_t009S1HEdUNjP735GDau2WxBEEPwNKeutw0xl7GKxx2iY6bAS0xEeHp5ReVj0L_GQtSqd5beyhqDER6IDzU4KZYdsvcvrHtyIp8AHBP2anjtifhfgZGtZjAmkuqgP28h7mfDqthXHdWh6WJ0CnEUoL1BeL8BtWkP8c8B7dKuHGUNP8_EDTTbWLBzCzb27MtyifjwhNyTsJuxBUuhCn90pOGXytpifYIutX_7vO0AieyqFnY2DUtmKXlHmHjB8Lb4_UMT8Oqj-iR7OoIW5HbkmBq3oQeO0i9gIeZJVRoXQBQnmzI0szg



Commande pour lister les routes

 aws ec2 describe-route-tables --route-table-ids rtb-0a9293aaf3c30b82c --profile devopsteam07 --region eu-central-1 --query 'RouteTables[0].Routes' --output table

Output :

---------------------------------------------------------------------
|                        DescribeRouteTables                        |
+-----------------------+------------+--------------------+---------+
| DestinationCidrBlock  | GatewayId  |      Origin        |  State  |
+-----------------------+------------+--------------------+---------+
|  10.0.0.0/16          |  local     |  CreateRouteTable  |  active |
+-----------------------+------------+--------------------+---------+


Commande pour associer la route table au subnet

aws ec2 associate-route-table --route-table-id rtb-0a9293aaf3c30b82c --subnet-id subnet-01cfa9e1ea9fb3d90--profile devopsteam07 --region eu-central-1 --output table

Output : 

An error occurred (UnauthorizedOperation) when calling the AssociateRouteTable operation: You are not authorized to perform this operation. User: arn:aws:iam::709024702237:user/devopsteam07-i346 is not authorized to perform: ec2:AssociateRouteTable on resource: arn:aws:ec2:eu-central-1:709024702237:subnet/subnet-01cfa9e1ea9fb3d90 because no identity-based policy allows the ec2:AssociateRouteTable action. Encoded authorization failure message: NnJ9dwjZiawcZ8wb06l_MrYWCGkPFW8_bH2oagbBAKJFwjRHBrMePexOwFot6TLgHdN8gbQpOftBjeZifIcMpsirX0ByJxBl_7cBbaMglUDNdzH9y3jqD37ECMzwPid1bE4b68HTSgQuZegAz3ho0cYuSCMQnM0YHatYLSgUn8lYH-5qfSpjDzHSTVtK3RwH0SeBHUjvrcIElqq03tapEdXdFqnr74wtCKc88Q6xvVSSHFFzMcCYPHi8j_vRCFtxsbYrePfJVg4CJx181mL1g5ODCPs543Biizq6WtI901SAq0y0GzmvucJbmaNBfty6hNwtQIoMkp3kQ-FBJAloaK-hDz2RdPzp8gC2UIQvSfCjCtuEyxkj1Q4EBcMTnfrhvRKhqHKOCbfka6C4_zsVrIHmehLau0fAyKVaTCibIOU10JfpU1DlNSmXMGhZLXyVezRjScKH3TV804wlZOV3hnMX12PRu4wEszjAkzKpcqY7kQYWESv8_HCAoKe8PVs6PpQ2MSSmqlW8Kn_1_YhGdrA0j6EX7PnQIP4QQWS3MyBaR9wfvGDC_oyV1wLxXdQMImWe5JEcb1PGJ9WudFPOqv-VK0gYVdLiI2l5o2itYx4tPGFc6XZOi-oRLW2De_VEFAqOFMPSaDr8uaalhmJKJDMpE-v-FaHrORZvgMd2X5u288EDRg



Associer la RouteTable au DMZ

aws ec2 associate-route-table --route-table-id rtb-0a9293aaf3c30b82c --subnet-id xxxxxxxxxxxxxxxx --profile devopsteam07 --region eu-central-1 --output table





Creer un grouper de sécurité sur le subnet

aws ec2 create-security-group --group-name groupe_securite_07_1 --description "Groupe de securite" --vpc-id vpc-0a22d771f16ae549d --region eu-central-1 --profile devopsteam07 --output table

(important de ne pas mettre d'accent ni de manjuscule)

Output :

---------------------------------------------------------------------------------------------------
|                                       CreateSecurityGroup                                       |
+------------------+------------------------------------------------------------------------------+
|  GroupId         |  sg-0b62f418c1fcff284                                                        |
|  SecurityGroupArn|  arn:aws:ec2:eu-central-1:709024702237:security-group/sg-0b62f418c1fcff284   |
+------------------+------------------------------------------------------------------------------+


Supprimer un groupe de sécurité:

aws ec2 delete-security-group --group-id sg-0b62f418c1fcff284  --profile devopsteam07 --region eu-central-1

output :

An error occurred (UnauthorizedOperation) when calling the DeleteSecurityGroup operation: You are not authorized to perform this operation. User: arn:aws:iam::709024702237:user/devopsteam07-i346 is not authorized to perform: ec2:DeleteSecurityGroup on resource: arn:aws:ec2:eu-central-1:709024702237:security-group/sg-0b62f418c1fcff284 because no identity-based policy allows the ec2:DeleteSecurityGroup action. Encoded authorization failure message: 3y8ZICNiehbgUqHnTZMnh4se6129gjOWsvICX4FMimJJLknTNKUtsAoT_faaUVu7ed5F7GM3qIMkMmBFBvMCYvcePqgPf942SsH5ie0AMi-kbdSidzHzIMd1Y0bqmJfDBy6ScLVVRRNS-2F0Y1-xoMRnUsNt59esca0BCxReSkTALUJxS41pX492k6-dOfHw1leBFV2DCie4GHOd7R7QYEpdOY2UfXFq6-pXJc8OjqKMJ0qQT50zq-tiOHO55EkEiQ9YW3i5l6I6npx1XThKimJzKvNpeEpuaNAWtwYA3Mh4uqd1pRjY1j0BzzyaDAuQhttMdaUDxv_8KSJIotQnRPRUT8x_c3RaXkCIqzxMTfL86aU6Zxw5APbySoVyfbBBt9ZrZrisufzVCMm4KBJR7k02D7eZ_mMUCOoIAczE9EsHjrHFcyHh44e7CrAoTVUGN3Br5fydYv9kIwdAv1bVrJELWcjkRuSZIv_hCr0n75b3-jULct8_V-VA5782FS5DCY5YnyFNXkIn7evI8ZLjA9jIxE2hQcYKEwxFd7lTUD0eJ585C5WsewCVNXFus0AeoJV7XZRaw073mQcr3dvO3uDuFkYxefLo0w


Création d'une clé

aws ec2 create-key-pair --key-name groupe_07 --query 'KeyMaterial' --output text --profile devopsteam07 --region eu-central-1 > groupe_07.pem

Output :

Aucun output



Upload une clé
