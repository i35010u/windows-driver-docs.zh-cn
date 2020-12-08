---
title: 调试 \_ 状态 \_ XXX
description: 调试 \_ 状态 \_ XXX
ms.date: 12/07/2017
keywords:
- DEBUG_STATUS_XXX Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_STATUS_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 6600374a258498825bc1f71ecc3900caf20e9a16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838825"
---
# <a name="debug_status_xxx"></a>调试 \_ 状态 \_ XXX


## <span id="ddk_debug_status_xxx_dbx"></span><span id="DDK_DEBUG_STATUS_XXX_DBX"></span>


调试 \_ 状态 \_ *XXX* 状态代码有两个用途。 它们指示引擎在目标中的执行如何继续，引擎使用这些方法来报告目标的执行状态。

事件发生后，引擎可能会收到若干说明，告诉它应如何继续目标中的执行。 在这种情况下，它对具有最高优先级的指令进行操作。 通常，较高优先级的状态代码表示更少的目标执行。

下表中的值按优先级反向排序;表中前面显示的值具有更高的优先级。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状态代码</th>
<th align="left">报告时</th>
<th align="left">指示</th>
<th align="left">优先级</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_NO_DEBUGGEE</p></td>
<td align="left"><p>无调试会话处于活动状态。</p></td>
<td align="left"><p>空值</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_OUT_OF_SYNC</p></td>
<td align="left"><p>调试器通信通道不同步。</p></td>
<td align="left"><p>空值</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_WAIT_INPUT</p></td>
<td align="left"><p>目标正在等待来自用户的输入。</p></td>
<td align="left"><p>空值</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_TIMEOUT</p></td>
<td align="left"><p>调试器通信通道已超时。</p></td>
<td align="left"><p>空值</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_BREAK</p></td>
<td align="left"><p>目标被挂起。</p></td>
<td align="left"><p>挂起目标。</p></td>
<td align="left"><p>最高优先级</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_STEP_INTO</p></td>
<td align="left"><p>目标正在执行一个指令。</p></td>
<td align="left"><p>针对单个指令继续执行目标。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_STEP_BRANCH</p></td>
<td align="left"><p>目标将在执行下一个分支指令之前执行。</p></td>
<td align="left"><p>继续执行目标，直到下一个分支指令。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_STEP_OVER</p></td>
<td align="left"><p>目标正在执行单个指令或--如果该指令为子程序调用--子程序。</p></td>
<td align="left"><p>针对单个指令继续执行目标。 如果指令为子程序调用，则会输入调用，并允许目标运行到子例程返回为止。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_GO_NOT_HANDLED</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>继续执行目标，将事件标记为 "未处理"。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_GO_HANDLED</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>继续执行目标，将事件标记为已处理。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_GO</p></td>
<td align="left"><p>目标正在正常执行。</p></td>
<td align="left"><p>继续执行目标的正常执行。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_IGNORE_EVENT</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>继续之前的目标执行，忽略事件。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_RESTART_REQUESTED</p></td>
<td align="left"><p>目标正在重新启动。</p></td>
<td align="left"><p>重新启动目标。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_NO_CHANGE</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>无说明。 当事件回调方法不希望指示引擎如何在目标中继续执行时，会返回此值。</p></td>
<td align="left"><p>最低优先级</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 状态代码的优先级不遵循常量的数值。



<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">DbgEng (包含 DbgEng) </td>
</tr>
</tbody>
</table>

 

 





