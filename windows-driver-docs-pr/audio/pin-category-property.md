---
title: 引脚类别属性
description: 引脚类别属性
ms.assetid: fd4a4afd-2c17-4002-87ae-21501b1d75c1
keywords:
- 音频属性 WDK，pin
- WDM 音频属性 WDK，pin
- pin WDK 音频，类别
- 输入终端标识符 WDK 音频
- 输出终端标识符 WDK 音频
- 双向终端标识符 WDK 音频
- 电话服务终端标识符 WDK 音频
- 外部终端标识符 WDK 音频
- 嵌入的函数终端标识符 WDK 音频
- 终端标识符 WDK 音频
- Guid WDK 音频
- 类别 Guid WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5909bf2de298ed4e3a1eee9de3121dc4d4e14e4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566381"
---
# <a name="pin-category-property"></a>引脚类别属性


## <span id="pin_category_property"></span><span id="PIN_CATEGORY_PROPERTY"></span>


Microsoft Windows 驱动程序模型 (WDM) USB 音频设备、 IEEE 1394 音频设备和所有内部总线上的音频设备的音频驱动程序表示 KS 筛选器以插针为其设备。 WDM 音频驱动程序会维护一个[ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)它支持每个固定类型的结构。 在此结构中，该驱动程序存储[KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584) pin 类型的属性。 这些属性之一是，即[ **KSPROPERTY\_PIN\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff565192)属性。 此属性的请求检索 KS pin 类别 GUID 从**KSPIN\_描述符**结构的**类别**成员。 此 GUID 表示 pin 提供的功能的常规类别。 例如，某个特定 pin 类别 GUID，KSNODETYPE\_耳机，标识为耳机输出插孔的 pin。

波形音频设备内部总线 (例如，PCI) 上，如果 PortCls 微型端口驱动程序包含的 pin 描述符的数组，其中每个描述 pin 类型表示的设备筛选器中。 每个 pin 描述符[ **PCPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537721)结构，它包含一个嵌入[ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)具有 pin 类别 GUID 结构。 在接收时[ **KSPROPERTY\_PIN\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff565192)属性从客户端请求端口驱动程序从微型端口驱动程序的 pin 说明符中检索 pin 类别 GUID对于指定的 pin 类型中。 关于 pin 描述符的详细信息，请参阅[Pin 工厂](pin-factories.md)。

USB 音频设备有一定数量的终端，通过该数字的流和模拟信号可以进入和退出设备。 构造 KS 筛选器来表示 USB 音频设备时[USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)会在设备上的终端将转换为筛选器上的 pin。 标头文件 Ksmedia.h 到 KS pin 类别 GUID 定义为每个 USB 终端类型标识符的映射。 以下六个表显示终端类型标识符和其相应的 pin 类别的 Guid。

