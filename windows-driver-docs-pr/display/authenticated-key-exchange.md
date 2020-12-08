---
title: 经过身份验证的密钥交换
description: 经过身份验证的密钥交换
keywords:
- 经过身份验证的密钥交换 WDK COPP
- 密钥交换 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91b0d1d83d126ad5054eef0577cf983ed3b5d611
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810467"
---
# <a name="authenticated-key-exchange"></a>经过身份验证的密钥交换


## <span id="ddk_authenticated_key_exchange_gg"></span><span id="DDK_AUTHENTICATED_KEY_EXCHANGE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

下图显示通过身份验证和密钥交换建立安全连接。 首先，视频微型端口驱动程序将图形硬件证书提供给应用程序。 接下来，应用程序从图形硬件证书中提取公钥。 在应用程序生成数据完整性密钥 (k<sub>DI</sub>) 后，应用程序将使用公钥来加密包含数据完整性密钥的序列，并向驱动程序提供序列。

然后，将通过未加密的命令和状态消息进行传递;但是，对于每个消息，将使用数据完整性密钥来创建 Mac。

![阐释身份验证和密钥交换的关系图](images/coppkey.png)

有关 Mac 的详细信息，请参阅 [COPP 使用的加密基元](cryptographic-primitives-used-by-copp.md)。

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
<td align="left"><p>r<sub>GH</sub></p></td>
<td align="left"><p>128由驱动程序生成的随机数字。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Cert<sub>GH</sub></p></td>
<td align="left"><p>图形硬件使用的可变长度数字证书。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>P<sub>GH</sub> (r<sub>GH</sub>，k<sub>DI</sub>，status_start，command_start) </p></td>
<td align="left"><p>安全通道的启动顺序，其中包含连接在一起的以下项：</p>
<ul>
<li><p>128由驱动程序生成的随机数字。</p></li>
<li><p>应用程序生成的128位随机数据完整性会话密钥。</p></li>
<li><p>由应用程序生成的32位随机起始状态序列号。</p></li>
<li><p>32位随机起始命令序列号由应用程序生成。</p></li>
</ul>
<p>应用程序通过使用从图形硬件证书获取的公钥来加密该序列。 序列的长度为2048位;序列的其余部分以0填充。</p></td>
</tr>
</tbody>
</table>

 

 

 





