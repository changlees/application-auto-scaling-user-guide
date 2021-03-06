# Service\-Linked Roles for Application Auto Scaling<a name="application-auto-scaling-service-linked-roles"></a>

Application Auto Scaling uses service\-linked roles for the permissions that it requires to call other AWS services on your behalf\. A service\-linked role is a unique type of AWS Identity and Access Management \(IAM\) role that is linked directly to an AWS service\. 

Service\-linked roles provide a secure way to delegate permissions to AWS services because only the linked service can assume a service\-linked role\. For more information, see [Using Service\-Linked Roles](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html) in the *IAM User Guide*\.

You can delete the roles only after first deleting their related resources\. This protects your resources because you can't inadvertently remove permissions to access the resources\. 

## Permissions Granted by the Service\-Linked Roles<a name="service-linked-role-permissions"></a>

Application Auto Scaling uses the following service\-linked roles to manage scaling on your behalf\. There is one service\-linked role per type of scalable resource\. In each case, the service\-linked role is a predefined role that includes all the necessary permissions\. Each service\-linked role trusts the specified service principal to assume it\.

**AWSServiceRoleForApplicationAutoScaling\_AppStreamFleet**

Actions:
+ `appstream:DescribeFleets`
+ `appstream:UpdateFleet`
+ `cloudwatch:DeleteAlarms`
+ `cloudwatch:DescribeAlarms`
+ `cloudwatch:PutMetricAlarm`

Service principal: `appstream.application-autoscaling.amazonaws.com`

**AWSServiceRoleForApplicationAutoScaling\_DynamoDBTable**

Actions:
+ `dynamodb:DescribeTable`
+ `dynamodb:UpdateTable`
+ `cloudwatch:DeleteAlarms`
+ `cloudwatch:DescribeAlarms`
+ `cloudwatch:PutMetricAlarm`

Service principal: `dynamodb.application-autoscaling.amazonaws.com`

**AWSServiceRoleForApplicationAutoScaling\_EC2SpotFleetRequest**

Actions:
+ `ec2:DescribeSpotFleetRequests`
+ `ec2:ModifySpotFleetRequest`
+ `cloudwatch:DeleteAlarms`
+ `cloudwatch:DescribeAlarms`
+ `cloudwatch:PutMetricAlarm`

Service principal: `ec2.application-autoscaling.amazonaws.com`

**AWSServiceRoleForApplicationAutoScaling\_ECSService**

Actions:
+ `ecs:DescribeServices`
+ `ecs:UpdateService`
+ `cloudwatch:DeleteAlarms`
+ `cloudwatch:DescribeAlarms`
+ `cloudwatch:PutMetricAlarm`

Service principal: `ecs.application-autoscaling.amazonaws.com`

**AWSServiceRoleForApplicationAutoScaling\_RDSCluster**

Actions:
+ `rds:AddTagsToResource`
+ `rds:CreateDBInstance`
+ `rds:DeleteDBInstance`
+ `rds:DescribeDBClusters`
+ `rds:DescribeDBInstance`
+ `cloudwatch:DeleteAlarms`
+ `cloudwatch:DescribeAlarms`
+ `cloudwatch:PutMetricAlarm`

Service principal: `rds.application-autoscaling.amazonaws.com`

**AWSServiceRoleForApplicationAutoScaling\_SageMakerEndpoint**

Actions:
+ `sagemaker:DescribeEndpoint`
+ `sagemaker:DescribeEndpointConfig`
+ `sagemaker:UpdateEndpointWeightsAndCapacities`
+ `cloudwatch:DeleteAlarms`
+ `cloudwatch:DescribeAlarms`
+ `cloudwatch:PutMetricAlarm`

Service principal: `sagemaker.application-autoscaling.amazonaws.com`

**AWSServiceRoleForApplicationAutoScaling\_CustomResource**

Actions:
+ `execute-api:Invoke`
+ `cloudwatch:DeleteAlarms `
+ `cloudwatch:DescribeAlarms `
+ `cloudwatch:PutMetricAlarm `

Service principal: `custom-resource.application-autoscaling.amazonaws.com `

## Create Service\-Linked Roles \(Automatic\)<a name="create-service-linked-role-automatic"></a>

Under most circumstances, you don't need to manually create a service\-linked role\. Application Auto Scaling creates the appropriate service\-linked role for you when you call `RegisterScalableTarget`\. For example, if you set up automatic scaling for an Amazon ECS service, Application Auto Scaling creates the `AWSServiceRoleForApplicationAutoScaling_ECSService` role\.

**Important**  
The IAM user calling the `RegisterScalableTarget` action must have the appropriate IAM permissions to create the service\-linked role\. Otherwise, the automatic creation fails\. For more information, see [Service\-Linked Role Permissions](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Create Service\-Linked Roles \(Manual\)<a name="create-service-linked-role-manual"></a>

To create the service\-linked role, you can use the IAM console, AWS CLI, or IAM API\. For more information, see [Creating a Service\-Linked Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\.

## Edit the Service\-Linked Roles<a name="edit-service-linked-role"></a>

Because various entities might reference a service\-linked role, you cannot change the name of the role\. 

However, you can edit the description of a service\-linked role created for Application Auto Scaling using IAM\. For more information, see [Editing a Service\-Linked Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Delete the Service\-Linked Roles<a name="delete-service-linked-role"></a>

If you no longer use Application Auto Scaling with a type of scalable resource, we recommend that you delete the corresponding service\-linked role\. You can delete a service\-linked role only after first deleting the related scalable resources\. For more information, see the documentation for the scalable resource\. For example, to delete an ECS service, see [Deleting a Service](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/delete-service.html) in the *Amazon Elastic Container Service Developer Guide*\.

To delete service\-linked roles, you can use the IAM console, the IAM CLI, or the IAM API \. For more information, see [Deleting a Service\-Linked Role](http://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

After you delete a service\-linked role, Application Auto Scaling creates the role again when you call `RegisterScalableTarget`\.