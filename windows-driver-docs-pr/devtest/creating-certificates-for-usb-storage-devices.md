---
title: 为 USB 存储设备创建证书
description: 增强的存储证书管理工具可以创建一个自签名证书，将其导入到符合 IEEE 1667 的 USB 存储设备。
keywords:
- 为 USB 存储设备创建证书驱动程序开发工具
topic_type:
- apiref
api_name:
- Creating
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba7e13d9a8f20cf0131c52ad9bce1026524b84a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841046"
---
# <a name="creating-certificates-for-usb-storage-devices"></a>为 USB 存储设备创建证书


增强的存储证书管理工具可以创建一个自签名证书，将其导入到符合 IEEE 1667 的 USB 存储设备。 证书的规范存储在文本 ( .txt) 或 ( .ini) 文件中，并且必须包含以下条目：

```
  [certificate]

    Subject=SubjectString
SignatureAlgorithm=[RSASSA-PSS-SHA1|
        RSASSA-PSS-SHA384|
        RSASSA-PSS-SHA512|
        RSASSA-PKCS1_5-SHA1|
        RSASSA-PKCS1_5-SHA256|
        RSASSA-PKCS1_5-SHA384|
        RSASSA-PKCS1_5-SHA512]
KeyType=RSAKeyStrength=[1024|2048|3072]
ExpirationDate=mm/dd/yy
[SelfSigned=[YES|NO]]
[OrganizationName=OrgNameString]
[OrganizationUnit=OrgUnitString]
[CompanyLocation=LocationString]
[State=StateString]
[ZipCode=ZipCodeString]
[Country=CountryString]
```

## <a name="span-identriesspanspan-identriesspanspan-identriesspanentries"></a><span id="Entries"></span><span id="entries"></span><span id="ENTRIES"></span>日志


<span id="_______Subject______"></span><span id="_______subject______"></span><span id="_______SUBJECT______"></span>**主题**   
此必需条目指定主题的证书名称。 此名称必须符合 x.509 标准。

<span id="_______SignatureAlgorithm______"></span><span id="_______signaturealgorithm______"></span><span id="_______SIGNATUREALGORITHM______"></span>**SignatureAlgorithm**   
此必需条目指定用于对证书进行数字签名的算法。 下表描述了签名算法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SignatureAlgorithm 值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PKCS-V1.5-PPS-SHA1</strong></p></td>
<td align="left"><p>使用160位 SHA-1 哈希算法的 RSASSA-PKCS-V1.5-PSS 数字签名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PKCS-V1.5-PSS-SHA256</strong></p></td>
<td align="left"><p>使用256位 SHA-256 哈希算法的 RSASSA-PKCS-V1.5-PSS 数字签名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PKCS-V1.5-PSS-SHA384</strong></p></td>
<td align="left"><p>使用384位 SHA-384 哈希算法的 RSASSA-PKCS-V1.5-PSS 数字签名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PKCS-V1.5-PSS-SHA512</strong></p></td>
<td align="left"><p>使用512位 SHA-512 哈希算法的 RSASSA-PKCS-V1.5-PSS 数字签名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PKCS-V1.5-PKCS1_5-SHA1</strong></p></td>
<td align="left"><p>RSASSA-PKCS-V1.5 PKCS1_5 (PKCS # 1 版本 1.5) 使用160位 SHA-1 哈希算法的数字签名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PKCS-V1.5-PKCS1_5-SHA256</strong></p></td>
<td align="left"><p>使用256位 SHA-256 哈希算法的 PKCS1_5 RSASSA-PKCS-V1.5 数字签名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PKCS-V1.5-PKCS1_5-SHA384</strong></p></td>
<td align="left"><p>使用384位 SHA-384 哈希算法的 PKCS1_5 RSASSA-PKCS-V1.5 数字签名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PKCS-V1.5-PKCS1_5-SHA512</strong></p></td>
<td align="left"><p>使用512位 SHA-512 哈希算法的 PKCS1_5 RSASSA-PKCS-V1.5 数字签名。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______KeyType______"></span><span id="_______keytype______"></span><span id="_______KEYTYPE______"></span>**KeyType**   
此必需条目指定主题的密钥类型。 从 Windows 7 开始，此项的值必须为 **RSA**。

<span id="_______KeyStrengh______"></span><span id="_______keystrengh______"></span><span id="_______KEYSTRENGH______"></span>**KeyStrengh**   
此必需条目指定密钥的强度，该密钥基于其长度 (以) 的位数为单位。

<span id="_______SelfSigned______"></span><span id="_______selfsigned______"></span><span id="_______SELFSIGNED______"></span>**SelfSigned**   
此可选条目指定证书是否由增强的存储证书管理工具自签名。 如果未指定此项，则在创建证书时，该工具会对证书进行签名。

**注意**  从 Windows 7 开始，不支持值为 "否"。 如果未指定，则该工具将发出错误消息。

 

<span id="_______ExpirationDate______"></span><span id="_______expirationdate______"></span><span id="_______EXPIRATIONDATE______"></span>**ExpirationDate**   
此必需条目指定证书有效期的结束时间。 证书的有效期从创建日期到指定的到期日期。

<span id="_______OrganizationName______"></span><span id="_______organizationname______"></span><span id="_______ORGANIZATIONNAME______"></span>**OrganizationName**   
此可选条目指定正在为主题发布证书的组织的名称。

<span id="_______OrganizationUnit______"></span><span id="_______organizationunit______"></span><span id="_______ORGANIZATIONUNIT______"></span>**OrganizationUnit**   
此可选条目指定组织中发布主题证书的业务单元的名称。

<span id="_______CompanyLocation______"></span><span id="_______companylocation______"></span><span id="_______COMPANYLOCATION______"></span>**CompanyLocation**   
此可选条目指定正在为主题发布证书的公司的街道地址。

<span id="_______State______"></span><span id="_______state______"></span><span id="_______STATE______"></span>**状态**   
此可选条目指定为其发布证书的公司所在的国家/地区的省/市/自治区。

<span id="_______ZipCode______"></span><span id="_______zipcode______"></span><span id="_______ZIPCODE______"></span>**ZipCode**   
此可选条目指定为其发布证书的公司所在位置的邮政编码。

<span id="_______Country______"></span><span id="_______country______"></span><span id="_______COUNTRY______"></span>**国家/地区**   
此可选条目指定为其发布证书的公司所在的国家/地区。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

证书规范文件中的第一项必须是 **\[ 证书 \]** 标签。

证书规格项区分大小写，但可以按任意顺序指定。

有关如何创建证书以导入到符合 IEEE 1667 的 USB 存储设备的详细信息，请参阅增强的存储证书管理工具的 [**/add**](enhstor-add-switch.md)和 [**/Replace**](-replace-switch.md)开关的 **新** 参数。

 

 





