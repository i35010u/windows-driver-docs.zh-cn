---
title: Bug 检查码 0xca PNP_DETECTED_FATAL_ERROR
description: PNP_DETECTED_FATAL_ERROR bug 检查的值为0x000000CA。 这表明即插即用管理器遇到了严重错误。
keywords:
- Bug 检查码 0xca PNP_DETECTED_FATAL_ERROR
- PNP_DETECTED_FATAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PNP_DETECTED_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dee6eed1cf056c3c7294ac5420c959ea5dba920d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825229"
---
# <a name="bug-check-0xca-pnp_detected_fatal_error"></a>Bug 检查码0xca： PNP \_ 检测 \_ 到 \_ 错误


PNP \_ 检测到 \_ \_ 错误 bug 检查的值为0x000000CA。 这表明即插即用管理器遇到了严重错误，可能是即插即用驱动程序出现问题。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="pnp_detected_fatal_error-parameters"></a>PNP \_ 检测 \_ 到 \_ 错误参数


参数1标识冲突类型。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>新报告的 PDO 的地址</p></td>
<td align="left"><p>已复制的旧版 PDO 的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>重<strong>制 PDO：</strong>驱动程序的特定实例已枚举多个具有相同设备 ID 和唯一 Id 的 PDOs。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>假想 PDO 的地址</p></td>
<td align="left"><p>驱动程序对象的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p><strong>PDO 无效：</strong> 需要使用随机内存、FDO 或尚未初始化的 PDO 调用了 PDO 的一个 API。</p>
<p>未初始化的 PDO (<strong>QueryDeviceRelation</strong> 或 <strong>QueryBusRelations</strong>未返回到即插即用。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>查询其 Id 的 PDO 的地址</p></td>
<td align="left"><p>ID 缓冲区的地址</p></td>
<td align="left"><p><strong>1：</strong> DeviceID</p>
<p><strong>2：</strong> UniqueID</p>
<p><strong>3：</strong> HardwareIDs</p>
<p><strong>4：</strong> CompatibleIDs</p></td>
<td align="left"><p><strong>ID 无效：</strong> 枚举器返回一个包含非法字符或未正确终止的 ID。  (Id 必须仅包含介于 0x20-0x2B 和 0x2D-0x7F 范围内的字符。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>具有 DOE_DELETE_PENDING 集的 PDO 的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p><strong>枚举的已删除 PDO 无效：</strong> 枚举器已返回使用 <strong>IoDeleteDevice</strong>删除的 PDO。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>PDO 的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p><strong>在 devnode 树中链接时，已释放 PDO：</strong> 当 devnode 仍在树中链接时，PDO 上的对象管理器引用计数将降到零。  (这通常表明驱动程序在查询 IRP 中返回 PDO 时未添加引用 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>其堆栈返回无效总线关系的 PDO 地址</p></td>
<td align="left"><p>作为总线关系返回的 PDOs 的总数</p></td>
<td align="left"><p>找到第一个 <strong>NULL</strong> PDO (从零开始的索引) </p></td>
<td align="left"><p><strong>作为总线关系返回的 NULL 指针：</strong> 总线上存在的一个或多个设备是 <strong>NULL</strong> PDO。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>传递的连接类型</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p><strong>传递给 IoDisconnectInterruptEx 的连接类型无效：</strong> 驱动程序向 <strong>IoDisconnectInterruptEx</strong>传递了无效的连接类型。 传递到此例程的连接类型必须与相应的成功调用 <strong>IoConnectInterruptEx</strong>返回的类型匹配。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>驱动程序对象</p></td>
<td align="left"><p>从驱动程序回调返回后的 IRQL</p></td>
<td align="left"><p>从驱动程序回调返回后，组合 APC 禁用计数</p></td>
<td align="left"><p><strong>通知回调行为不正确：</strong> 驱动程序无法在插入 "n" 播放通知中保留 IRQL 或合并的 APC 禁用计数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xB</p></td>
<td align="left"><p>相关 PDO</p></td>
<td align="left"><p>删除关系</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p><strong>已删除已报告为关系的 PDO：</strong> 正在删除的设备的删除关系之一已被删除。</p></td>
</tr>
</tbody>
</table>

 

 

 




