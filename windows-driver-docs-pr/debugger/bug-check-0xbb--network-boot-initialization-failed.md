---
title: Bug 检查 0xBB NETWORK_BOOT_INITIALIZATION_FAILED
description: NETWORK_BOOT_INITIALIZATION_FAILED bug 检查的值为0x000000BB。 这表明 Windows 未能成功地从网络启动。
keywords:
- Bug 检查 0xBB NETWORK_BOOT_INITIALIZATION_FAILED
- NETWORK_BOOT_INITIALIZATION_FAILED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- NETWORK_BOOT_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6c6c19a117b1584a35fc283501c0575e88e395e0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838239"
---
# <a name="bug-check-0xbb-network_boot_initialization_failed"></a>Bug 检查0xBB：网络 \_ 启动 \_ 初始化 \_ 失败


网络 \_ 启动 \_ 初始化 \_ 失败 bug 检查的值为0x000000BB。 这表明 Windows 未能成功地从网络启动。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="network_boot_initialization_failed-parameters"></a>网络 \_ 启动 \_ 初始化 \_ 失败参数


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
<td align="left"><p>失败的网络初始化部分。 可能的值为：</p>
<p><strong>1：</strong> 更新注册表时失败。</p>
<p><strong>2：</strong> 启动网络堆栈时失败。 Windows 将 IOCTLs 发送到重定向程序和数据报接收器，然后等待重定向程序准备就绪。 如果在特定时间段内未准备就绪，则会发出此错误。</p>
<p><strong>3：</strong> 将 DHCP IOCTL 发送到 TCP 时失败。 这是 Windows 通知其 IP 地址的传输方式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>失败状态</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

当 Windows 在网络上启动时，此错误将导致，而关键功能在 i/o 初始化过程中失败。

 

 




