---
title: 拓扑 Pin
description: 拓扑 Pin
ms.assetid: b434e2a7-4acc-4ef1-9db9-8f1b82f68de3
keywords:
- 拓扑 pin WDK 音频
- pin WDK 音频，拓扑
- S/PDIF pin 翻译 WDK 音频
- 固定 WDK 音频转换
- KS 固定 WDK 音频，转换
- pin WDK 音频，描述符
- mixer 行描述符 WDK 音频
- 源 mixer 行 WDK 音频
- 目标 mixer 行 WDK 音频
- 转换 pin WDK 音频
- pin 工厂 WDK 音频
- PCPIN_DESCRIPTOR 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2ec2c37f3b4244c8d17f5050eda21c0197adc78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524396"
---
# <a name="topology-pins"></a>拓扑 Pin


## <span id="topology_pins"></span><span id="TOPOLOGY_PINS"></span>


[WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)拓扑插针上 KS 筛选器转换为 mixer API 向应用程序公开的源和目标混音器行。 （接收器） 输入插针变为源 mixer 行，并且输出 （源） 插针成为目标混音器行。

如中所述[Pin 工厂](pin-factories.md)，微型端口驱动程序提供了一系列 pin 描述符，其中每个是类型的结构[ **PCPIN\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff537721) ，介绍属于筛选器的 pin 工厂。 每个 pin 描述符包含以下信息：

-   **数据流方向说明符**

    指示数据流是否进入 (KSPIN\_数据流\_中) 或退出 (KSPIN\_数据流\_出) 通过 pin 的筛选器。

-   **KS pin 类别 GUID**

    表示属于 pin 的 pin 类别。 例如，音频播放设备上一个插针可能会接受波形格式数字音频流，和另一个 pin 可能会生成模拟音频信号来驱动演讲者。 微型端口驱动程序标识为属于不同的 pin 类别 pin 这两种类型。

