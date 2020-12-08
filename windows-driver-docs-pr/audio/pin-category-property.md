---
title: 引脚类别属性
description: 引脚类别属性
keywords:
- 音频属性 WDK，pin
- WDM 音频属性 WDK，pin
- 锁定 WDK 音频，类别
- 输入终端标识符 WDK 音频
- 输出终端标识符 WDK 音频
- 双向终端标识符 WDK 音频
- 电话服务终端标识符 WDK 音频
- 外部终端标识符 WDK 音频
- 嵌入函数终端标识符 WDK 音频
- 终端标识符 WDK 音频
- Guid WDK 音频
- 类别 Guid WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 707977c73486c44e39ed1a659b98f7170616e696
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800935"
---
# <a name="pin-category-property"></a>引脚类别属性


## <span id="pin_category_property"></span><span id="PIN_CATEGORY_PROPERTY"></span>


Microsoft Windows 驱动模型 (WDM) 用于 USB 音频设备、IEEE 1394 音频设备和内置总线上音频设备的音频驱动程序，它们都将其设备表示为带有 pin 的 KS 筛选器。 WDM 音频驱动程序为其支持的每个 pin 类型维护一个 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor) 结构。 在此结构中，驱动程序存储固定类型的 [KSPROPSETID \_ pin](../stream/kspropsetid-pin.md) 属性。 在这些属性中， [**KSPROPERTY \_ 固定 \_ 类别**](../stream/ksproperty-pin-category.md) 属性。 此属性的请求从 **KSPIN \_ 描述符** 结构的 **类别** 成员检索 KS pin 类别 GUID。 此 GUID 指示 pin 提供的常规功能类别。 例如，特定的 pin 类别 GUID KSNODETYPE 耳机将 \_ pin 标识为耳机的输出插孔。

对于内部总线上的波形音频设备 (例如，PCI) ，PortCls 微型端口驱动程序包含一个 pin 描述符数组，其中每个描述符描述了表示设备的筛选器中的 pin 类型。 每个 pin 描述符都是一个 [**PCPIN \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor) 结构，其中包含具有 pin 类别 GUID 的嵌入 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor) 结构。 收到来自客户端的 [**KSPROPERTY \_ PIN \_ 类别**](../stream/ksproperty-pin-category.md) 属性请求后，端口驱动程序将从指定的 pin 类型的微型端口驱动程序的 pin 描述符检索 pin 类别 GUID。 有关 pin 描述符的详细信息，请参阅 [固定工厂](pin-factories.md)。

USB 音频设备具有一定数量的终端，其中的数字流和模拟信号可以进入和退出设备。 构造用于表示 USB 音频设备的 KS 筛选器时， [USBAudio 类系统驱动程序](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) 将设备上的终端转换为锁定筛选器上的 pin。 标头文件 Ksmedia 定义了每个 USB 终端类型标识符到 KS pin 类别 GUID 的映射。 以下六个表显示了终端类型标识符及其相应的 pin 类别 Guid。

### <a name="span-idinput_terminal_typesspanspan-idinput_terminal_typesspan-input-terminal-types"></a><span id="input_terminal_types"></span><span id="INPUT_TERMINAL_TYPES"></span> 输入终端类型

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

 

### <a name="span-idoutput_terminal_typesspanspan-idoutput_terminal_typesspan-output-terminal-types"></a><span id="output_terminal_types"></span><span id="OUTPUT_TERMINAL_TYPES"></span> 输出终端类型

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

 

### <a name="span-idbidirectional_terminal_typesspanspan-idbidirectional_terminal_typesspan-bidirectional-terminal-types"></a><span id="bidirectional_terminal_types"></span><span id="BIDIRECTIONAL_TERMINAL_TYPES"></span> 双向终端类型

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

 

### <a name="span-idtelephony_terminal_typesspanspan-idtelephony_terminal_typesspan-telephony-terminal-types"></a><span id="telephony_terminal_types"></span><span id="TELEPHONY_TERMINAL_TYPES"></span> 电话服务终端类型

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

 

