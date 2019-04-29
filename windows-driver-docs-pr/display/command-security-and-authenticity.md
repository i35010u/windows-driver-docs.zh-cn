---
title: 命令安全性和真实性
description: 命令安全性和真实性
ms.assetid: 2a70f974-c34c-4462-a772-d8253f842ed8
keywords:
- WDK COPP 命令
- 命令 exchange WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e27ce3bab19312abf3f704d377e7873521441cb9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382344"
---
# <a name="command-security-and-authenticity"></a>命令安全性和真实性


## <span id="ddk_command_security_and_authenticity_gg"></span><span id="DDK_COMMAND_SECURITY_AND_AUTHENTICITY_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

下图显示了通过安全通道发送到微型端口驱动程序的命令消息的应用程序。

![说明命令 exchange 的关系图](images/coppcmnd.png)

这些命令消息包含在一个信封中。 信封包含数据和 MAC 部分。 应用程序使用的数据完整性密钥和 OMAC 计算 MAC 命令数据。 了解 MAC 和 OMAC 的详细信息，请参阅[基元使用加密 COPP](cryptographic-primitives-used-by-copp.md)。

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
<td align="left"><p>命令</p></td>
<td align="left"><p>长度可变的命令的数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MAC<sub>KDI</sub>(COMMAND)</p></td>
<td align="left"><p>命令使用的数据的数据完整性会话密钥的 128 位 MAC。</p></td>
</tr>
</tbody>
</table>

 

 

 





