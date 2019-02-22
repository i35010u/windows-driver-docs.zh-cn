---
title: 加密\_类型\_限定符
description: 加密\_类型\_限定符
ms.assetid: a1caedb8-18ab-4810-ac46-691925df250e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5f5b6b6e139ed6eacb8df1b1712b909ecdbeb7ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524964"
---
# <a name="encryptiontypesqualifiers"></a>加密\_类型\_限定符


## <span id="ddk_encryption_types_qualifiers_kr"></span><span id="DDK_ENCRYPTION_TYPES_QUALIFIERS_KR"></span>


加密\_类型\_限定符 WMI 属性限定符的值，用于指示哪些形式的加密 HBA 支持一组相对应。

下表描述了与加密相关联的值\_类型\_限定符属性限定符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">符号常量</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ISCSI_ENCRYPT_NONE</p></td>
<td align="left"><p>主机总线适配器 (HBA) 不支持任何形式的加密或身份验证。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_ENCRYPT_3DES_HMAC_SHA1</p></td>
<td align="left"><p>HBA 支持 3DES HMAC/SHA1 加密。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_ENCRYPT_AES_CTR</p></td>
<td align="left"><p>HBA 支持使用 XCBC AES CTR CBC MAC 加密。</p></td>
</tr>
</tbody>
</table>

 

 

 





