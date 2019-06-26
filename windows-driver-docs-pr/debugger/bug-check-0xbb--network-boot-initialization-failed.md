---
title: Bug 检查 0xBB NETWORK_BOOT_INITIALIZATION_FAILED
description: NETWORK_BOOT_INITIALIZATION_FAILED bug 检查具有 0x000000BB 值。 这表示 Windows 无法关闭网络已成功启动。
ms.assetid: 1cc86ca0-437d-4a26-90ed-76f122c522ef
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
ms.openlocfilehash: 092a15498775fd6789ee923a04de9af0a21d803c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367221"
---
# <a name="bug-check-0xbb-networkbootinitializationfailed"></a>Bug 检查 0xBB：网络\_引导\_初始化\_失败


网络\_引导\_初始化\_失败错误检查的值为 0x000000BB。 这表示 Windows 无法关闭网络已成功启动。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="networkbootinitializationfailed-parameters"></a>网络\_引导\_初始化\_失败参数


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
<td align="left"><p>失败的网络初始化的一部分。 可能的值为：</p>
<p><strong>1:</strong>更新注册表时发生故障。</p>
<p><strong>2:</strong>启动网络堆栈时失败。 Windows 将 Ioctl 发送到重定向程序和数据报接收方，然后等待重定向程序准备就绪。 如果还没有准备好在一段时间内，将发出此错误消息。</p>
<p><strong>3:</strong>将 DHCP IOCTL 发送到 TCP 时失败。 这是 Windows 如何通知其 IP 地址的传输。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>故障状态</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Windows 启动关闭网络，并在 I/O 初始化过程中一项重要功能失败时，会出现此错误。

 

 