### <a name="span-idinputterminaltypesspanspan-idinputterminaltypesspan-input-terminal-types"></a><span id="input_terminal_types"></span><span id="INPUT_TERMINAL_TYPES"></span> 输入终端类型

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 终端 ID</th>
<th align="left">KS Pin 类别 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0201</p></td>
<td align="left"><p>KSNODETYPE_MICROPHONE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0202</p></td>
<td align="left"><p>KSNODETYPE_DESKTOP_MICROPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0203</p></td>
<td align="left"><p>KSNODETYPE_PERSONAL_MICROPHONE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0204</p></td>
<td align="left"><p>KSNODETYPE_OMNI_DIRECTIONAL_MICROPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0205</p></td>
<td align="left"><p>KSNODETYPE_MICROPHONE_ARRAY</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0206</p></td>
<td align="left"><p>KSNODETYPE_PROCESSING_MICROPHONE_ARRAY</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idoutputterminaltypesspanspan-idoutputterminaltypesspan-output-terminal-types"></a><span id="output_terminal_types"></span><span id="OUTPUT_TERMINAL_TYPES"></span> 输出终端类型

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 终端 ID</th>
<th align="left">KS Pin 类别 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0301</p></td>
<td align="left"><p>KSNODETYPE_SPEAKER</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0302</p></td>
<td align="left"><p>KSNODETYPE_HEADPHONES</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0303</p></td>
<td align="left"><p>KSNODETYPE_HEAD_MOUNTED_DISPLAY_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0304</p></td>
<td align="left"><p>KSNODETYPE_DESKTOP_SPEAKER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0305</p></td>
<td align="left"><p>KSNODETYPE_ROOM_SPEAKER</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0306</p></td>
<td align="left"><p>KSNODETYPE_COMMUNICATION_SPEAKER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0307</p></td>
<td align="left"><p>KSNODETYPE_LOW_FREQUENCY_EFFECTS_SPEAKER</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idbidirectionalterminaltypesspanspan-idbidirectionalterminaltypesspan-bidirectional-terminal-types"></a><span id="bidirectional_terminal_types"></span><span id="BIDIRECTIONAL_TERMINAL_TYPES"></span> 双向终端类型

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 终端 ID</th>
<th align="left">KS Pin 类别 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0401</p></td>
<td align="left"><p>KSNODETYPE_HANDSET</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0402</p></td>
<td align="left"><p>KSNODETYPE_HEADSET</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0403</p></td>
<td align="left"><p>KSNODETYPE_SPEAKERPHONE_NO_ECHO_REDUCTION</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0404</p></td>
<td align="left"><p>KSNODETYPE_ECHO_SUPPRESSING_SPEAKERPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0405</p></td>
<td align="left"><p>KSNODETYPE_ECHO_CANCELING_SPEAKERPHONE</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idtelephonyterminaltypesspanspan-idtelephonyterminaltypesspan-telephony-terminal-types"></a><span id="telephony_terminal_types"></span><span id="TELEPHONY_TERMINAL_TYPES"></span> 电话服务终端类型

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 终端 ID</th>
<th align="left">KS Pin 类别 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0501</p></td>
<td align="left"><p>KSNODETYPE_PHONE_LINE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0502</p></td>
<td align="left"><p>KSNODETYPE_TELEPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0503</p></td>
<td align="left"><p>KSNODETYPE_DOWN_LINE_PHONE</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idexternalterminaltypesspanspan-idexternalterminaltypesspan-external-terminal-types"></a><span id="external_terminal_types"></span><span id="EXTERNAL_TERMINAL_TYPES"></span> 外部终端类型

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 终端 ID</th>
<th align="left">KS Pin 类别 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0601</p></td>
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0602</p></td>
<td align="left"><p>KSNODETYPE_DIGITAL_AUDIO_INTERFACE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0603</p></td>
<td align="left"><p>KSNODETYPE_LINE_CONNECTOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0604</p></td>
<td align="left"><p>KSNODETYPE_LEGACY_AUDIO_CONNECTOR</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0605</p></td>
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0606</p></td>
<td align="left"><p>KSNODETYPE_1394_DA_STREAM</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0607</p></td>
<td align="left"><p>KSNODETYPE_1394_DV_STREAM_SOUNDTRACK</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idembeddedfunctionterminaltypesspanspan-idembeddedfunctionterminaltypesspan-embedded-function-terminal-types"></a><span id="embedded_function_terminal_types"></span><span id="EMBEDDED_FUNCTION_TERMINAL_TYPES"></span> 嵌入的函数终端类型

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB 终端 ID</th>
<th align="left">KS Pin 类别 GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0701</p></td>
<td align="left"><p>KSNODETYPE_LEVEL_CALIBRATION_NOISE_SOURCE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0702</p></td>
<td align="left"><p>KSNODETYPE_EQUALIZATION_NOISE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0703</p></td>
<td align="left"><p>KSNODETYPE_CD_PLAYER</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0704</p></td>
<td align="left"><p>KSNODETYPE_DAT_IO_DIGITAL_AUDIO_TAPE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0705</p></td>
<td align="left"><p>KSNODETYPE_DCC_IO_DIGITAL_COMPACT_CASSETTE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0706</p></td>
<td align="left"><p>KSNODETYPE_MINIDISK</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0707</p></td>
<td align="left"><p>KSNODETYPE_ANALOG_TAPE</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0708</p></td>
<td align="left"><p>KSNODETYPE_PHONOGRAPH</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0709</p></td>
<td align="left"><p>KSNODETYPE_VCR_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x070A</p></td>
<td align="left"><p>KSNODETYPE_VIDEO_DISC_AUDIO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x070B</p></td>
<td align="left"><p>KSNODETYPE_DVD_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x070C</p></td>
<td align="left"><p>KSNODETYPE_TV_TUNER_AUDIO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x070D</p></td>
<td align="left"><p>KSNODETYPE_SATELLITE_RECEIVER_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x070E</p></td>
<td align="left"><p>KSNODETYPE_CABLE_TUNER_AUDIO</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x070F</p></td>
<td align="left"><p>KSNODETYPE_DSS_AUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0710</p></td>
<td align="left"><p>KSNODETYPE_RADIO_RECEIVER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0711</p></td>
<td align="left"><p>KSNODETYPE_RADIO_TRANSMITTER</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0712</p></td>
<td align="left"><p>KSNODETYPE_MULTITRACK_RECORDER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0713</p></td>
<td align="left"><p>KSNODETYPE_SYNTHESIZER</p></td>
</tr>
</tbody>
</table>

 

