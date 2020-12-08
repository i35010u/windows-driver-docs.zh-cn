---
title: 状态安全性和真实性
description: 状态安全性和真实性
keywords:
- 状态信息 WDK COPP
- 状态交换 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6abbe20ab751e7f3ad75225f1a277fbc0cb25acd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820805"
---
# <a name="status-security-and-authenticity"></a>状态安全性和真实性


## <span id="ddk_status_security_and_authenticity_gg"></span><span id="DDK_STATUS_SECURITY_AND_AUTHENTICITY_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

下图显示了一个应用程序，该应用程序从视频微型端口驱动程序请求状态消息，然后使用视频微型端口驱动程序通过安全通道将状态消息发送到应用程序。

![说明状态交换的关系图](images/coppstus.png)

这些状态消息包含在信封中。 信封包含数据和 MAC 部分。 视频微型端口驱动程序使用数据完整性密钥和 OMAC 计算状态数据的 MAC。 有关 MAC 和 OMAC 的详细信息，请参阅 [COPP 使用的加密基元](cryptographic-primitives-used-by-copp.md)。

下表描述了上图中的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>r<sub>应用</sub></p></td>
<td align="left"><p>128由应用程序生成的随机数字。</p></td>
</tr>
<tr class="even">
<td align="left"><p>状态</p></td>
<td align="left"><p>可变长度状态数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MAC<sub>KDI</sub> (r<sub>应用</sub>，状态) </p></td>
<td align="left"><p>使用数据完整性会话密钥的状态数据的128位 MAC。</p></td>
</tr>
</tbody>
</table>

 

 

 





