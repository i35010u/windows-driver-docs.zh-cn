---
title: 从 WDM 音频驱动程序的扩展的功能
description: 从 WDM 音频驱动程序的扩展的功能
ms.assetid: 8ee081ee-623d-4eaf-953f-20ccfbbe9800
keywords:
- 有关旧版支持扩展的 WDM 音频扩展 WDK，
- WDM 音频扩展 WDK，设备 Id
- 设备 Id WDK 音频
- 唯一的设备 Id WDK 音频
- 识别的音频设备
- 特定于硬件的信息 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ed4463d9772a3f738c25d51753057fc19458235
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525827"
---
# <a name="extended-capabilities-from-a-wdm-audio-driver"></a>从 WDM 音频驱动程序的扩展的功能


## <span id="extended_capabilities_from_a_wdm_audio_driver"></span><span id="EXTENDED_CAPABILITIES_FROM_A_WDM_AUDIO_DRIVER"></span>


通过处理[ **KSPROPERTY\_常规\_COMPONENTID** ](https://msdn.microsoft.com/library/windows/hardware/ff565171)属性，音频筛选器可以提供应用程序可以使用到唯一的特定于硬件的信息确定基础设备。 Microsoft Windows XP 是第一个版本的 Windows，若要支持此功能;此功能不是早期版本中提供的。

筛选器提供的窗体中的特定于硬件的信息[ **KSCOMPONENTID** ](https://msdn.microsoft.com/library/windows/hardware/ff561027)包含以下结构：

-   制造商 GUID

-   产品 GUID

-   组件 GUID

-   名称 GUID

-   硬件版本数

-   硬件修订号

若要提供访问此信息，WDM 音频驱动程序属性处理程序为指定 KSPROPERTY\_常规\_筛选器自动化表中的 COMPONENTID。

应用程序可以通过以下的旧 Windows 多媒体 Api 的驱动程序的 KSCOMPONENTID 结构从访问数据： **aux**， **midiIn**， **midiOut**， **mixer**， **waveIn**，并**waveOut**。 客户端通过下表中调用的多媒体功能之一和扩展功能结构作为第二个参数中传递查询此信息的驱动程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">多媒体函数</th>
<th align="left">扩展功能结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>auxGetDevCaps</strong></p></td>
<td align="left"><p>AUXCAPS2</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>midiInGetDevCaps</strong></p></td>
<td align="left"><p>MIDIINCAPS2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>midiOutGetDevCaps</strong></p></td>
<td align="left"><p>MINIOUTCAPS2</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>mixerGetDevCaps</strong></p></td>
<td align="left"><p>MIXERCAPS2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>waveInGetDevCaps</strong></p></td>
<td align="left"><p>WAVEINCAPS2</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>waveOutGetDevCaps</strong></p></td>
<td align="left"><p>WAVEOUTCAPS2</p></td>
</tr>
</tbody>
</table>

 

从筛选器的属性处理程序收到 KSCOMPONENTID 结构之后, WDMAud 系统驱动程序 (Wdmaud.sys) 将数据从转换到此结构*XXX*CAPS2 格式化*xxx*GetDevCaps 函数使用。

验证功能结构传递给该函数是否足以包含制造商、 产品和名称 Guid 后*xxx*GetDevCaps 函数将此信息复制到之前的扩展结构返回。 （不使用当前的组件中 KSCOMPONENTID GUID。）

WDMAud 串联**版本**并**修订**成员从 KSCOMPONENTID 以形成的 16 位修订号*xxx*GetDevCaps 函数复制到**vDriverVersion**功能结构中的成员：

**vDriverVersion** = (**版本** &lt; &lt; 8) |(**修订**和 0xFF)

Microsoft 以前需要供应商注册制造商 Id 和为其音频设备的产品 Id。 标头文件 Mmreg.h 然后发布这些 Id。

在 Windows XP 及更高版本，注册 Id 不再是必需的;通过 KSPROPERTY 提供的制造商和产品 Guid 会替换这些\_常规\_COMPONENTID 属性。 Guid 的供应商可以使用不是已注册的 Id 的 Guid 是本质上是唯一的因为轻松生成和需要注册任何更方便。

但是，如果具有已注册到 Microsoft 的产品和制造商 Id （并且位于 Mmreg.h），则可以使用宏 INIT\_MMREG\_PID 和 INIT\_MMREG\_中要转换的 Ksmedia.h MID 你到 Guid 的产品和制造商 Id。 如果您使用这些宏生成 Guid，是能够从 Guid 中恢复原始的产品和制造商 Id 并复制到这些 Id WDMAud **wPid**并**wMid**成员的功能结构，它由填写*xxx*GetDevCaps 调用。

否则，如果没有已注册的制造商和产品 Id，只需使用 GuidGen 实用程序来生成制造商和产品 Guid。 （GuidGen 包含在 Microsoft Windows SDK 中）。此类型的驱动程序的 Guid 时，WDMAud 加载默认常量 MM\_未映射和 MM\_PID\_未映射到**wMid**并**wPid**成员，通过填写的功能结构的分别*xxx*GetDevCaps 调用。

使用 WDMAud**名称**KSCOMPONENTID 结构中的 GUID 查找注册表中的"Name"键。 此密钥下的注册表路径名称 HKLM\\系统\\CurrentControlSet\\控制\\MediaCategories。 设备的"Name"键具有关联的字符串值，该值包含设备名称。 *Xxx*GetDevCaps 函数将复制到此名称字符串的前 31 个字符**szPname**功能结构中的成员。 针对设备名称长度超过 31 个字符，客户端应用程序可以打开注册表项和直接读取整个字符串。 驱动程序可以填充两种方式之一在此注册表项：

-   该驱动程序可以指定在设备的 INF 文件中的条目安装时间。

-   该驱动程序可以执行其筛选器初始化例程期间加载项。

GUID 的名称是可选的。 如果驱动程序设置**名称**成员中与 GUID KSCOMPONENTID\_NULL 值，WDMAud 提供设备的友好名称*xxx*GetDevCaps 函数，将复制到此名称**szPname**功能结构中的成员。

如果筛选器不公开任何处理程序用于 KSPROPERTY\_常规\_COMPONENTID 属性，WDMAud 使用代替 KSCOMPONENTID 结构中的数据的默认值。 旧功能结构一部分的默认值如下所示：

-   **wMid** = MM\_MICROSOFT

-   **wPid** = 设备类从以下列表：MM\_MSFT\_WDMAUDIO\_WAVEOUT MM\_MSFT\_WDMAUDIO\_WAVEIN MM\_MSFT\_WDMAUDIO\_MIDIOUT MM\_MSFT\_WDMAUDIO\_MIDIIN MM\_MSFT\_WDMAUDIO\_MIXER MM\_MSFT\_WDMAUDIO\_AUX
-   **vDriverVersion** = 0x050a （适用于 Windows XP) 或 0x0500 的值 (早于 Windows XP)

Windows 版本早于 Windows XP 的旧功能结构的成员始终设置为更高版本的默认值。 Windows XP 及更高版本，扩展功能的默认值如下所示：

-   **NameGuid** = GUID\_NULL

-   INIT\_MMREG\_MID(&**ManufacturerGuid**, **wMid**)

-   INIT\_MMREG\_PID(&**ProductGuid**, **wPid**)

INIT\_MMREG\_MID 和 INIT\_MMREG\_Ksmedia.h 中定义更高版本的 PID 宏。 这些宏用于在转换中的制造商和产品 Id **wMid**并**wPid**成员加载到 Guid **ManufacturerGuid**和**ProductGuid**成员。

 

 