-   **通信类型说明符**

    指示 pin 支持的 IRP 通信的类型。 支持的 IRP 通信的 pin 可以是 IRP 接收器 (KSPIN\_通信\_接收器)，IRP 源 (KSPIN\_通信\_源)，和 / 或 (KSPIN\_通信\_两者). 不支持 IRP 的通信的 pin 可以 KS 筛选器关系图中的任一欺骗 (KSPIN\_通信\_NONE) 也是*桥 pin*在关系图的终结点 (KSPIN\_通信\_桥）。

有关桥的 pin 的详细信息，请参阅[音频筛选器关系图](audio-filter-graphs.md)。

WDMAud 信息转换为从微型端口驱动程序的 pin 描述符 mixer 行描述符，这是类型包括以下信息的 MIXERLINE 的结构：

-   **Mixer 行组件类型**

    指示 mixer 行是否为源或目标行，还指示混音器行的常规函数。 例如，传输从批生成模拟信号的混音器行的组件类型输出 （呈现） 流来驱动的耳机是 MIXERLINE\_COMPONENTTYPE\_DST\_耳机。

-   **Mixer 行目标类型**

    指示合成器行传输的数据流中的类型。 例如，会出现一批的目标类型输出 （呈现） 流是 MIXERLINE\_TARGETTYPE\_WAVEOUT 和目标类型的批输入 （捕获） 流为 MIXERLINE\_TARGETTYPE\_WAVEIN。

MIXERLINE 结构的详细信息，请参阅 Microsoft Windows SDK 文档。

以下两个表显示如何 WDMAud 转换输入 (KSPIN\_数据流\_IN) 到源混音器行的 pin。 第一个表显示如何输入固定**KS pin 类别 GUID**的映射到关联的 MIXERLINE 目标类型。

PCPIN\_描述符值 MIXERLINE 值 KS pin 类别 GUID 桥 pin？
目标类型 KSNODETYPE\_麦克风

KSNODETYPE\_DESKTOP\_MICROPHONE

--

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_旧版\_音频\_连接器

KSCATEGORY\_音频

KSNODETYPE\_演讲者

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_CD\_播放器

--

MIXERLINE\_TARGETTYPE\_未定义

KSNODETYPE\_合成器

--

MIXERLINE\_TARGETTYPE\_MIDIOUT

KSNODETYPE\_行\_连接器

--

MIXERLINE\_TARGETTYPE\_未定义

KSNODETYPE\_电话

KSNODETYPE\_PHONE\_行

KSNODETYPE\_向下\_行\_电话

--

MIXERLINE\_TARGETTYPE\_未定义

KSNODETYPE\_模拟\_连接器

是

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_模拟\_连接器

否

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_SPDIF\_INTERFACE

是

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_SPDIF\_INTERFACE

否

MIXERLINE\_TARGETTYPE\_WAVEOUT

 

下表显示了如何输入固定**KS pin 类别 GUID**的映射到关联的 MIXERLINE 组件类型。

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

 

在前面的表中，左侧的列指定的 pin 类别中的 pin PCPIN GUID\_描述符结构和右边的列指定相应的目标类型和 MIXERLINE 结构的组件类型。

标记为"桥固定？"的列中的条目 指示 pin 是否桥 pin。 "是"表示 pin 通信类型为 KSPIN\_通信\_桥。 Pin 通信键入"否"表示是 KSPIN\_通信\_*Xxx* KSPIN 以外的值\_通信\_桥。 如果 WDMAud 转换 mixer 行参数，"桥固定？"的固定参数时忽略 pin 通信类型 项是短划线 （-）。

不会显示在前面的表中的所有 pin 类别，WDMAud 都转换到源与目标类型的 MIXERLINE mixer 行输入插针\_TARGETTYPE\_未定义和组件类型的 MIXERLINE\_COMPONENTTYPE\_SRC\_未定义。

下表显示了如何 WDMAud 转换输出 (KSPIN\_数据流\_出) 到目标混音器行的 pin。 列标题具有相同的含义，如前面的表中所示。 第一个表显示了如何将固定输出**KS pin 类别 GUID**的映射到关联的 MIXERLINE 目标类型。

PCPIN\_描述符值 MIXERLINE 值 KS pin 类别 GUID 桥 pin？
目标类型 KSNODETYPE\_演讲者

KSNODETYPE\_DESKTOP\_SPEAKER

KSNODETYPE\_聊天室\_演讲者

KSNODETYPE\_通信\_演讲者

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSCATEGORY\_音频

PINNAME\_捕获

--

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_耳机

KSNODETYPE\_HEAD\_已装载\_显示\_音频

--

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_电话

KSNODETYPE\_PHONE\_行

KSNODETYPE\_向下\_行\_电话

--

MIXERLINE\_TARGETTYPE\_未定义

KSNODETYPE\_模拟\_连接器

是

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_模拟\_连接器

否

MIXERLINE\_TARGETTYPE\_WAVEIN

KSNODETYPE\_SPDIF\_INTERFACE

是

MIXERLINE\_TARGETTYPE\_WAVEOUT

KSNODETYPE\_SPDIF\_INTERFACE

否

MIXERLINE\_TARGETTYPE\_WAVEIN

 

下表显示了如何将固定输出**KS pin 类别 GUID**的映射到关联的 MIXERLINE 组件类型。

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

 

不会显示在前面的表中的所有 pin 类别，WDMAud 将都转换为与目标类型的 MIXERLINE 目标 mixer 行输出插针\_TARGETTYPE\_未定义和组件类型的 MIXERLINE\_COMPONENTTYPE\_DST\_未定义。

在前面的表中，大部分 KS 固定类别 Guid 具有 KSNODETYPE\_*Xxx*名称。 Ksmedia.h 和 Dmusprop.h 的标头文件中定义了这些名称。 (此命名约定的两个人员变动是 Guid KSCATEGORY\_音频和 PINNAME\_捕获，这也在 Ksmedia.h 中定义。)如中所述[拓扑节点](topology-nodes.md)，KSNODETYPE\_*Xxx* Guid 还可用于将 KS 指定节点类型。 大多数 KSNODETYPE\_*Xxx* Guid 指定 pin 类别或节点类型，但不是能同时指定。 例外情况是[ **KSNODETYPE\_合成器**](https://msdn.microsoft.com/library/windows/hardware/ff537203)，可以指定使用 pin 类别还是一个节点类型，具体取决于在其中的上下文。 有关一系列 KSNODETYPE\_*Xxx* Guid 表示 pin 类别，请参阅[Pin Category 属性](pin-category-property.md)。 有关一系列 KSNODETYPE\_*Xxx* Guid 表示节点类型，请参阅[音频拓扑节点](https://msdn.microsoft.com/library/windows/hardware/ff536219)。

KSCATEGORY\_音频是另一个双使用 GUID。 可用作任一**KS pin 类别 GUID**或**KS 筛选类别 GUID**，取决于上下文。 在设备安装、 音频驱动程序注册其设备接口筛选器类别 KSCATEGORY 下的\_音频。 有关详细信息，请参阅[音频适配器安装设备接口](installing-device-interfaces-for-an-audio-adapter.md)。

Pin 类别的 KSNODETYPE\_模拟\_连接器或 KSNODETYPE\_SPDIF\_接口，WDMAud 需要知道 pin 是否桥 pin 才能正确地转换固定到其 mixer 行等效项。 例如，一个 S/PDIF 插针 (与 pin 类别 KSNODETYPE\_SPDIF\_接口) 转换为在下图中所示的四个 mixer 行类型之一。 转换取决于 pin 的数据方向 （入或出） 以及它是否桥 pin （是或否），mixer 行的哪个组合在一起 yield 四个可能的类型 (在 + 是的在 + 否，out +，是的 out + 否)。 图表示中前面的表中的项的底部对，四种 mixer 行类型所示。

![说明的 s/pdif pin mixer 行转换的关系图](images/spdifpin.png)

请注意，图中的音频设备右侧的两个流的 S/PDIF 格式，在左侧的两个流的波形格式。 音频设备执行两个数字格式之间转换。

SndVol32 应用程序是混音器 API 的客户端。 API 将转换源或目标混音器行中，但在行拓扑中找到每个 pin 混音器可能不会显示在 SndVol32，识别 mixer API 该标头文件定义了 Mmsystem.h 的混音器行的组件类型的一个子集。 有关 SndVol32 详细信息，请参阅[任务栏和 SndVol32](systray-and-sndvol32.md)。

 

 




