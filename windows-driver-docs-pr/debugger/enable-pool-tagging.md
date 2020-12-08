---
title: 启用池标记
description: 启用池标记
keywords:
- '启用 (全局标志的池标记) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 397d4c1157ad056ed1c664307886824c3d4a0c7d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813273"
---
# <a name="enable-pool-tagging"></a>启用池标记


## <span id="ddk_enable_pool_tagging_dtools"></span><span id="DDK_ENABLE_POOL_TAGGING_DTOOLS"></span>


" **启用池标记** " 标志收集数据并计算按池标记值排序的池内存分配的统计信息。

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
<td align="left"><p>系统范围内的注册表项</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

此标志在 Windows Server 2003 和更高版本的 Windows 中被永久设置。 在这些系统中，"全局标志" 对话框中的 " **启用池标记** " 复选框将灰显，启用或禁用池标记的命令将失败。

使用 **ExAllocatePoolWithTag** 或 **ExAllocatePoolWithQuotaTag** 设置标记值。 如果未指定任何标记值 (**ExAllocatePool**， **ExAllocatePoolWithQuota**) ，Windows 将创建默认值为 "None" 的标记。 由于将所有具有 "无" 标记的分配的数据组合在一起，因此不能将数据与特定分配区分开来。 有关这些例程的信息，请参阅 Windows 驱动程序工具包 (WDK) 。

在 Windows XP 及更早版本的系统中，此标志还会指示 Windows 附加池标记，即使池内存是使用 **ExAllocatePoolWithQuotaTag** 分配的也是如此。 否则，标记字节用于存储配额值。 在 Windows Server 2003 中，标记值和配额值存储在附加到每个池内存分配的单独字段中。

**注意**   若要显示 Windows 为标记分配收集的数据，请使用 PoolMon，它是 Windows 驱动程序工具包中包含的工具。
Windows XP 支持工具文档中的 " **启用池标记** " 标志的说明不完整。 此标志指示 Windows 按标记值收集和处理数据。

 

 

 