有关 USB 终端类型标识符的详细信息，请参阅*通用串行总线的设备类定义的终端类型*（版本 1.0），可通过[USB 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)网站。

上表中的所有 pin 类别 Guid 都具有参数名称的窗体 KSNODETYPE\_*XXX*。 请注意，KS 节点类型的 Guid 还具有 KSNODETYPE\_*XXX*参数名称。 此命名约定创建一些可能出现的混淆 pin 类别 Guid 和节点类型的 Guid。 幸运的是，几乎每个 KSNODETYPE\_*XXX*参数标识 pin 类别或一个节点类型，但不可同时使用两者。 该规则的一个例外是[ **KSNODETYPE\_合成器**](https://msdn.microsoft.com/library/windows/hardware/ff537203)，可识别 pin 类别或节点类型，具体取决于上下文。 节点类型的 Guid 的列表，请参阅[音频拓扑节点](https://msdn.microsoft.com/library/windows/hardware/ff536219)。

实例化 USB 音频设备，USBAudio 类系统驱动程序会查询其内部的拓扑，包括其终端的设备。 使用此信息，USBAudio 驱动程序构造筛选器来表示设备，并将转换上筛选器对应的插针为每个终端。 在此过程中，该驱动程序将每个 USB 终端类型标识符转换为其相应 KS pin 类别 GUID，它是一个在前面的表中的 Guid。 驱动程序构造[ **KSPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff563533)结构来描述 pin，并且它将 pin 类别 GUID 写入到结构。

PortCls 微型端口驱动程序不一定使用类别显示在前面的 6 个表中的 Guid。 例如，驱动程序可能会定义和使用自定义的 pin 类别 GUID 来描述其功能的类别范围之外的表中的类别的 pin 类型。 正常情况下，自定义的 pin 类别 GUID 可仅对识别 GUID 的客户端。

音频子系统维护 pin 类别 Guid 的列表，以及在系统注册表中其关联的友好名称。 Guid 和友好名称存储在注册表路径 HKLM\\系统\\CurrentControlSet\\控制\\MediaCategories。 媒体类安装程序会将 GUID 名称对复制到从 Ks.inf 文件位于主 Windows 文件夹 Inf 子文件夹中的注册表 (例如，c:\\Windows\\Inf\\Ks.inf)。

在 Windows Vista 及更高版本，操作系统使用 pin 类别将友好名称与音频终结点设备相关联。 有关如何将友好名称与音频终结点设备相关联的详细信息，请参阅[终结点的音频设备的友好名称](friendly-names-for-audio-endpoint-devices.md)。

在 Windows XP、 Windows 2000 和 Windows Millennium Edition 中，操作系统能够仅有限的使用 pin 类别。 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)混音器 API 将翻译为 MIXERLINE pin 类别 Guid 代表\_COMPONENTTYPE\_*XXX*供客户端应用程序使用的值。 WDMAud 识别 pin 类别显示在前面的 6 个表中的 Guid 的一个子集。 此外，由于历史原因，WDMAud 识别两个 pin 类别 Guid，KSCATEGORY\_音频和 PINNAME\_捕获，并显示在表中。 有关 pin 类别对混音器行的转换的详细信息，请参阅[拓扑 Pin](topology-pins.md)。 有关混音器 API 的信息，请参阅 Windows SDK 文档。

 

 




