---
title:  "AWS: Hospedando Site Estatico no S3"
date:   2017-05-07 15:25:00
description: Hospedando conteudo estatico a baixo custo
---

Como o AWS Simple Storage System, S3, você pode hospedar seu site estatico (HTML, CSS e Javascript) a um preço extremamente baixo, praticamente de graça. E o melhor seu site fica replicado entre varios datacenter com alta disponibilidade. E tudo isso é muito facil de fazer.


1. Criar um bucket no s3

O bucket precisa ter o mesmo nome o dominio que você vai hospedar nele.
![](https://s3.amazonaws.com/yagonobre.com/01.png)
Digite o nome do seu bucket escolha a região e clique em "Create".

2. Faça o upload dos seus arquivos

Basta arrastar seus arquivos para dentro do seu bucket ;)

3. Deixe seus arquivos publicos

Va em Permissions -> Bucket Policy e adicione a seguinte politica
{% highlight bash %}
{
	"Version":"2008-10-17",
	"Statement":[{
	"Sid":"AllowPublicRead",
		"Effect":"Allow",
		"Principal": {
			"AWS": "*"
			},
		"Action":["s3:GetObject"],
		"Resource":["arn:aws:s3:::SEUDOMINIO.COM/*"
		]
	}
	]
}
{% endhighlight %}
