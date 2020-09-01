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
ms.openlocfilehash: 56d02d3dfbbe4108f59ea7cca42793431dbf85f3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209933"
---
# <a name="topology-pins"></a>拓扑引脚


## <span id="topology_pins"></span><span id="TOPOLOGY_PINS"></span>


[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)将 KS 筛选器上的拓扑引脚转换为混音器 API 公开给应用程序的源和目标混音器行。 输入 (接收器) 针成为源混音器线条，输出 (源) 针变为目标混音器线。

如 [Pin 工厂](pin-factories.md)中所述，微型端口驱动程序提供了一系列 pin 描述符，其中每个描述符都是描述属于筛选器的 Pin 工厂的 [**PCPIN \_ 描述符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor) 类型的结构。 每个 pin 描述符都包含以下信息：

-   **数据流方向说明符**

    指示数据流是否进入) 中的 (KSPIN \_ 数据流 \_ ，或退出 (KSPIN \_ \_ 通过 pin) 筛选器。

-   **KS pin 类别 GUID**

    指示 pin 所属的 pin 类别。 例如，在音频播放设备上，一个 pin 可能会接受波形格式的数字音频流，另一个 pin 可能会生成模拟音频信号来驱动扬声器。 微型端口驱动程序将这两种类型的 pin 标识为属于不同的 pin 类别。

-   **通信类型说明符**

    指示 pin 支持的 IRP 通信的类型。 支持 IRP 通信的 pin 可以是 IRP 接收器 (KSPIN 的 \_ 通信 \_ 接收器) 、irp 源 (KSPIN \_ 通信 \_ 源) ，或两者 (两种) 的 KSPIN \_ 通信 \_ 。 不支持 IRP 通信的 pin 可以位于 KS 筛选器图中 (KSPIN \_ 通信 \_ 无) ，也可以是图形终结点上的 *桥接* (KSPIN \_ 通信 \_ 桥) 。

有关桥接 pin 的详细信息，请参阅 [音频筛选器图](audio-filter-graphs.md)。

WDMAud 将来自微型端口驱动程序的 pin 描述符的信息转换为一个混音器描述符，它是 MIXERLINE 类型的结构，其中包含以下信息：

-   **混合器行组件类型**

    指示混音器线条是否为源线或目标线，还指示混音器线条的一般功能。 例如，混音器线的组件类型会传输从 wave 输出生成的模拟信号， (呈现) 流来驱动一组耳机，就是 MIXERLINE \_ COMPONENTTYPE \_ DST \_ 耳机。

-   **混音器行目标类型**

    指示混音器线路传输的数据流类型。 例如， (呈现) 流的波形输出目标类型为 MIXERLINE \_ TARGETTYPE \_ WAVEOUT，而波形输入 (捕获) 流的目标类型为 MIXERLINE \_ TARGETTYPE \_ WAVEIN。

有关 MIXERLINE 结构的详细信息，请参阅 Microsoft Windows SDK 文档。

以下两个表显示了 WDMAud 如何 \_ \_ 在) 引脚中将输入 (KSPIN 数据流转换为源混音器行。 第一个表显示输入插针 **KS pin 类别 GUID**如何映射到关联的 MIXERLINE 目标类型。

PCPIN \_ 描述符值 MIXERLINE 值 KS pin 类别 GUID 桥插？
目标类型 KSNODETYPE \_ 麦克风

KSNODETYPE \_ 桌面 \_ 麦克风

--

MIXERLINE \_ TARGETTYPE \_ WAVEIN

KSNODETYPE \_ 传统 \_ 音频 \_ 连接器

KSCATEGORY \_ 音频

KSNODETYPE \_ 发言人

--

MIXERLINE \_ TARGETTYPE \_ WAVEOUT

KSNODETYPE \_ CD \_ 播放机

--

\_ \_ 未定义 MIXERLINE TARGETTYPE

KSNODETYPE \_ 合成器

--

MIXERLINE \_ TARGETTYPE \_ MIDIOUT

KSNODETYPE \_ 线 \_ 连接器

--

\_ \_ 未定义 MIXERLINE TARGETTYPE

KSNODETYPE \_ 电话

KSNODETYPE \_ 电话线 \_

KSNODETYPE \_ \_ \_ 电话

--

\_ \_ 未定义 MIXERLINE TARGETTYPE

KSNODETYPE \_ 模拟 \_ 连接器

是

MIXERLINE \_ TARGETTYPE \_ WAVEIN

KSNODETYPE \_ 模拟 \_ 连接器

否

MIXERLINE \_ TARGETTYPE \_ WAVEOUT

KSNODETYPE \_ SPDIF \_ 接口

是

MIXERLINE \_ TARGETTYPE \_ WAVEIN

KSNODETYPE \_ SPDIF \_ 接口

否

MIXERLINE \_ TARGETTYPE \_ WAVEOUT

 

下表显示了输入插针 **KS pin 类别 GUID**如何映射到关联的 MIXERLINE 组件类型。

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

 

在前面的表中，左栏指定了 pin 的 PCPIN 描述符结构中的 pin 类别 GUID \_ ，右侧列指定了 MIXERLINE 结构的相应目标类型和组件类型。

列中的条目标有 "桥接 Pin？" 指示 pin 是否为桥接 pin。 "是" 表示 pin 通信类型为 KSPIN \_ COMMUNICATION \_ BRIDGE。 如果是 "否"，则表示 pin 通信类型为 KSPIN \_ 通信 \_ *Xxx*值，而不是 KSPIN \_ 通信 \_ 桥。 如果在将 pin 参数转换为混音器参数时 WDMAud 忽略 pin 通信类型，则 "桥接" 条目是一个短划线 (-) 。

对于上表中未显示的所有 pin 类别，WDMAud 会将输入插针转换为未定义 MIXERLINE TARGETTYPE 目标类型的源混合器行， \_ \_ 并将 MIXERLINE COMPONENTTYPE 源的组件类型 \_ 定义为 \_ \_ undefined。

下表显示了 WDMAud 如何将输出 (KSPIN 的输出转换 \_ \_ 为向目标混音器行) 针脚。 列标题与上表中的相同。 第一个表显示 output 引脚 **KS pin 类别 GUID**如何映射到关联的 MIXERLINE 目标类型。

PCPIN \_ 描述符值 MIXERLINE 值 KS pin 类别 GUID 桥插？
目标类型 KSNODETYPE \_ 演讲者

KSNODETYPE \_ 桌面 \_ 扬声器

KSNODETYPE \_ 房间 \_ 发言人

KSNODETYPE \_ 通信 \_ 发言人

--

MIXERLINE \_ TARGETTYPE \_ WAVEOUT

KSCATEGORY \_ 音频

PINNAME \_ 捕获

--

MIXERLINE \_ TARGETTYPE \_ WAVEIN

KSNODETYPE \_ 耳机

KSNODETYPE \_ 头盔 \_ \_ 显示 \_ 音频

--

MIXERLINE \_ TARGETTYPE \_ WAVEOUT

KSNODETYPE \_ 电话

KSNODETYPE \_ 电话线 \_

KSNODETYPE \_ \_ \_ 电话

--

\_ \_ 未定义 MIXERLINE TARGETTYPE

KSNODETYPE \_ 模拟 \_ 连接器

是

MIXERLINE \_ TARGETTYPE \_ WAVEOUT

KSNODETYPE \_ 模拟 \_ 连接器

否

MIXERLINE \_ TARGETTYPE \_ WAVEIN

KSNODETYPE \_ SPDIF \_ 接口

是

MIXERLINE \_ TARGETTYPE \_ WAVEOUT

KSNODETYPE \_ SPDIF \_ 接口

否

MIXERLINE \_ TARGETTYPE \_ WAVEIN

 

下表显示 output 引脚 **KS pin 类别 GUID**如何映射到关联的 MIXERLINE 组件类型。

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

 

对于上表中未显示的所有 pin 类别，WDMAud 会将输出插针转换为目标混音器行，其目标类型为 MIXERLINE \_ TARGETTYPE， \_ 未定义 MIXERLINE \_ COMPONENTTYPE DST 的组件类型 \_ \_ 。

在前面的表中，大多数 KS pin 类别 Guid 都具有 KSNODETYPE 的 \_ *Xxx*名称。 在头文件 Ksmedia 和 Dmusprop 中定义这些名称。  (这种命名约定中的两个出发都是 Guid KSCATEGORY \_ 音频和 PINNAME \_ 捕获，如[拓扑节点](topology-nodes.md)中所述 ) ，KSNODETYPE \_ *XXX* guid 还可用于指定 KS 节点类型。 大多数 KSNODETYPE \_ *Xxx* guid 指定固定类别或节点类型，但不能同时指定两者。 [**KSNODETYPE \_ 合成**](./ksnodetype-synthesizer.md)器例外，它可以指定 pin 类别或节点类型，具体取决于使用的上下文。 有关 \_ 表示 pin 类别的 KSNODETYPE*Xxx* guid 列表，请参阅[固定类别属性](pin-category-property.md)。 有关 \_ 表示节点类型的 KSNODETYPE*Xxx* guid 列表，请参阅[音频拓扑节点](./audio-topology-nodes.md)。

KSCATEGORY \_ AUDIO 是另一个双重使用 GUID。 它可用作 **ks pin 类别 guid** 或 **ks 筛选器类别 guid**，具体取决于上下文。 在设备安装过程中，音频驱动程序在筛选器类别 KSCATEGORY 音频下注册其设备接口 \_ 。 有关详细信息，请参阅 [安装音频适配器的设备接口](installing-device-interfaces-for-an-audio-adapter.md)。

对于 KSNODETYPE \_ 模拟 \_ 连接器或 KSNODETYPE SPDIF 接口的 pin \_ 类别 \_ ，WDMAud 需要知道 pin 是否为桥接 pin，以将 pin 正确地转换为其等效混音器。 例如，使用 pin 类别 KSNODETYPE SPDIF 接口 (S/PDIF pin \_ \_) 可转换为以下四个混合器行类型之一。 转换取决于 pin 的数据方向 (为 ") " 或 "传出"，以及它是否是一个桥接 ("是" 或 "否") ，它们共同产生了四种可能的混音器线类型 (在 + yes、in + no、out + yes 和 out + no) 中。 图中所示的四个混合器线条类型表示上表中的下一对条目。

![说明如何将 s/pdif pin 转换为混音器线的关系图](images/spdifpin.png)

请注意，图中音频设备右侧的两个流为 S/PDIF 格式，左侧的两个流采用波形格式。 音频设备执行两种数字格式之间的转换。

SndVol32 应用程序是混音器 API 的客户端。 混音器 API 将拓扑中找到的每个 pin 转换为源或目标混音器行，但该线条可能不会显示在 SndVol32 中，后者仅识别标头文件 Mmsystem 为混音器 API 定义的混音器线组件类型的子集。 有关 SndVol32 的详细信息，请参阅 " [托盘" 和 "SndVol32](systray-and-sndvol32.md)"。

 