### <a name="span-idexternal_terminal_typesspanspan-idexternal_terminal_typesspan-external-terminal-types"></a><span id="external_terminal_types"></span><span id="EXTERNAL_TERMINAL_TYPES"></span> 外部终端类型

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

 

### <a name="span-idembedded_function_terminal_typesspanspan-idembedded_function_terminal_typesspan-embedded-function-terminal-types"></a><span id="embedded_function_terminal_types"></span><span id="EMBEDDED_FUNCTION_TERMINAL_TYPES"></span> 嵌入函数终端类型

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

 

有关 USB 终端类型标识符的详细信息，请参阅 [Usb 实现论坛](https://www.usb.org/)网站上提供的终端类型 (版本 1.0) 的 *通用串行总线设备类定义*。

前面的表中的所有 pin 类别 Guid 都具有形式为 KSNODETYPE XXX 的参数名称 \_ *XXX*。 请注意，KS 节点类型 Guid 还具有 KSNODETYPE \_ *XXX* 参数名称。 此命名约定会导致在 pin 类别 Guid 与节点类型 Guid 之间产生混淆。 幸运的是，几乎每个 KSNODETYPE \_ *XXX* 参数都标识了 pin 类别或节点类型，但不能同时标识这两者。 规则的一个例外是 [**KSNODETYPE \_ 合成**](./ksnodetype-synthesizer.md)器，它可以标识 pin 类别或节点类型，具体取决于上下文。 有关节点类型 Guid 的列表，请参阅 [音频拓扑节点](./audio-topology-nodes.md)。

在实例化 USB 音频设备时，USBAudio 类系统驱动程序会在设备中查询其内部拓扑，包括其终端。 使用此信息，USBAudio 驱动程序将构造一个用于表示设备的筛选器，并将每个终端转换为筛选器上的相应 pin。 在此过程中，驱动程序将每个 USB 终端类型标识符转换为相应的 KS pin 类别 GUID，这是上述表中的 Guid 之一。 驱动程序将构造一个 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor) 结构来描述 pin，并将 pin 类别 GUID 写入结构中。

PortCls 微型端口驱动程序不一定只使用前面六个表中显示的类别 Guid。 例如，驱动程序可能定义并使用自定义 pin 类别 GUID 来描述其功能类别在表中的类别之外的 pin 类型。 自定义 pin 类别 GUID 当然仅适用于识别 GUID 的客户端。

音频子系统在系统注册表中维护 pin 类别 Guid 及其关联的友好名称的列表。 Guid 和友好名称存储在注册表路径 HKLM \\ SYSTEM \\ CurrentControlSet \\ Control \\ MediaCategories 中。 媒体类安装程序将 GUID 名称对从主 Windows 文件夹的 Inf 子文件夹中的 Ks 文件复制到注册表中 (例如，C： \\ Windows \\ inf \\ Ks) 。

在 Windows Vista 和更高版本中，操作系统使用 pin 类别将友好名称与音频终结点设备关联起来。 有关如何将友好名称与音频终结点设备关联的详细信息，请参阅 [音频终结点设备的友好名称](friendly-names-for-audio-endpoint-devices.md)。

在 Windows XP、Windows 2000 和 Windows Millennium Edition 中，操作系统仅限制使用 pin 类别。 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)代表混音器 API，将 Pin 类别 guid 转换为 MIXERLINE \_ COMPONENTTYPE \_ *XXX* 值，供客户端应用程序使用。 WDMAud 仅识别在前六个表中出现的 pin 类别 Guid 的子集。 此外，由于历史原因，WDMAud 识别出两个 \_ \_ 不会出现在表中的 Pin 类别 GUID，KSCATEGORY 音频和 PINNAME 捕获。 有关将 pin 类别翻译成混音器的详细信息，请参阅 [拓扑 pin](topology-pins.md)。 有关混音器 API 的信息，请参阅 Windows SDK 文档。

 

