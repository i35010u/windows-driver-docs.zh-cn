---
title: DirectSound 硬件加速和 SRC 滑块
description: DirectSound 硬件加速和 SRC 滑块
keywords:
- 硬件加速 WDK DirectSound，源滑块
- 滑杆音频
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: e565ecf235e6fc7baf448550ac82df82ce67f99e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789273"
---
# <a name="directsound-hardware-acceleration-and-src-sliders"></a>DirectSound 硬件加速和 SRC 滑块


## <span id="directsound_hardware_acceleration_and_src_sliders"></span><span id="DIRECTSOUND_HARDWARE_ACCELERATION_AND_SRC_SLIDERS"></span>


Windows 提供了全局滑块控件，用于在整个系统范围内更改 DirectSound 性能。 滑块控制 DirectSound 应用程序可使用的源) 的硬件加速和质量 (。 对硬件加速和 SRC 滑杆所做的更改在启动时保持不变。

只能通过直接最终用户操作来更改硬件加速和 SRC 设置。 没有可用于从应用程序更改硬件加速或 SRC 设置的 API。 此行为可提高稳定性，并防止软件将音频系统置于无法删除的状态，而无需重新启动。

这些设置仅影响 DirectSound 的应用程序。 请注意，无论 DirectSound SRC 滑块的设置如何，waveOut API 始终使用最佳的 SRC 质量。 此外，在所有当前版本的 Windows 中，waveOut 应用程序无法在音频设备上使用硬件加速的 pin，并且不受 DirectSound 硬件加速滑块的设置影响。 有关 Windows 多媒体 waveOut API 的详细信息，请参阅 Microsoft Windows SDK 文档。

例如，若要在 Windows 中查找 DirectSound 硬件加速和 SRC 滑杆，请遵循以下步骤：

1.  在 "控制面板" 中，双击 " **声音和音频设备** " 图标 (或只需 mmsys.cpl) 运行。

2.  在 " **音频** " 选项卡上，从 " **声音播放** " 列表中选择一个设备。

3.  选择“高级”按钮。

4.  选择“性能”选项卡。

此时，应会看到两个标记为 **硬件加速** 和 **采样速率转换质量** 的滑块。

"硬件加速" 滑块有四个设置，范围是从 " **无** " (级别 0) 左侧到 " **完整** (第三级) "。 下表显示了这些设置的含义。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">加速级别</th>
<th align="left">设置名称</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>仿真</p></td>
<td align="left"><p>强制执行模拟。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>基本</p></td>
<td align="left"><p>禁用 DirectSound 辅助缓冲区的硬件加速。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>Standard</p></td>
<td align="left"><p>启用 DirectSound 辅助缓冲区的硬件加速，但禁用特定于供应商的属性集扩展。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>完整</p></td>
<td align="left"><p>启用 DirectSound 辅助缓冲区的硬件加速，并启用特定于供应商的属性集扩展。</p></td>
</tr>
</tbody>
</table>

 

<span id="Emulation_Setting"></span><span id="emulation_setting"></span><span id="EMULATION_SETTING"></span>**模拟设置**  
上述 **模拟** 设置会强制 DirectSound 进入模拟模式。 在此模式下，DirectSound 应用程序的运行方式为，但不存在 DirectSound 驱动程序。 所有混合都是在用户模式下通过 DirectSound 来完成的，并且生成的音频数据会通过 waveOut API 播放回来。 结果通常会大幅增加延迟。 

<span id="Basic_Setting"></span><span id="basic_setting"></span><span id="BASIC_SETTING"></span>**基本设置**  
" **基本** " 设置禁用 DirectSound 辅助缓冲区的硬件加速。 在此设置下，无论使用哪种声卡功能，所有 DirectSound 应用程序都将运行，但没有硬件加速可用。 在测试过程中，可以使用此设置来模拟无 DirectSound 加速功能的声卡。 对于适配器（如 OPL），如果没有加速 DirectSound 辅助缓冲区，此设置的效果与 **标准** 设置相同。 在 Windows Server 2003 中， **Basic** 是默认设置。

<span id="Standard_Setting"></span><span id="standard_setting"></span><span id="STANDARD_SETTING"></span>**标准设置**  
**标准** 设置启用 DirectSound 辅助缓冲区的硬件加速，但会禁用特定于供应商的扩展，如 EAX (创造性技术的环境音频扩展) ，这些扩展通过 **IKsPropertySet** 接口公开为属性集 (请参阅 [公开自定义音频属性集](exposing-custom-audio-property-sets.md)) 。 在 Windows 2000 中，默认情况下将选择 " **标准** " 设置。

<span id="Full_Setting"></span><span id="full_setting"></span><span id="FULL_SETTING"></span>**完全设置**  
**Full** 设置启用 DirectSound 辅助缓冲区的完全加速。 此设置还为通过 **IKsPropertySet** 接口公开的供应商特定的扩展启用了属性集 (请参阅 [公开自定义音频属性集](exposing-custom-audio-property-sets.md)) 。 **IKsPropertySet** 扩展包括特定于供应商的硬件增强功能，如 EAX。 


如果用户将硬件加速或 SRC 设置调整为默认值以外的值，则 DirectSound 将使用新设置而不是默认值。



 

 




