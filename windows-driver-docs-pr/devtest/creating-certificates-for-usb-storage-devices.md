---
title: 为 USB 存储设备创建证书
description: 增强型存储证书管理工具可以创建自签名的证书导入到 IEEE 1667 合规 USB 存储设备。
ms.assetid: c63e69c3-ba60-417e-8838-825d81ac7301
keywords:
- 为 USB 存储设备驱动程序开发工具创建证书
topic_type:
- apiref
api_name:
- Creating
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9fcf3fc5d6ce2bc40e5866c763a8913f5db3dca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380969"
---
# <a name="creating-certificates-for-usb-storage-devices"></a>为 USB 存储设备创建证书


增强型存储证书管理工具可以创建自签名的证书导入到 IEEE 1667 合规 USB 存储设备。 证书的规范中的文本 (.txt) 或初始化 (.ini) 文件存储，必须包含以下条目：

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

## <a name="span-identriesspanspan-identriesspanspan-identriesspanentries"></a><span id="Entries"></span><span id="entries"></span><span id="ENTRIES"></span>条目


<span id="_______Subject______"></span><span id="_______subject______"></span><span id="_______SUBJECT______"></span> **主题**   
此必需的项指定了使用者的证书名称。 此名称必须符合 X.509 标准。

<span id="_______SignatureAlgorithm______"></span><span id="_______signaturealgorithm______"></span><span id="_______SIGNATUREALGORITHM______"></span> **SignatureAlgorithm**   
此必需的项指定用来对证书进行数字签名的算法。 下表所述的签名算法。

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
<td align="left"><p><strong>RSASSA-PSS-SHA1</strong></p></td>
<td align="left"><p>使用 160 位 sha-1 哈希算法 RSASSA-PSS 数字签名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PSS-SHA256</strong></p></td>
<td align="left"><p>使用 256 位 SHA-256 哈希算法 RSASSA-PSS 数字签名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PSS-SHA384</strong></p></td>
<td align="left"><p>使用 384 位 SHA-384 哈希算法 RSASSA-PSS 数字签名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PSS-SHA512</strong></p></td>
<td align="left"><p>使用 512 位 SHA-512 哈希算法 RSASSA-PSS 数字签名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PKCS1_5-SHA1</strong></p></td>
<td align="left"><p>使用 160 位 sha-1 哈希算法 RSASSA PKCS1_5 (PKCS #1 1.5 版) 数字签名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PKCS1_5-SHA256</strong></p></td>
<td align="left"><p>使用 256 位 SHA-256 哈希算法 RSASSA PKCS1_5 数字签名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RSASSA-PKCS1_5-SHA384</strong></p></td>
<td align="left"><p>使用 384 位 SHA-384 哈希算法 RSASSA PKCS1_5 数字签名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RSASSA-PKCS1_5-SHA512</strong></p></td>
<td align="left"><p>使用 512 位 SHA-512 哈希算法 RSASSA PKCS1_5 数字签名。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______KeyType______"></span><span id="_______keytype______"></span><span id="_______KEYTYPE______"></span> **KeyType**   
此必需的项指定使用者密钥类型。 从 Windows 7 开始，此项必须具有的值**RSA**。

<span id="_______KeyStrengh______"></span><span id="_______keystrengh______"></span><span id="_______KEYSTRENGH______"></span> **KeyStrengh**   
此必需的项指定的密钥，其长度 （以位单位） 为依据的强度。

<span id="_______SelfSigned______"></span><span id="_______selfsigned______"></span><span id="_______SELFSIGNED______"></span> **SelfSigned**   
此可选项指定是否由增强存储证书管理工具进行自签名证书。 如果未指定此项，该工具对证书进行签名时创建的证书。

**请注意**  从 Windows 7 开始，不支持值为 NO。 如果未指定，则该工具会发出一条错误消息。

 

<span id="_______ExpirationDate______"></span><span id="_______expirationdate______"></span><span id="_______EXPIRATIONDATE______"></span> **ExpirationDate**   
此所需的项指定证书的有效期结束。 证书的有效期从创建到指定的过期日期的日期。

<span id="_______OrganizationName______"></span><span id="_______organizationname______"></span><span id="_______ORGANIZATIONNAME______"></span> **OrganizationName**   
此可选项指定将证书发布的主题的组织的名称。

<span id="_______OrganizationUnit______"></span><span id="_______organizationunit______"></span><span id="_______ORGANIZATIONUNIT______"></span> **OrganizationUnit**   
此可选项指定将证书发布针对使用者在组织内的业务单位的名称。

<span id="_______CompanyLocation______"></span><span id="_______companylocation______"></span><span id="_______COMPANYLOCATION______"></span> **CompanyLocation**   
此可选条目指定将证书发布针对使用者的公司的街道地址。

<span id="_______State______"></span><span id="_______state______"></span><span id="_______STATE______"></span> **State**   
此可选项指定的州或省的公司将证书发布针对使用者的位置。

<span id="_______ZipCode______"></span><span id="_______zipcode______"></span><span id="_______ZIPCODE______"></span> **ZipCode**   
此可选项指定的公司将证书发布针对使用者的位置的邮政编码。

<span id="_______Country______"></span><span id="_______country______"></span><span id="_______COUNTRY______"></span> **Country**   
此可选项指定国家/地区的公司将证书发布针对使用者的位置。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

必须为证书规范文件中的第一个条目**\[证书\]** 标签。

为证书指定的项区分大小写，但可以按任意顺序指定。

有关如何创建要导入到 IEEE 1667 合规 USB 存储设备的证书的详细信息，请参阅**的新**的参数[ **/add** ](enhstor-add-switch.md)和[ **/替换**](-replace-switch.md)增强存储证书管理工具的开关。

 

 





