---
title: Bug 检查 0x6B PROCESS1_INITIALIZATION_FAILED
description: PROCESS1_INITIALIZATION_FAILED bug 检查具有 0x0000006B 值。 此 bug 检查指示 Microsoft Windows 操作系统的初始化失败。
ms.assetid: 8680d924-3041-4927-a228-52b281bbc267
keywords:
- Bug 检查 0x6B PROCESS1_INITIALIZATION_FAILED
- PROCESS1_INITIALIZATION_FAILED
ms.date: 06/27/2018
topic_type:
- apiref
api_name:
- PROCESS1_INITIALIZATION_FAILED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9dd2a4c37258a5130acb59f7f3c3dbd8d3ef2e94
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361791"
---
# <a name="bug-check-0x6b-process1initializationfailed"></a>Bug 检查 0x6B：PROCESS1\_初始化\_失败


PROCESS1\_初始化\_失败错误检查的值为 0x0000006B。 此 bug 检查指示 Microsoft Windows 操作系统的初始化失败。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="process1initializationfailed-parameters"></a>PROCESS1\_初始化\_失败参数


在蓝色屏幕上显示以下参数。

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
<td align="left"><p>导致失败的 NT 状态代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
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

磁盘子系统的任何部分可能会导致 PROCESS1\_初始化\_失败错误检查，包括损坏的磁盘错误或不正确的电缆，混合使用不同的 ATA 类型设备上的同一个链或不是由于可用的驱动器硬件重新生成。

启动分区中缺少文件或用户无意中禁用的驱动程序也会导致此 bug 检查**驱动程序**选项卡。

 
## <a name="resolution"></a>分辨率
[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。 




