---
title: 启用池标记
description: 启用池标记
keywords:
- '启用 (全局标志的池标记) '
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: ec1a1fc2076fe32be3e048069771c8623e5838e1
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648180"
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

 

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>备注

此标志在 Windows Server 2003 和更高版本的 Windows 中被永久设置。 在这些系统中，"全局标志" 对话框中的 " **启用池标记** " 复选框将灰显，启用或禁用池标记的命令将失败。

使用 **ExAllocatePoolWithTag** 或 **ExAllocatePoolWithQuotaTag** 设置标记值。 如果未指定任何标记值 (**ExAllocatePool**， **ExAllocatePoolWithQuota**) ，Windows 将创建默认值为 "None" 的标记。 由于将所有具有 "无" 标记的分配的数据组合在一起，因此不能将数据与特定分配区分开来。 有关这些例程的信息，请参阅 Windows 驱动程序工具包 (WDK) 。

>[!IMPORTANT]
> 本主题中讨论的 ExAllocatePool DDIs 已在 Windows 10 版本2004中弃用，并且已被 [ExAllocatePool2](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool2) 和 [ExAllocatePool3](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool3)替换。 有关详细信息，请参阅 [将弃用的 ExAllocatePool 调用更新到 ExAllocatePool2 和 ExAllocatePool3](../kernel/updating-deprecated-exallocatepool-calls.md)。

**注意**   若要显示 Windows 为标记分配收集的数据，请使用 PoolMon，它是 Windows 驱动程序工具包中包含的工具。


 

 

