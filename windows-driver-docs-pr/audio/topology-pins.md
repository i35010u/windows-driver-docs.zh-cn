---
title: 拓扑引脚
description: 拓扑引脚
ms.assetid: b434e2a7-4acc-4ef1-9db9-8f1b82f68de3
keywords:
- 拓扑引脚 WDK 音频
- 锁定 WDK 音频、拓扑
- S/PDIF pin 翻译 WDK 音频
- 锁定 WDK 音频，转换
- KS 引脚音频，转换
- 锁定 WDK 音频、描述符
- 混音器行描述符音频
- 源混合器线条 WDK 音频
- 目标混音器线条 WDK 音频
- 转换引脚 WDK 音频
- 固定工厂的 WDK 音频
- PCPIN_DESCRIPTOR 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf5f99615cc377bfae1528448af03d16617681e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832334"
---
# <a name="topology-pins"></a>拓扑引脚


## <span id="topology_pins"></span><span id="TOPOLOGY_PINS"></span>


[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)将 KS 筛选器上的拓扑引脚转换为混音器 API 公开给应用程序的源和目标混音器行。 输入（接收器）插针成为源混合器行，输出（源）引脚成为目标混音器线。

如[Pin 工厂](pin-factories.md)中所述，微型端口驱动程序提供了一系列 pin 描述符，其中每个描述符都是[**PCPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)的结构，用于描述属于筛选器的 Pin 工厂。 每个 pin 描述符都包含以下信息：

-   **数据流方向说明符**

    指示数据流是否进入（KSPIN\_数据流\_中）或退出（KSPIN\_数据流\_OUT）通过 pin 的筛选器。

-   **KS pin 类别 GUID**

    指示 pin 所属的 pin 类别。 例如，在音频播放设备上，一个 pin 可能会接受波形格式的数字音频流，另一个 pin 可能会生成模拟音频信号来驱动扬声器。 微型端口驱动程序将这两种类型的 pin 标识为属于不同的 pin 类别。

-   **通信类型说明符**

    指示 pin 支持的 IRP 通信的类型。 支持 IRP 通信的 pin 可以是 IRP 接收器（KSPIN\_通信\_接收器）、IRP 源（KSPIN\_通信\_源），或两者（KSPIN\_通信\_两者）。 不支持 IRP 通信的 pin 既可以位于 KS 筛选器关系图中（KSPIN\_通信\_NONE），也可以是位于关系图终结点（KSPIN\_通信\_桥）的*桥接*。

有关桥接 pin 的详细信息，请参阅[音频筛选器图](audio-filter-graphs.md)。

WDMAud 将来自微型端口驱动程序的 pin 描述符的信息转换为一个混音器描述符，它是 MIXERLINE 类型的结构，其中包含以下信息：

-   **混合器行组件类型**

    指示混音器线条是否为源线或目标线，还指示混音器线条的一般功能。 例如，混音器线的组件类型将从 wave 输出（渲染）流生成的模拟信号传输到驱动一组耳机，就是 MIXERLINE\_COMPONENTTYPE\_DST\_耳机。

-   **混音器行目标类型**

    指示混音器线路传输的数据流类型。 例如，波形输出（渲染）流的目标类型为 MIXERLINE\_TARGETTYPE\_WAVEOUT，而波形输入（捕获）流的目标类型为 MIXERLINE\_TARGETTYPE\_WAVEIN。

有关 MIXERLINE 结构的详细信息，请参阅 Microsoft Windows SDK 文档。

以下两个表显示了 WDMAud 如何将输入（KSPIN\_数据流\_）转换为源混合器行。 第一个表显示输入插针**KS pin 类别 GUID**如何映射到关联的 MIXERLINE 目标类型。

PCPIN\_描述符值 MIXERLINE 值 KS pin 类别 GUID 桥插？
目标类型 KSNODETYPE\_麦克风

KSNODETYPE\_桌面\_麦克风

--

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_旧\_音频\_连接器

KSCATEGORY\_音频

KSNODETYPE\_发言人

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_CD\_播放器

--

MIXERLINE\_TARGETTYPE\_未定义

