---
title: Bug 检查位 0xCA PNP_DETECTED_FATAL_ERROR
description: PNP_DETECTED_FATAL_ERROR bug 检查具有 0x000000CA 值。 这指示插 Manager 遇到了错误。
ms.assetid: 2092c4a7-e068-461f-b28e-8063faf5a031
keywords:
- Bug 检查位 0xCA PNP_DETECTED_FATAL_ERROR
- PNP_DETECTED_FATAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PNP_DETECTED_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a9331051725375a909c0ab44260b942de31132f6
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239842"
---
# <a name="bug-check-0xca-pnpdetectedfatalerror"></a>Bug 检查 0xCA：PNP\_DETECTED\_FATAL\_ERROR


PNP\_已检测\_致命错误\_错误 bug 检查的值为 0x000000CA。 这指示插 Manager 遇到了错误，可能是由于有问题即插即用驱动程序。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="pnpdetectedfatalerror-parameters"></a>PNP\_已检测\_致命错误\_错误参数


参数 1 标识冲突的类型。

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
<th align="left">参数 2</th>
<th align="left">参数 3</th>
<th align="left">参数 4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>新报告 PDO 地址</p></td>
<td align="left"><p>较旧的 PDO 其中重复的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p><strong>重复的 PDO:</strong>驱动程序的特定实例具有枚举多个 PDOs 具有相同设备 ID 和唯一 Id。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>声称 PDO 的地址</p></td>
<td align="left"><p>驱动程序对象的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p><strong>无效的 PDO:</strong>已调用 API 需要 PDO 随机内存或 FDO 或 PDO 其尚未初始化。</p>
<p>(未初始化的 PDO 是指尚未返回插入并通过播放<strong>QueryDeviceRelation</strong>或<strong>QueryBusRelations</strong>。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>PDO 查询其 Id 的地址</p></td>
<td align="left"><p>ID 缓冲区的地址</p></td>
<td align="left"><p><strong>1:</strong>DeviceID</p>
<p><strong>2:</strong>UniqueID</p>
<p><strong>3:</strong>HardwareIDs</p>
<p><strong>4:</strong>CompatibleIDs</p></td>
<td align="left"><p><strong>ID 无效：</strong>一个枚举器返回了包含非法字符或未正确终止的 ID。 (必须包含 Id 仅中的字符范围 0x20-0x2B 和 0x2D-0x7F。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>设置与 DOE_DELETE_PENDING PDO 地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p><strong>已删除 PDO 的无效的枚举：</strong>一个枚举器已返回它之前必须删除使用 PDO <strong>IoDeleteDevice</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>PDO 的地址</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p><strong>PDO 释放时在 devnode 树链接：</strong>上一个期间 devnode 仍链接在树中删除为零的 PDO 对象管理器引用计数。 （这通常表示该驱动程序不添加的引用，IRP 的查询中返回 PDO 时。）</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>PDO 其堆栈返回无效总线关系的地址</p></td>
<td align="left"><p>PDOs 作为总线关系返回的总行数</p></td>
<td align="left"><p>索引 （从零开始） 的第一个<strong>NULL</strong> PDO 找</p></td>
<td align="left"><p><strong>作为总线关系返回 NULL 指针：</strong>一个或多个当前总线上的设备是<strong>NULL</strong> PDO。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>传递的连接类型</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p><strong>无效的连接类型传递给 IoDisconnectInterruptEx:</strong>驱动程序已传递到一个无效的连接类型<strong>IoDisconnectInterruptEx</strong>。 传递到此例程的连接类型必须与相应地成功调用返回<strong>IoConnectInterruptEx</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>驱动程序对象</p></td>
<td align="left"><p>从驱动程序回调返回后的 IRQL</p></td>
<td align="left"><p>从驱动程序回调返回后组合的 APC 禁用计数</p></td>
<td align="left"><p><strong>不正确的通知回调行为：</strong>驱动程序无法保留 IRQL 或跨即插即用合并 APC 禁用计数 n 播放通知。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xB</p></td>
<td align="left"><p>相关的 PDO</p></td>
<td align="left"><p>删除关系</p></td>
<td align="left"><p>保留</p></td>
<td align="left"><p><strong>已删除的 PDO 报告为关系：</strong>正在删除设备的删除关系的一个已被删除。</p></td>
</tr>
</tbody>
</table>

 

 

 




