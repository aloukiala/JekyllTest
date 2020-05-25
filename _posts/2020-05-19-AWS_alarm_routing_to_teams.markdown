---
layout: post
title:  "AWS alarm routing to Teams"
date:   2020-05-25 22:00:00
categories: jekyll update
---

You start to built an application and early on want to have some monitoring in place. You identify the first key metric and think how to catch these. I run into this problem all the time. I'm not keen on emails, as those seem to get lost and require you to define who to send them to. I really like chats. Teams and Slack give you channels where you can collaborate on the issues rising and it is easy to add people to the channels. 

I typically create a CloudWatch alarms and route them to SNS topic. Attaching a simple Lambda function on this SNS to send the message to the Teams. Teams allows you to create cards, where you can format the message. I created simple card that has some information about the alarm and a link to the metric. I found my self doing this all the time. Creating metrics and routing them to chat channels. This started to repeat itself, so I decided to built a terraform module for it. 

Here is a simple image of the setup. Terraform module sets up SNS and Lambda to which all CloudWatch metric alarms that want to be send to Teams channel are routed to.
![Architecture image](/assets/images/SNSChatHook.svg)

Currently the module supports only Teams endpoint and is tightly connected CloudWatch metric alarms. I'm looking to extend this module to Slack endpoint and have other input messages as well.

You can now find the terraform module from the [terraform registry](https://registry.terraform.io/modules/aloukiala/alarm-chat-notification/aws/0.1.0?tab=resources). Code is also available in my git [repo](https://github.com/aloukiala/terraform-aws-alarm-chat-notification)
