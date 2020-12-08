---
title: 从 WDM 音频驱动程序扩展的功能
description: 从 WDM 音频驱动程序扩展的功能
keywords:
- WDM 音频扩展 WDK，关于旧版支持扩展
- WDM 音频扩展 WDK，设备 Id
- 设备 Id WDK 音频
- 唯一设备 Id WDK 音频
- 识别音频设备
- 特定于硬件的信息 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17feb60cade7fc0a8fe7a2047f84f5f66070295f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784807"
---
# <a name="extended-capabilities-from-a-wdm-audio-driver"></a>从 WDM 音频驱动程序扩展的功能


## <span id="extended_capabilities_from_a_wdm_audio_driver"></span><span id="EXTENDED_CAPABILITIES_FROM_A_WDM_AUDIO_DRIVER"></span>


通过处理 [**KSPROPERTY \_ GENERAL \_ 组件**](../stream/ksproperty-general-componentid.md) 属性，音频过滤器可以提供特定于硬件的信息，应用程序可以使用这些信息来唯一标识基础设备。 Microsoft Windows XP 是支持此功能的第一个 Windows 版本;此功能在早期版本中不可用。

此筛选器以 [**KSCOMPONENTID**](/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid) 结构的形式提供特定于硬件的信息，其中包含以下内容：

-   制造商 GUID

-   产品 GUID

-   组件 GUID

-   名称 GUID

-   硬件版本号

-   硬件修订号

为提供对此信息的访问，WDM 音频驱动程序 \_ \_ 在筛选器自动化表中为 KSPROPERTY 常规组件 id 指定属性处理程序。

应用程序可以通过以下旧版 Windows 多媒体 Api 从驱动程序的 KSCOMPONENTID 结构访问数据： **aux**、 **midiIn**、 **midiOut**、 **混合器**、 **waveIn** 和 **waveOut**。 客户端通过调用下表中的一个多媒体函数并传入扩展功能结构作为第二个参数，来查询驱动程序以获取此信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">多媒体函数</th>
<th align="left">Extended-Capabilities 结构</th>
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

 

接收到来自筛选器的属性处理程序的 KSCOMPONENTID 结构后，WDMAud 系统驱动程序 ( # A0) 将此结构中的数据转换为 *xxx* GetDevCaps 函数使用的 *xxx* CAPS2 格式。

在验证传递给函数的功能结构是否足以包含制造商、产品和名称 Guid 后， *xxx* GetDevCaps 函数会将此信息复制到扩展结构中，然后再返回。  (当前未使用 KSCOMPONENTID 中的组件 GUID。 ) 

WDMAud 将 **版本** 和 **修订** 成员从 KSCOMPONENTID 连接起来，以形成 *xxx* GetDevCaps 函数复制到功能结构 **vDriverVersion** 成员的16位版本号：

**vDriverVersion** = (**版本** &lt; &lt; 8) | (**修订**& 0xff) 

Microsoft 以前要求供应商为其音频设备注册制造商 Id 和产品 Id。 然后在头文件 Mmreg 中释放这些 Id。

在 Windows XP 和更高版本中，不再需要已注册的 Id;它们由通过 KSPROPERTY 常规组件程序属性提供的制造商和产品 Guid 替换 \_ \_ 。 与已注册的 Id 相比，Guid 更为方便，因为 Guid 本质上是唯一的，很容易生成，并且无需注册。

但是，如果你已经向 Microsoft (注册了产品和制造商 Id 并且它们位于 Mmreg) 中，则可以使用 \_ Mmreg \_ PID 和 INIT \_ Mmreg \_ MID 将你的产品和制造商 id 转换为 guid。 如果使用这些宏生成 Guid，则 WDMAud 可以从 Guid 恢复原始产品和制造商 Id，并将这些 Id 复制到由 *xxx* GetDevCaps 调用填充的功能结构的 **wPid** 和 **wMid** 成员中。

否则，如果没有已注册的制造商和产品 Id，只需使用 Guidgen.exe 实用程序来生成制造商和产品 Guid 即可。  (Guidgen.exe 包含在 Microsoft Windows SDK 中。 ) 当驱动程序的 Guid 为此类型时，WDMAud 将默认的常量 MM \_ 映射和 MM \_ PID \_ 映射分别加载到由 *xxx* GetDevCaps 调用填充的功能结构的 **wMid** 和 **wPid** 成员中。

WDMAud 使用 KSCOMPONENTID 结构中的 **名称** GUID 在注册表中查找 "名称" 密钥。 此密钥位于注册表路径名称 HKLM \\ 系统 \\ CurrentControlSet \\ Control \\ MediaCategories 下。 设备的 "名称" 键包含一个关联的字符串值，该字符串值包含设备名称。 *Xxx* GetDevCaps 函数将此名称字符串的前31个字符复制到功能结构的 **szPname** 成员中。 对于长度超过31个字符的设备名称，客户端应用程序可以打开注册表项并直接读取整个字符串。 驱动程序可以通过以下两种方式之一填充此注册表项：

-   驱动程序可以在安装时指定设备 INF 文件中的条目。

-   驱动程序可以在其筛选器初始化例程执行期间加载条目。

Name GUID 是可选的。 如果驱动程序将 KSCOMPONENTID 中的 **名称** 成员设置为 GUID \_ NULL 值，则 WDMAud 会为 *xxx* GetDevCaps 函数提供设备的友好名称，该名称将此名称复制到功能结构的 **szPname** 成员中。

如果筛选器不公开 KSPROPERTY 常规组件器属性的处理程序 \_ \_ ，则 WDMAud 将使用默认值来代替 KSCOMPONENTID 结构中的数据。 功能结构的旧部分的默认值如下所示：

-   **wMid** = MM \_ MICROSOFT

-   **wPid** = 以下列表中的一个设备类： MM \_ MSFT \_ WDMAUDIO \_ WAVEOUT MM \_ msft \_ WDMAUDIO \_ WAVEIN mm \_ msft \_ WDMAUDIO \_ MIDIOUT WDMAUDIO \_ \_ \_ \_ \_ \_ \_ \_ \_
-   **vDriverVersion** = 适用于 windows xp) 或0x0500 的 0x050a ( (windows xp 以前的) 

在 Windows XP 之前的 Windows 版本中，功能结构的旧成员始终设置为上面的默认值。 在 Windows XP 和更高版本中，扩展功能的默认值如下所示：

-   **NameGuid** = GUID \_ NULL

-   INIT \_ MMREG \_ MID ( # B0 **ManufacturerGuid**， **wMid**) 

-   INIT \_ MMREG \_ PID ( # B0 **ProductGuid**， **wPid**) 

上述 INIT \_ MMREG \_ MID 和 init \_ MMREG \_ PID 宏是在 Ksmedia 中定义的。 这些宏用于将 **wMid** 和 **wPid** 成员中的制造商和产品 id 转换为加载到 **ManufacturerGuid** 和 **ProductGuid** 成员的 guid。

 

