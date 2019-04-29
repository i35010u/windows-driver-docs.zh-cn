---
title: 状态安全性和真实性
description: 状态安全性和真实性
ms.assetid: 554d74ee-26fb-4e75-b799-c55c6bdd0153
keywords:
- WDK COPP 的状态信息
- 状态 exchange WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f51d9830df9a37c3d8bc14b782344922c23d3c55
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376042"
---
# <a name="status-security-and-authenticity"></a>状态安全性和真实性


## <span id="ddk_status_security_and_authenticity_gg"></span><span id="DDK_STATUS_SECURITY_AND_AUTHENTICITY_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

下图显示应用程序请求状态消息从微型端口驱动程序，然后通过安全通道发送到应用程序的状态消息的微型端口驱动程序。

![说明状态 exchange 的关系图](images/coppstus.png)

这些状态消息包含在一个信封中。 信封包含数据和 MAC 部分。 微型端口驱动程序使用的数据完整性密钥和 OMAC 计算状态数据的 MAC。 了解 MAC 和 OMAC 的详细信息，请参阅[基元使用加密 COPP](cryptographic-primitives-used-by-copp.md)。

下表介绍了在上图中的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>r<sub>APP</sub></p></td>
<td align="left"><p>128 位随机数字生成由应用程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>状态</p></td>
<td align="left"><p>长度可变的状态数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MAC<sub>KDI</sub>(r<sub>APP</sub>, STATUS)</p></td>
<td align="left"><p>使用数据完整性会话密钥的状态数据的 128 位 MAC。</p></td>
</tr>
</tbody>
</table>

 

 

 





