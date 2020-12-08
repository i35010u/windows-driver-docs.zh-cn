---
title: Bug 检查 0xBC NETWORK_BOOT_DUPLICATE_ADDRESS
description: NETWORK_BOOT_DUPLICATE_ADDRESS bug 检查的值为0x000000BC。 这表示从网络启动时，为此计算机分配了重复的 IP 地址。
keywords:
- Bug 检查 0xBC NETWORK_BOOT_DUPLICATE_ADDRESS
- NETWORK_BOOT_DUPLICATE_ADDRESS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NETWORK_BOOT_DUPLICATE_ADDRESS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8f0121f13d8d18d7f1643db4541f9ee7088630b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838237"
---
# <a name="bug-check-0xbc-network_boot_duplicate_address"></a>Bug 检查0xBC：网络 \_ 启动 \_ 重复 \_ 地址


网络 \_ 启动 \_ 重复 \_ 地址错误检查的值为0x000000BC。 这表示从网络启动时，为此计算机分配了重复的 IP 地址。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="network_boot_duplicate_address-parameters"></a>网络 \_ 启动 \_ 重复 \_ 地址参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>以 DWORD 形式显示的 IP 地址。 格式为 <em>aa.bb.cc.dd</em> 的地址将显示为0xDDCCBBAA。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>另一台计算机的硬件地址。 对于以太网连接 (，请参阅以下说明。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>另一台计算机的硬件地址。 对于以太网连接 (，请参阅以下说明。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>另一台计算机的硬件地址。 对于以太网连接 (，此值将为零。 ) </p></td>
</tr>
</tbody>
</table>

 

**注意**   当参数4等于零时，这表示以太网连接。 在这种情况下，将在参数2和参数3中存储 MAC 地址。 格式为 *aa-bb---* ------Ff 的以太网 MAC 地址会导致参数2等于0xAABBCCDD，并使用参数3来0xEEFF0000。

 

<a name="cause"></a>原因
-----

此错误表示当 TCP/IP 发出 IP 地址的 ARP 时，会收到来自另一台计算机的响应，指示存在重复的 IP 地址。

当 Windows 在网络上启动时，这是一个严重错误。

 

 




