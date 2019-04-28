---
title: 已过时内核模式驱动程序支持函数
description: 已过时内核模式驱动程序支持函数
ms.assetid: 8bdfbd2e-a0d6-424f-9092-297e533efa33
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba0d1b2c9edd652f6ffe760c979c88caa5045216
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332288"
---
# <a name="obsolete-kernel-mode-driver-support-functions"></a>已过时内核模式驱动程序支持函数


## <span id="ddk_obsolete_kernel_mode_driver_support_functions_ks"></span><span id="DDK_OBSOLETE_KERNEL_MODE_DRIVER_SUPPORT_FUNCTIONS_KS"></span>


标头文件 portcls.hdefines 四个宏包含过时的内核模式驱动程序支持函数的名称。 这些宏允许包含对要重新编译以使用新的内核函数，而无需对源代码文件的任何编辑的已过时的函数名称的引用的旧源代码。

当编译使用过时的名称的源代码，定义的参数名称 PC\_旧\_名称。 此参数可以由编译器命令行参数"-DPC\_旧\_名称"这是比简介语句更方便`#define PC_OLD_NAMES`到源文件本身。

下表列出了左侧列中的已过时的内核模式驱动程序支持函数名称。 对于每个已过时的名称，右侧的列包含替换为新内核函数的名称。 每种情况下，在宏的定义相当于一个简单名称更改。 为已过时的函数的参数列表和新的函数是相同的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">已过时的函数名称</th>
<th align="left">新的函数名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WIN95COMPAT_ReadPortUChar</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560797" data-raw-source="[&lt;strong&gt;READ_PORT_UCHAR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560797)"><strong>READ_PORT_UCHAR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WIN95COMPAT_WritePortUChar</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566386" data-raw-source="[&lt;strong&gt;WRITE_PORT_UCHAR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566386)"><strong>WRITE_PORT_UCHAR</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WIN95COMPAT_ReadPortUShort</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560806" data-raw-source="[&lt;strong&gt;READ_PORT_USHORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560806)"><strong>READ_PORT_USHORT</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WIN95COMPAT_WritePortUShort</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566388" data-raw-source="[&lt;strong&gt;WRITE_PORT_USHORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566388)"><strong>WRITE_PORT_USHORT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 





