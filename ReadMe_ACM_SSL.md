# SSL Certificates

## - What are they ?
SSL Certificates are small data files that digitally bind a cryptographic key to an organisations details. When installed on a web server, It activates the padlock and the https protocol and allow secure connections from a web server to a browser. SSL is used to secure credit card transactions, data transfer and logins, and even social media sites.

SSL Certificates Bind Together - A domain name, hostname or server-name. / Company Name and Location

### How do they work

This particular kind of cryptography harnesses the power of two keys which are long strings of randomly generated numbers.A public key is known to your server and available in the public domain, yet you would need the private key to decrypt data which is transferred.


## - How do you set them up

AWS Certificates Manager is a service that lets you easily provision, manage, and deploy public and private SSL/TLS  certificates for use with AWS services and your internal connected resources. SSL/TLS certificates are used to secure network communications. ACM removes the time consuming process of purchasing, uploading, and renewing SSL/TLS certificates.

ACM allows you to request a certificate, deploy it on AWS resources. And this is an easier way to set up an SSL certificate.

Although you can alternatively do it in a manual way, and the process to do this is:
* Host with a Dedicated IP Address
* Buy a Certificate
* Activate the Certificate
* Install the Certificate
* Update your site to use HTTPs

## - How do you set them up with load balancers

You can use ACM to create an SSL and then on your load balancer use the certificate to terminate the connection and then decrypt request from clients before sending them to the instance.
You can create a certificate using AWS Certificate Manager or a tool that supports the SSL and TLS protocols, such as OpenSSL. You will specify this certificate when you create or update an HTTPS listener for your load balancer. When you create a certificate for use with your load balancer, you must specify a domain name.

---
```hcl
resource "aws_acm_certificate" "example" {
  domain_name       = "example.com"
  validation_method = "DNS"

  tags = {
    Environment = "test"
  }

  lifecycle {
    create_before_destroy = true
  }
}
}

resource "aws_lb" "front_end" {
  # ...
}

resource "aws_lb_listener" "front_end" {
  # ...
}

resource "aws_lb_listener_certificate" "example" {
  listener_arn    = "${aws_lb_listener.front_end.arn}"
  certificate_arn = "${aws_acm_certificate.example.arn}"
}

```

---

# **Sources**
- https://aws.amazon.com/certificate-manager/
- https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/SSL-on-amazon-linux-ami.html
- https://medium.com/@Markus.Hanslik/setting-up-an-ssl-certificate-using-aws-and-terraform-198c6fb90743
- https://www.globalsign.com/en/ssl-information-center/what-is-an-ssl-certificate
- https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/ssl-server-cert.html
- https://www.terraform.io/docs/providers/aws/r/lb_listener_certificate.html
#### Author
**Victor Sibanda** - *Junior DevOps Engineer* - [victorsibanda](https://github.com/victorsibanda)
