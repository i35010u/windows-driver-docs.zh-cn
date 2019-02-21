---
title: 启用标记池
description: 启用标记池
ms.assetid: e88f97a0-a8c3-4162-871a-b78671b902bb
keywords:
- 启用池标记 （全局标志）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dabbd77f722b6d6b55c0062b42487ea6432a08d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526833"
---
# <a name="enable-pool-tagging"></a>启用标记池


## <span id="ddk_enable_pool_tagging_dtools"></span><span id="DDK_ENABLE_POOL_TAGGING_DTOOLS"></span>


**启用池标记**标志收集数据并计算池按池标记值排序的内存分配的相关统计信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>缩写</strong></p></td>
<td align="left"><p>ptg</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>十六进制值</strong></p></td>
<td align="left"><p>0x400</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>符号名称</strong></p></td>
<td align="left"><p>FLG_POOL_ENABLE_TAGGING</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>整个系统的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

Windows Server 2003 和更高版本的 Windows 中永久设置此标志。 在这些系统上**启用池标记**全局标志对话框中的复选框呈灰色和命令来启用或禁用池标记失败。

使用**ExAllocatePoolWithTag**或**ExAllocatePoolWithQuotaTag**设置标记值。 当未指定任何标记值 (**ExAllocatePool**， **ExAllocatePoolWithQuota**)，Windows 创建一个标记，默认值为"None。 因为所有分配，则使用"无"结合使用标记的数据，您无法区分特定分配的数据。 有关这些例程的信息，请参阅 Windows Driver Kit (WDK)。

在 Windows XP 和早期系统中，此标志还指示 Windows 将池标记附加即使通过使用分配的池内存**ExAllocatePoolWithQuotaTag**。 否则，使用标记字节来存储配额值。 在 Windows Server 2003 中，标记值和配额值存储在附加到每个池的内存分配的不同域中。

**请注意**  若要显示 Windows 收集有关标记的分配的数据，请使用 PoolMon，Windows 驱动程序工具包中包含的工具。
说明**启用池标记**Windows XP 支持工具文档中的标志是不完整。 此标志指示 Windows 收集和处理数据的标记值。

 

 

 





