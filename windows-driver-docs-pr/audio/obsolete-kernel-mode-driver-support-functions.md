---
title: 已过时内核模式驱动程序支持函数
description: 已过时内核模式驱动程序支持函数
ms.assetid: 8bdfbd2e-a0d6-424f-9092-297e533efa33
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97f89fd24058655615576ee98b7bca90844c341c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102302"
---
# <a name="obsolete-kernel-mode-driver-support-functions"></a>已过时内核模式驱动程序支持函数


## <span id="ddk_obsolete_kernel_mode_driver_support_functions_ks"></span><span id="DDK_OBSOLETE_KERNEL_MODE_DRIVER_SUPPORT_FUNCTIONS_KS"></span>


标头文件 portcls hdefines 四个宏，其中包含过时的内核模式驱动程序支持函数的名称。 这些宏允许将包含对过时函数名称引用的旧源代码重新编译为使用新的内核函数，而无需对源文件进行任何编辑。

在编译使用过时名称的源代码时，定义参数名称 "PC \_ 旧 \_ 名称"。 此参数可由编译器命令行参数 "-DPC \_ OLD \_ 名称" 定义，前提是比将语句引入 `#define PC_OLD_NAMES` 源文件本身更方便。

下表列出了左栏中过时的内核模式驱动程序支持函数名称。 对于每个过时名称，右侧列包含替代它的新内核函数的名称。 在每种情况下，宏定义为简单名称更改。 过时函数和新函数的参数列表是相同的。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">过时的函数名称</th>
<th align="left">新函数名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>WIN95COMPAT_ReadPortUChar</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-read_port_uchar" data-raw-source="[&lt;strong&gt;READ_PORT_UCHAR&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-read_port_uchar)"><strong>READ_PORT_UCHAR</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WIN95COMPAT_WritePortUChar</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-write_port_uchar" data-raw-source="[&lt;strong&gt;WRITE_PORT_UCHAR&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-write_port_uchar)"><strong>WRITE_PORT_UCHAR</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>WIN95COMPAT_ReadPortUShort</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-read_port_ushort" data-raw-source="[&lt;strong&gt;READ_PORT_USHORT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-read_port_ushort)"><strong>READ_PORT_USHORT</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>WIN95COMPAT_WritePortUShort</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-write_port_ushort" data-raw-source="[&lt;strong&gt;WRITE_PORT_USHORT&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-write_port_ushort)"><strong>WRITE_PORT_USHORT</strong></a></p></td>
</tr>
</tbody>
</table>

 

