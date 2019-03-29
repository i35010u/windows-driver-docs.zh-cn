---
title: 在注册表中设置硬件信息
description: 在注册表中设置硬件信息
ms.assetid: 82f5d399-58c3-4bed-a3f2-3501f21fa3e8
keywords:
- 硬件 WDK 微型端口
- 注册表 WDK 微型端口
- VideoPortSetRegistryParameters
- VideoPortGetRegistryParameters
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb9433dc4aec4fe869b674e1531b4094827f63f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562297"
---
# <a name="setting-hardware-information-in-the-registry"></a>在注册表中设置硬件信息


## <span id="ddk_setting_hardware_information_in_the_registry_gg"></span><span id="DDK_SETTING_HARDWARE_INFORMATION_IN_THE_REGISTRY_GG"></span>


[*HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)可以调用[ **VideoPortGetRegistryParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff570316)并[ **VideoPortSetRegistryParameters**](https://msdn.microsoft.com/library/windows/hardware/ff570365)函数来获取和设置在注册表中的配置信息。 例如， *HwVidFindAdapter*可能会在调用**VideoPortSetRegistryParameters**注册表中的下一次启动设置非易失性的配置信息。 它可能会调用**VideoPortGetRegistryParameters**若要获取特定于适配器的、 总线相对配置参数由安装程序写入到注册表。

建议微型端口驱动程序来显示有用的信息，向用户和帮助调试在注册表中设置特定硬件的信息。 芯片类型、 DAC 类型、 内存大小 （的适配器） 和一个字符串来标识该适配器，可以设置微型端口驱动程序。 通过控制面板中显示程序会显示此信息。

该驱动程序通过调用来设置此信息**VideoPortSetRegistryParameters**。 通常情况下，驱动程序，可以在调用其*HwVidFindAdapter*例程。

下表描述的信息，该驱动程序可以注册并提供详细信息*ValueName*并*ValueData*参数的**VideoPortSetRegistryParameters**:

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">条目的信息</th>
<th align="left"><em>ValueName</em></th>
<th align="left"><em>ValueData</em></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>芯片类型</p></td>
<td align="left"><p>HardwareInformation.ChipType</p></td>
<td align="left"><p>包含的芯片名称 null 结尾的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DAC 类型</p></td>
<td align="left"><p>HardwareInformation.DacType</p></td>
<td align="left"><p>Null 结尾的字符串包含 DAC 名称或 id。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>内存大小</p></td>
<td align="left"><p>HardwareInformation.MemorySize</p></td>
<td align="left"><p>Ulong 值，以 mb 为单位，包含在适配器上的视频内存量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>适配器 ID</p></td>
<td align="left"><p>HardwareInformation.AdapterString</p></td>
<td align="left"><p>包含适配器的名称的以 null 结尾的字符串。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BIOS</p></td>
<td align="left"><p>HardwareInformation.BiosString</p></td>
<td align="left"><p>包含有关 BIOS 的信息的以 null 结尾的字符串。</p></td>
</tr>
</tbody>
</table>

 

 

 