KSNODETYPE\_合成器

--

MIXERLINE\_TARGETTYPE\_MIDIOUT

KSNODETYPE\_LINE\_连接器

--

MIXERLINE\_TARGETTYPE\_未定义

KSNODETYPE\_电话

KSNODETYPE\_电话\_行

KSNODETYPE\_向下\_LINE\_手机

--

MIXERLINE\_TARGETTYPE\_未定义

KSNODETYPE\_模拟\_连接器

“是”

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_模拟\_连接器

无

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_SPDIF\_接口

“是”

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_SPDIF\_接口

无

MIXERLINE\_TARGETTYPE\_WAVEOUT

 

下表显示了输入插针**KS pin 类别 GUID**如何映射到关联的 MIXERLINE 组件类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCPIN_DESCRIPTOR 值</th>
<th align="left">MIXERLINE 值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">KS pin 类别 GUID</td>
<td align="left">组件类型</td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_MICROPHONE</p>
<p>KSNODETYPE_DESKTOP_MICROPHONE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_MICROPHONE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_LEGACY_AUDIO_CONNECTOR</p>
<p>KSCATEGORY_AUDIO</p>
<p>KSNODETYPE_SPEAKER</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_WAVEOUT</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_CD_PLAYER</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_COMPACTDISC</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_SYNTHESIZER</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_SYNTHESIZER</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_LINE_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_LINE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_TELEPHONE</p>
<p>KSNODETYPE_PHONE_LINE</p>
<p>KSNODETYPE_DOWN_LINE_PHONE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_TELEPHONE</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_ANALOG</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_ANALOG</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_DIGITAL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_SRC_DIGITAL</p></td>
</tr>
</tbody>
</table>

 

在前面的表中，左栏指定了 pin 的 PCPIN\_描述符结构中的 pin 类别 GUID，右侧列指定了 MIXERLINE 结构的相应目标类型和组件类型。

列中的条目标有 "桥接 Pin？" 指示 pin 是否为桥接 pin。 "是" 表示 pin 通信类型为 KSPIN\_通信\_BRIDGE。 如果是 "否"，则表示 pin 通信类型为 KSPIN\_通信\_*Xxx*值（而不是 KSPIN\_通信\_桥）。 如果在将 pin 参数转换为混音器参数时 WDMAud 忽略 pin 通信类型，则 "桥接" 条目为短划线（-）。

对于上表中未显示的所有 pin 类别，WDMAud 会将输入插针转换为 MIXERLINE\_TARGETTYPE 的目标类型的源混合器行，并将 MIXERLINE 的\_\_COMPONENTTYPE\_SRC\_UNDEFINED。

下表显示了 WDMAud 如何将输出（KSPIN\_数据流\_输出）转换为目标混音器行。 列标题与上表中的相同。 第一个表显示 output 引脚**KS pin 类别 GUID**如何映射到关联的 MIXERLINE 目标类型。

PCPIN\_描述符值 MIXERLINE 值 KS pin 类别 GUID 桥插？
目标类型 KSNODETYPE\_发言人

KSNODETYPE\_桌面\_发言人

KSNODETYPE\_发言人\_会议室

KSNODETYPE\_通信\_发言人

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSCATEGORY\_音频

PINNAME\_捕获

--

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_耳机

KSNODETYPE\_HEAD\_装载的\_显示\_音频

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_电话

KSNODETYPE\_电话\_行

KSNODETYPE\_向下\_LINE\_手机

--

MIXERLINE\_TARGETTYPE\_未定义

KSNODETYPE\_模拟\_连接器

“是”

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_模拟\_连接器

无

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_SPDIF\_接口

“是”

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_SPDIF\_接口

无

MIXERLINE\_TARGETTYPE\_WAVEIN

 

