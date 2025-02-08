# Laboratório 5: Notificações de Upload/Exclusão no S3 com SNS e SQS

**Curso:** Preparatório para o exame AWS Solutions Architect Associate (C03)


**Instituição:** [Escola da Nuvem](https://escoladanuvem.org/)


**Turma:** DPCN07 - JAN/2025

**Professora:** [Josely Castro](https://www.linkedin.com/in/joselybcastro)

## [Instruções Passo a Passo para o Lab 5](./Lab%205.%20Integração%20e%20Mensageria%20com%20SQS%20e%20SNS%20-%20Passo%20a%20Passo%20Detalhado.pdf) 📜
## [Policies JSON](#policies-json) 📑
## [Prints do Lab](#prints) 🔥

---

## Policies JSON

**Política SNS**
```yam
{
  "Version": "2008-10-17",
  "Id": "__default_policy_ID",
  "Statement": [
    {
      "Sid": "__default_statement_ID",
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": [
        "SNS:Publish",
        "SNS:RemovePermission",
        "SNS:SetTopicAttributes",
        "SNS:DeleteTopic",
        "SNS:ListSubscriptionsByTopic",
        "SNS:GetTopicAttributes",
        "SNS:Receive",
        "SNS:AddPermission",
        "SNS:Subscribe"
      ],
      "Resource": "COLE AQUI O ARN DO SEU TÓPICO SNS",
      "Condition": {
        "StringEquals": {
          "AWS:SourceOwner": "SEU ID DE CONTA DA AWS (12 DÍGITOS)"
        }
      }
    },
    {
      "Sid": "AllowS3ToPublishToTopic",
      "Effect": "Allow",
      "Principal": {
        "Service": "s3.amazonaws.com"
      },
      "Action": "SNS:Publish",
      "Resource": "COLE AQUI O ARN DO SEU TÓPICO SNS",
      "Condition": {
        "ArnLike": {
          "aws:SourceArn": "COLE AQUI O ARN DO SEU BUCKET S3"
        }
      }
    }
  ]
}
```

**Política da Fila SQS**
```yam
{
  "Version": "2012-10-17",
  "Id": "__default_policy_ID",
  "Statement": [
    {
      "Sid": "__default_statement_ID",
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": [
        "SQS:SendMessage",
        "SQS:ReceiveMessage",
        "SQS:DeleteMessage",
        "SQS:GetQueueAttributes",
        "SQS:SetQueueAttributes",
        "SQS:ListQueues"
      ],
      "Resource": "COLE AQUI O ARN DA SUA FILA SQS"
    },
    {
      "Sid": "AllowSNSToSendMessageToSQS",
      "Effect": "Allow",
      "Principal": {
        "Service": "sns.amazonaws.com"
      },
      "Action": "sqs:SendMessage",
      "Resource": "COLE AQUI O ARN DA SUA FILA SQS",
      "Condition": {
        "ArnEquals": {
          "aws:SourceArn": "COLE AQUI O ARN DO SEU TÓPICO SNS"
        }
      }
    }
  ]
}
```

---

## Prints

![p1](https://github.com/user-attachments/assets/810323f8-342f-448a-8f38-45e94cfbfce0)

![p2](https://github.com/user-attachments/assets/5530655f-b715-4efa-b6ea-708bdaa61e89)

![p3](https://github.com/user-attachments/assets/f66fc641-7763-44dc-9789-bc99e71c47f9)

![p4](https://github.com/user-attachments/assets/a65d51ff-58a6-4c0b-be29-e60117d6db40)

![p5](https://github.com/user-attachments/assets/d0dc7fde-8e4c-4ee8-9f06-30d0aeb6e98b)

![p6](https://github.com/user-attachments/assets/56f1cd40-9a79-48ed-9ef2-3ef5ab107c70)

![p7](https://github.com/user-attachments/assets/b00cabc6-5a6a-4704-84cb-7c9bb2853483)

![p8](https://github.com/user-attachments/assets/1e830669-2892-4fca-b703-dbc2910105d4)

![p9](https://github.com/user-attachments/assets/da403579-3099-4771-88ac-5bc41225ac57)

---

- Laboratórios relacionados
	- [Monitoramento de NGINX com Python + SNS](https://github.com/nolascojoao/monitoramento-nginx-com-python-sns)
	- [AWS SNS Image Notification Lab](https://github.com/nolascojoao/aws-sns-lab)
