---
title: 池扩展命令
description: 池扩展显示有关特定池分配或整个系统范围内池的信息。
ms.assetid: 1c224e0c-d50c-487e-8238-9be054368ac2
keywords:
- 池
- pooltag.txt 文件
- 池标记
- 内存池标记
- 调试 Windows 池
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3cf251bdbfcc78380be579d49c36c0732164db8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334374"
---
# <a name="pool"></a>!pool


**！ 池**扩展显示有关特定池分配或整个系统范围内池的信息。

```dbgcmd
!pool [Address [Flags]]
```

## <a name="span-idddkpooldbgspanspan-idddkpooldbgspanparameters"></a><span id="ddk__pool_dbg"></span><span id="DDK__POOL_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示的池项。 如果*地址*为-1，此命令显示有关进程中的所有堆的信息。

如果*地址*为 0 或省略，此命令显示有关进程堆的信息。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定要使用的详细信息级别。 这可以是下列位值; 中的任意组合默认值为零：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
将导致显示以包括池内容，而不仅仅是池标头。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
禁止显示所有的池，除实际包含指定的池标头信息的显示将导致*地址*。

<span id="Bit_31__0x80000000_"></span><span id="bit_31__0x80000000_"></span><span id="BIT_31__0X80000000_"></span>第 31 (0x80000000) 位  
禁止显示池类型和池标记中显示的说明。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关内存池的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

在 Windows XP 和更高版本的 Windows， **！ 池**扩展插件都会显示与每个分配关联的池标记。 此外会显示该池标记的所有者。 此显示基于 pooltag.txt 文件的内容。 此文件位于您的 Windows 调试工具的安装的会审子目录中。 如果你想，您可以编辑此文件以添加到你的项目相关的其他池标记。

**警告**  如果为当前版本的相同目录中安装的 Windows 调试工具的更新的版本，它将覆盖所有在该目录中包括 pooltag.txt 文件。 如果修改或替换示例 pooltag.txt 文件，请务必将它的一个副本保存到不同的目录。 重新安装调试器之后, 可将已保存的 pooltag.txt 复制的默认版本。

 

如果 **！ 池**扩展插件将报表集损坏，则应使用[ **！ poolval** ](-poolval.md)进行调查。

下面是一个示例。 如果*地址*指定 0xE1001050，会显示此块中的所有池的标头，和 0xE1001050 本身标有星号 (\*)。

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

在此示例中，最右侧的列显示了池标记。 左侧的此列显示该池是免费还是已分配。

以下命令显示池标头和池内容：

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

 

 