下表显示 output 引脚**KS pin 类别 GUID**如何映射到关联的 MIXERLINE 组件类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCPIN_DESCRIPTOR 值</th>
<th align="left">MIXERLINE 值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">KS pin 类别 GUID</td>
<td align="left">组件类型</td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_SPEAKER</p>
<p>KSNODETYPE_DESKTOP_SPEAKER</p>
<p>KSNODETYPE_ROOM_SPEAKER</p>
<p>KSNODETYPE_COMMUNICATION_SPEAKER</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_SPEAKERS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSCATEGORY_AUDIO</p>
<p>PINNAME_CAPTURE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_WAVEIN</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_HEADPHONES</p>
<p>KSNODETYPE_HEAD_MOUNTED_DISPLAY_AUDIO</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_HEADPHONES</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_TELEPHONE</p>
<p>KSNODETYPE_PHONE_LINE</p>
<p>KSNODETYPE_DOWN_LINE_PHONE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_TELEPHONE</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_SPEAKERS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_ANALOG_CONNECTOR</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_WAVEIN</p></td>
</tr>
<tr class="even">
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_SPEAKERS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KSNODETYPE_SPDIF_INTERFACE</p></td>
<td align="left"><p>MIXERLINE_COMPONENTTYPE_DST_WAVEIN</p></td>
</tr>
</tbody>
</table>

 

对于上表中未显示的所有 pin 类别，WDMAud 将输出插针转换为目标混音器行，其目标类型为 MIXERLINE\_TARGETTYPE\_未定义，组件类型为 MIXERLINE\_COMPONENTTYPE\_DST\_未定义。

在前面的表中，大多数 KS pin 类别 Guid 都具有 KSNODETYPE\_*Xxx*名称。 在头文件 Ksmedia 和 Dmusprop 中定义这些名称。 （这种命名约定中的两个出发是 Guid KSCATEGORY\_音频和 PINNAME\_捕获，它们也在 Ksmedia 中定义。）如[拓扑节点](topology-nodes.md)中所述，KSNODETYPE\_*Xxx* guid 还可用于指定 KS 节点类型。 大多数 KSNODETYPE\_*Xxx* guid 指定固定类别或节点类型，但不能同时指定两者。 [**KSNODETYPE\_合成**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer)器例外，它可以指定 pin 类别或节点类型，具体取决于使用的上下文。 有关表示 pin 类别的 KSNODETYPE\_*Xxx* guid 的列表，请参阅[固定类别属性](pin-category-property.md)。 有关表示节点类型的 KSNODETYPE\_*Xxx* guid 的列表，请参阅[音频拓扑节点](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-topology-nodes)。

KSCATEGORY\_音频是另一个双重使用 GUID。 它可用作**ks pin 类别 guid**或**ks 筛选器类别 guid**，具体取决于上下文。 在设备安装过程中，音频驱动程序会在 KSCATEGORY\_音频的筛选器类别下注册其设备接口。 有关详细信息，请参阅[安装音频适配器的设备接口](installing-device-interfaces-for-an-audio-adapter.md)。

对于 KSNODETYPE 的 pin 类别\_模拟\_连接器或 KSNODETYPE\_SPDIF\_接口，WDMAud 需要知道 pin 是否为桥接 pin，以将 pin 正确地转换为其等效的混合器行。 例如，S/PDIF pin （带有 pin 类别 KSNODETYPE\_SPDIF\_接口）转换为以下四种混音器类型中的一种： 转换取决于 pin 的数据方向（传入或传出）以及它是否为桥接（是或否），它们共同产生了四种可能的混音器线类型（在 + yes 中、在 + no、out + yes 和 out + no 中）。 图中所示的四个混合器线条类型表示上表中的下一对条目。

![说明如何将 s/pdif pin 转换为混音器线的关系图](images/spdifpin.png)

请注意，图中音频设备右侧的两个流为 S/PDIF 格式，左侧的两个流采用波形格式。 音频设备执行两种数字格式之间的转换。

SndVol32 应用程序是混音器 API 的客户端。 混音器 API 将拓扑中找到的每个 pin 转换为源或目标混音器行，但该线条可能不会显示在 SndVol32 中，后者仅识别标头文件 Mmsystem 为混音器 API 定义的混音器线组件类型的子集。 有关 SndVol32 的详细信息，请参阅 "[托盘" 和 "SndVol32](systray-and-sndvol32.md)"。

 

 




