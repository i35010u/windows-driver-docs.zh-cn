---
title: 经过身份验证的密钥交换
description: 经过身份验证的密钥交换
ms.assetid: cd8c29ab-6276-4236-9b9c-152adf2868c3
keywords:
- 经过身份验证密钥交换 WDK COPP
- 密钥交换 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 244120aed1b91c30fa13a61aed64e4f218ac526a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347013"
---
# <a name="authenticated-key-exchange"></a>经过身份验证的密钥交换


## <span id="ddk_authenticated_key_exchange_gg"></span><span id="DDK_AUTHENTICATED_KEY_EXCHANGE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

下图显示了建立安全的连接通过身份验证和密钥交换。 首先，微型端口驱动程序提供给应用程序的图形硬件证书。 接下来，应用程序从图形硬件证书中提取的公钥。 应用程序生成的数据完整性密钥之后 (k<sub>DI</sub>)，应用程序使用的公钥来加密一个序列，其中包括数据完整性密钥并提供了驱动程序的序列。

命令和状态消息，随后传递未加密;但是，对于每个消息，Mac 创建使用数据完整性密钥。

![关系图演示身份验证和密钥交换](images/coppkey.png)

有关 Mac 的详细信息，请参阅[基元使用加密 COPP](cryptographic-primitives-used-by-copp.md)。

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
<td align="left"><p>r<sub>GH</sub></p></td>
<td align="left"><p>128 位随机数字生成由驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Cert<sub>GH</sub></p></td>
<td align="left"><p>长度可变的数字证书由图形硬件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P<sub>GH</sub>(r<sub>GH</sub>，k<sub>DI</sub>，status_start，command_start)</p></td>
<td align="left"><p>启动安全通道，其中包括以下各项串联在一起的序列：</p>
<ul>
<li><p>128 位随机数字生成由驱动程序。</p></li>
<li><p>应用程序生成的 128 位随机数据完整性的会话密钥。</p></li>
<li><p>32 位随机起始状态序列号生成的应用程序。</p></li>
<li><p>32 位随机起始命令序列号生成的应用程序。</p></li>
</ul>
<p>应用程序通过使用从图形硬件证书获取的公共密钥加密该序列。 该序列为 2,048 位长;序列的其余部分则用 0 填充。</p></td>
</tr>
</tbody>
</table>

 

 

 





