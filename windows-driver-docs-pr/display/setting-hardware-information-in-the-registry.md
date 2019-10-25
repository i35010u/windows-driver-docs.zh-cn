---
title: 在注册表中设置硬件信息
description: 在注册表中设置硬件信息
ms.assetid: 82f5d399-58c3-4bed-a3f2-3501f21fa3e8
keywords:
- 硬件 WDK 视频微型端口
- 注册表 WDK 视频微型端口
- VideoPortSetRegistryParameters
- VideoPortGetRegistryParameters
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e584229255493126e6e6489493dd838a6fab246a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829502"
---
# <a name="setting-hardware-information-in-the-registry"></a>在注册表中设置硬件信息


## <span id="ddk_setting_hardware_information_in_the_registry_gg"></span><span id="DDK_SETTING_HARDWARE_INFORMATION_IN_THE_REGISTRY_GG"></span>


[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)可以调用[**VideoPortGetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetregistryparameters)和[**VideoPortSetRegistryParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportsetregistryparameters)函数来获取和设置注册表中的配置信息。 例如， *HwVidFindAdapter*可能会调用**VideoPortSetRegistryParameters** ，为下一次启动设置注册表中的非易失性配置信息。 它可以调用**VideoPortGetRegistryParameters**来获取由安装程序写入到注册表中的特定于适配器的总线相关配置参数。

建议微型端口驱动程序将注册表中的某些硬件信息设置为向用户显示有用信息，并帮助进行调试。 微型端口驱动程序可以设置芯片类型、DAC 类型、内存大小（对于适配器）和标识适配器的字符串。 此信息由控制面板中的 "显示" 程序显示。

驱动程序通过调用**VideoPortSetRegistryParameters**来设置此信息。 通常，驱动程序会在其*HwVidFindAdapter*例程中进行调用。

下表描述了驱动程序可以注册的信息，并提供了**VideoPortSetRegistryParameters**的*ValueName*和*ValueData*参数的详细信息：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">输入信息</th>
<th align="left"><em>ValueName</em></th>
<th align="left"><em>ValueData</em></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>芯片类型</p></td>
<td align="left"><p>HardwareInformation.ChipType</p></td>
<td align="left"><p>包含芯片名称的以 Null 结尾的字符串。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DAC 类型</p></td>
<td align="left"><p>HardwareInformation. DacType</p></td>
<td align="left"><p>以 Null 结尾的字符串，其中包含 DAC 名称或 ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>内存大小</p></td>
<td align="left"><p>HardwareInformation. MemorySize</p></td>
<td align="left"><p>ULONG，其中包含适配器上的视频内存量（以 MB 为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>适配器 ID</p></td>
<td align="left"><p>HardwareInformation.AdapterString</p></td>
<td align="left"><p>以 Null 结尾的字符串，其中包含适配器的名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BIOS</p></td>
<td align="left"><p>HardwareInformation.BiosString</p></td>
<td align="left"><p>以 Null 结尾的字符串，其中包含有关 BIOS 的信息。</p></td>
</tr>
</tbody>
</table>

 

 

 





