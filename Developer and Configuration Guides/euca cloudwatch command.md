euwatch-get-stats CPUUtilization --start-time 2013-06-10T07:09:00.043Z --end-time 2013-06-10T08:46:54.043Z --period 3600 --statistics "Average,Minimum,Maximum" --namespace "AWS/EC2" --dimensions "InstanceId=i-06BC4507"

euscale-create-launch-config MyLC --image-id emi-12C94217 --instance-type m1.small

euscale-create-auto-scaling-group MyASGroup --launch-configuration MyLC --availability-zones clearlogy --min-size 1 --max-size 2

euscale-describe-auto-scaling-groups

euscale-put-scaling-policy MyScaleoutPolicy --auto-scaling-group MyASGroup --adjustment=30 --type PercentChangeInCapacity

euscale-put-scaling-policy MyScaleInPolicy --auto-scaling-group MyASGroup --adjustment=-2  --type ChangeInCapacity

euwatch-put-metric-alarm AddCapacity --metric-name CPUUtilization \
--namespace "AWS/EC2" --statistic Average --period 120 --threshold 80 \
--comparison-operator GreaterThanOrEqualToThreshold --dimensions "AutoScalingGroupName=MyASGroup" \
--evaluation-periods 2 \
--alarm-actions (o/p of euscale-put-scaling-policy MyScaleoutPolicy --auto-scaling-group MyASGroup --adjustment=30 --type PercentChangeInCapacity)arn:aws:autoscaling::077577678152:scalingPolicy:4c60097b-9fba-4362-83df-e04713490c94:autoScalingGroupName/MyASGroup:policyName/MyScaleoutPolicy

euwatch-put-metric-alarm RemoveCapacity --metric-name CPUUtilization \
--namespace "AWS/EC2" --statistic Average --period 120 --threshold 40 \
--comparison-operator LessThanOrEqualToThreshold  --dimensions "AutoScalingGroupName=MyASGroup" \
--evaluation-periods 2 \
--alarm-actions (o/p of scalein policy) arn:aws:autoscaling::576514848852:scalingPolicy:a4148c27-81da-4eff-9140-cba3ba9381cb:autoScalingGroupName/MyASGroup:policyName/MyScaleInPolicy

euwatch-set-alarm-state --state-value OK \
--state-reason "testing" AddCapacity

euwatch-set-alarm-state --state-value OK \
--state-reason "testing" RemoveCapacity

euwatch-get-stats CPUUtilization --start-time 2013-06-10T07:09:00.043Z --end-time 2013-06-10T08:46:54.043Z --period 3600 --statistics "Average,Minimum,Maximum" --namespace "AWS/EC2" --dimensions "InstanceId=i-06BC4507"
 
euscale-create-launch-config MyLC --image-id emi-12C94217 --instance-type m1.small
 
euscale-create-auto-scaling-group MyASGroup --launch-configuration MyLC --availability-zones clearlogy --min-size 1 --max-size 2
 
euscale-describe-auto-scaling-groups
 
euscale-put-scaling-policy MyScaleoutPolicy --auto-scaling-group MyASGroup --adjustment=30 --type PercentChangeInCapacity
 
euscale-put-scaling-policy MyScaleInPolicy --auto-scaling-group MyASGroup --adjustment=-2  --type ChangeInCapacity
 
euwatch-put-metric-alarm AddCapacity --metric-name CPUUtilization \
--namespace "AWS/EC2" --statistic Average --period 120 --threshold 80 \
--comparison-operator GreaterThanOrEqualToThreshold --dimensions "AutoScalingGroupName=MyASGroup" \
--evaluation-periods 2 \
--alarm-actions (o/p of euscale-put-scaling-policy MyScaleoutPolicy --auto-scaling-group MyASGroup --adjustment=30 --type PercentChangeInCapacity)arn:aws:autoscaling::077577678152:scalingPolicy:4c60097b-9fba-4362-83df-e04713490c94:autoScalingGroupName/MyASGroup:policyName/MyScaleoutPolicy
 
euwatch-put-metric-alarm RemoveCapacity --metric-name CPUUtilization \
--namespace "AWS/EC2" --statistic Average --period 120 --threshold 40 \
--comparison-operator LessThanOrEqualToThreshold  --dimensions "AutoScalingGroupName=MyASGroup" \
--evaluation-periods 2 \
--alarm-actions (o/p of scalein policy) arn:aws:autoscaling::576514848852:scalingPolicy:a4148c27-81da-4eff-9140-cba3ba9381cb:autoScalingGroupName/MyASGroup:policyName/MyScaleInPolicy
 
euwatch-set-alarm-state --state-value OK \
--state-reason "testing" AddCapacity
 
euwatch-set-alarm-state --state-value OK \
--state-reason "testing" RemoveCapacity

