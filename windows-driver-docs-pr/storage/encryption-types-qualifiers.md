---
title: 加密 \_ 类型 \_ 限定符
description: 加密 \_ 类型 \_ 限定符
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 88e0aefa11bd31e9d9d22b5f346386cf79170b9c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835311"
---
# <a name="encryption_types_qualifiers"></a>加密 \_ 类型 \_ 限定符


## <span id="ddk_encryption_types_qualifiers_kr"></span><span id="DDK_ENCRYPTION_TYPES_QUALIFIERS_KR"></span>


加密 \_ 类型 \_ 限定符 WMI 属性限定符对应于一组值，这些值指示 HBA 支持的加密形式。

下表描述了与加密 \_ 类型限定符属性限定符关联的值 \_ 。

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
<td align="left"><p>HBA 支持通过 XCBC 进行 AES CTR/CBC MAC 加密。</p></td>
</tr>
</tbody>
</table>

 

 

 





