---
title: DirectSound 硬件加速和 SRC 滑块
description: DirectSound 硬件加速和 SRC 滑块
ms.assetid: 40329177-b8d5-49a2-a1d3-6730a26b6e78
keywords:
- 硬件加速 WDK DirectSound，SRC 滑块
- 滑块 WDK 音频
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d0f62d71aaf7519a9266c260184e027fd3f99fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333847"
---
# <a name="directsound-hardware-acceleration-and-src-sliders"></a>DirectSound 硬件加速和 SRC 滑块


## <span id="directsound_hardware_acceleration_and_src_sliders"></span><span id="DIRECTSOUND_HARDWARE_ACCELERATION_AND_SRC_SLIDERS"></span>


Windows 提供全局滑块控件更改 DirectSound 在系统范围内的性能。 滑块控件硬件加速和供 DirectSound 应用程序的采样率转换 （源） 的质量的级别。 在启动 ups，硬件加速和 SRC 滑块所做的更改是永久性的。

硬件加速和 SRC 设置可以更改只能由直接的最终用户操作。 可以从应用程序更改的硬件加速或 SRC 设置任何 API 不。 此行为提高了稳定性并阻止软件音频系统放在从中它不能删除不重启的状态。

这些设置会影响仅 DirectSound 应用程序。 请注意 waveOut API 始终使用最佳的 SRC 质量，而不考虑 DirectSound SRC 滑块的设置。 此外，在所有当前版本的 Windows，waveOut 应用程序无法在音频设备上使用硬件加速的 pin 和不受 DirectSound 硬件加速滑块的设置。 有关 Windows 多媒体 waveOut API 的详细信息，请参阅 Microsoft Windows SDK 文档。

若要在 Windows 中找到的 DirectSound 硬件加速和 SRC 滑块，例如，请执行以下步骤：

1.  在控制面板中，双击**声音和音频设备**图标 （或只需运行的 mmsys.cpl）。

2.  上**音频**选项卡上，选择从一个设备**声音播放**列表。

3.  单击“高级”按钮。

4.  单击**性能**选项卡。

此时，应看到两个标记的滑块**硬件加速**并**采样率转换质量**。

硬件加速滑块有四个设置的重量**无**（级别 0） 到左侧**完整**（三个级别） 在右侧。 下表显示了这些设置的含义。

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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>仿真</p></td>
<td align="left"><p>强制仿真。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>基本</p></td>
<td align="left"><p>禁用硬件加速的 DirectSound 辅助缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>标准</p></td>
<td align="left"><p>启用硬件加速的 DirectSound 辅助缓冲区，但禁用特定于供应商的属性集扩展。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>完全</p></td>
<td align="left"><p>启用 DirectSound 辅助缓冲区的硬件加速，并启用特定于供应商的属性集扩展。</p></td>
</tr>
</tbody>
</table>

 

<span id="Emulation_Setting"></span><span id="emulation_setting"></span><span id="EMULATION_SETTING"></span>**模拟设置**  
**仿真**上面的设置强制 DirectSound 到仿真模式。 在此模式下，DirectSound 应用程序运行就好像没有 DirectSound 驱动程序存在。 所有混合使用通过在用户模式下，DirectSound 和生成的音频数据播放通过 waveOut API。 结果通常是大幅增加的延迟。 

<span id="Basic_Setting"></span><span id="basic_setting"></span><span id="BASIC_SETTING"></span>**基本设置**  
**基本**设置将禁用 DirectSound 辅助缓冲区的硬件加速。 在此设置下 DirectSound 的所有应用程序运行像未采用硬件加速不可用，而不考虑声卡正在使用的功能。 在测试期间此设置可用于模拟具有未 DirectSound 加速的声卡。 此设置与 OPL，有没有加速 DirectSound 辅助缓冲区，例如适配器具有相同的效果**标准**设置。 在 Windows Server 2003**基本**是默认设置。

<span id="Standard_Setting"></span><span id="standard_setting"></span><span id="STANDARD_SETTING"></span>**标准设置**  
**标准**设置启用硬件加速的 DirectSound 辅助缓冲区，但禁用作为属性公开的特定于供应商扩展如 EAX （Creative 技术环境的音频扩展）通过设置**IKsPropertySet**接口 (请参阅[公开自定义音频属性设置](exposing-custom-audio-property-sets.md))。 在 Windows 2000 中，**标准**设置默认处于选中状态。

<span id="Full_Setting"></span><span id="full_setting"></span><span id="FULL_SETTING"></span>**完整设置**  
**完整**设置启用 DirectSound 辅助缓冲区的全部加速。 此设置还允许通过公开的特定于供应商扩展的属性集**IKsPropertySet**接口 (请参阅[公开自定义音频属性设置](exposing-custom-audio-property-sets.md))。 **IKsPropertySet**扩展包括特定于供应商的硬件增强功能，如 EAX。 


如果用户调整硬件加速或 SRC 设置为默认值以外的值，DirectSound 而不是默认使用新的设置。



 

 




