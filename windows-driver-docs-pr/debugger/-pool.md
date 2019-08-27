---
title: 池扩展命令
description: 池扩展显示有关特定池分配或整个系统范围池的信息。
ms.assetid: 1c224e0c-d50c-487e-8238-9be054368ac2
keywords:
- 池子
- pooltag 文件
- 池标记
- 内存, 池标记
- 池 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2fff8b18eb0c0f6a2706471eedcd3bc422d36bab
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025194"
---
# <a name="pool"></a>!pool


**! Pool**扩展显示有关特定池分配或整个系统范围池的信息。

```dbgcmd
!pool [Address [Flags]]
```

## <a name="span-idddk__pool_dbgspanspan-idddk__pool_dbgspanparameters"></a><span id="ddk__pool_dbg"></span><span id="DDK__POOL_DBG"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示的池条目。 如果*Address*为-1, 则此命令将显示有关进程中的所有堆的信息。

如果*Address*为0或省略, 则此命令将显示有关进程堆的信息。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要使用的详细信息的级别。 这可以是以下位值的任意组合;默认值为零:

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
使显示内容包括池内容, 而不仅仅是池标头。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
使显示抑制所有池的池标头信息, 但实际包含指定*地址*的池除外。

<span id="Bit_31__0x80000000_"></span><span id="bit_31__0x80000000_"></span><span id="BIT_31__0X80000000_"></span>位 31 (0x80000000)  
取消显示中池类型和池标记的说明。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内存池的信息, 请参阅 Windows 驱动程序工具包 (WDK) 文档和*Microsoft Windows 内部机制*, 标记 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

在 Windows XP 和更高版本的 Windows 中, **! 池**扩展显示与每个分配关联的池标记。 还会显示该池标记的所有者。 此显示基于 pooltag 文件的内容。 此文件位于适用于 Windows 的调试工具安装的 "会审" 子目录中。 如果需要, 可以编辑此文件以添加与项目相关的其他池标记。

**警告如果您**在与当前版本相同的目录中安装了 Windows 调试工具的更新版本, 则会覆盖该目录中的所有文件, 包括 pooltag。   如果修改或替换示例 pooltag 文件, 请务必将其副本保存到其他目录。 重新安装调试器后, 可以将保存的 pooltag 复制到默认版本。

 

如果 **! 池**扩展报告池损坏, 应使用[ **! poolval**](-poolval.md)进行调查。

下面是一个示例。 如果*Address*指定 0xE1001050, 则会显示此块中所有池的标头, 并且0xE1001050 本身标记为带有星号 (\*)。

```dbgcmd
kd> !pool e1001050 
 e1001000 size:   40 previous size:    0  (Allocated)  MmDT
 e1001040 size:   10 previous size:   40  (Free)       Mm  
*e1001050 size:   10 previous size:   10  (Allocated) *ObDi
 e1001060 size:   10 previous size:   10  (Allocated)  ObDi
 e1001070 size:   10 previous size:   10  (Allocated)  Symt
 e1001080 size:   40 previous size:   10  (Allocated)  ObDm
 e10010c0 size:   10 previous size:   40  (Allocated)  ObDi
.....
```

在此示例中, 最右侧的列显示了池标记。 此左侧的列显示池是否可用或已分配。

以下命令显示池标头和池内容:

```dbgcmd
kd> !pool e1001050 1
 e1001000 size:   40 previous size:    0  (Allocated)  MmDT
 e1001008  ffffffff 0057005c 004e0049 004f0044
    e1001018  ffffffff 0053005c 00730079 00650074

 e1001040 size:   10 previous size:   40  (Free)       Mm  
 e1001048  ffffffff e1007ba8 e1501a58 01028101
    e1001058  ffffffff 00000000 e1000240 01028101

*e1001050 size:   10 previous size:   10  (Allocated) *ObDi
 e1001058  ffffffff 00000000 e1000240 01028101
    e1001068  ffffffff 00000000 e10009c0 01028101

 e1001060 size:   10 previous size:   10  (Allocated)  ObDi
 e1001068  ffffffff 00000000 e10009c0 01028101
    e1001078  ffffffff 00000000 00000000 04028101

......
```

 

 





