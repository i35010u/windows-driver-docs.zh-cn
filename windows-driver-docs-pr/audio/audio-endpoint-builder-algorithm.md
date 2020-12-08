---
title: 音频终结点生成器算法
description: 音频终结点生成器算法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 185ebe2b58350b160b21d5e2eceb6e78896b44bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789425"
---
# <a name="audio-endpoint-builder-algorithm"></a>音频终结点生成器算法


在 Windows Vista 和更高版本的 Windows 中，AudioEndpointBuilder 是一项系统服务，用于枚举、初始化和激活系统中的音频终结点。 本主题概述了 AudioEndpointBuilder 服务所使用的算法。

AudioEndpointBuilder 服务使用一种算法来发现和枚举终结点。 算法旨在简化系统对多路复用 (MUXed) 捕获设备的访问，并帮助处理涉及多个主机插针和/或多个桥接 pin 的拓扑。

在 Windows XP 中，音频模型使用术语 "音频设备" 引用即插即用 (PnP) 树中的概念设备。 在 Windows Vista 和更高版本的 Windows 中，音频设备的概念已经过重新设计，可以更好地表示与用户进行物理交互的设备。

使用 Windows Vista 中的两个新 Api、 [MMDEVICE API](/windows/win32/coreaudio/mmdevice-api) 和 [WASAPI](/windows/win32/coreaudio/wasapi)，你可以访问和操作这些新的音频设备。 MMDevice API 是指作为终结点的新音频设备。

AudioEndpointBuilder 服务会监视 [**KSCATEGORY \_ 音频**](../install/kscategory-audio.md) 类，寻找设备接口到达和删除。 当音频设备驱动程序注册 KSCATEGORY \_ 音频设备接口类的新实例时，AudioEndpointBuilder 服务会检测设备接口通知，并使用算法检查系统中音频设备的拓扑并采取适当的措施。

下面的列表总结了 AudioEndpointBuilder 使用的算法的工作原理：

1.  查找任何未连接的桥接 pin。

2.  为任何未连接的桥接 pin 创建终结点。 例如，当 AudioEndpointBuilder 发现带有 KSNODETYPE 扬声器的 pin 类别 GUID 的未连接桥插针时 \_ ，它将为此桥接创建一个扬声器终结点。 有关 KSNODETYPE \_ 发言人和其他 pin 类别 guid 的详细信息，请参阅 WinDDK \\ &lt; 内部版本号 &gt; \\ inc. \\ api 中的 Ksmedia。

3.  设置终结点的默认属性。 例如，AudioEndpointBuilder 设置名称、图标和外形规格。

4.  确定是否存在从终结点到主机 pin 的路径，该主机支持脉冲) 、音频编解码器 ( (E-AC3) 或 Windows media 视频 (WMV) 。 主机 pin 是 KSPIN 结构，其通信成员设置为 KSPIN \_ 通信 \_ 接收器或 KSPIN \_ 通信 \_ 。 有关 KSPIN 结构的详细信息，请参阅 [**KSPIN**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)。

5.  用音频设备接口的注册表项中的属性信息填充终结点 PropertyStore。

6.  设置终结点的状态。 终结点的状态可以是以下三个值之一：

    -   活动。 这表明路径存在，如步骤4中所述。

    -   下. 如果音频设备支持插座检测，则此状态表明终结点存在路径，并且从音频适配器上的物理连接器中拔出插孔。

    -   不存在。 此状态指示在步骤4中找不到路径，此终结点不支持插座检测。

7.  如果此终结点是在关联的 INF 文件中指定的终结点，则将此终结点设置为默认终结点。

枚举终结点后，音频系统的客户端可以使用新的 Windows Vista Api 直接对其进行操作 (如前文所述) 或使用更熟悉的 Api （例如 Wave、 [DirectShow](/windows/win32/directshow/directshow) 或 [DirectSound）。](/previous-versions/windows/desktop/bb318665(v=vs.85)) 提供了新的 API 方法，以便音频客户端可以使用终结点的 MMDevice ID 开始，并访问同一终结点的波形或 DirectSound ID。

使用终结点时，可以利用以下各项：

-   无论重新启动计算机的频率如何，相同的全局唯一 ID (GUID) 都可用。 使用此永久性 GUID 比保存终结点的 waveOut ID 或友好名称更可靠。

-   无论重新启动计算机的频率如何，都可以使用相同的 PropertyStore。 与音频设备相关的元数据保存在终结点 PropertyStore 中。

-   多路复用 (MUX) 和取消多路复用 (多路分解器) pin 由 AudioEndpointBuilder 服务自动管理和枚举。

如果您开发自己的音频设备驱动程序和 INF 文件以便使用您的音频设备，并开发音频应用程序，或同时开发这两种应用程序，则最好注意以下问题和最佳实践。 当你使用这些建议开发驱动程序和应用程序时，将生成驱动程序、INF 文件和音频客户端，以便更有效地使用 AudioEndpointBuilder。

-   命名约定。 用于终结点的命名约定基于桥接 pin 的友好名称。 但对于扬声器终结点，名称已硬编码为 "发言人"，不能被驱动程序或第三方应用程序更改。

-   不理想的拓扑。 由于 AudioEndpointBuilder 使用的算法枚举终结点，某些拓扑被视为不理想。 例如，当你创建其中一个不理想的拓扑时，你创建的主机 pin 具有隐藏的终结点，并且不能通过 AudioEndpointBuilder 或 (拆分端点查看) ，因为 AudioEndpointBuilder 无法链接到其关联的主机 pin。

    -   **隐藏的终结点**

        在下图中，KS 筛选器显示有两个主机引脚连接到一个桥接)  (扬声器。

        ![在左侧显示带有隐藏终结点的 ac 3 主机 pin 的有问题拓扑是单独的 pcm 和 ac 3] 共享单个筛选器 (映像/hidden-endpoint-bad.png) 

        当 AudioEndpointBuilder 发现此桥接程序时，它将只跟踪一个主机 pin 的路径，设置桥接 pin 的默认值，创建并激活扬声器终结点，并继续发现其他桥接。 因此，另一个主机 pin 在 AudioEndpointBuilder 中保持隐藏状态。

        ![具有主机 pin 和终结点之间的可跟踪路径的推荐拓扑](images/hidden-endpoint-good.png)

        在前面的关系图中，已重新设计了有问题的拓扑，以便 AudioEndpointBuilder 可以发现两个主机引脚 (PCM 和 AC 3/PCM) ，因为它现在可以看到两个桥接 (扬声器和 SPDIF) 。

    -   **器**

        当一台主机 pin 连接到多个桥接 pin 时，将创建另一种不太理想的拓扑。 下图显示了 PCM 主机 pin 连接到扬声器桥接 pin 的拓扑和 SPDIF 桥接 pin。

        ![出现有问题的拓扑显示两个终结点连接到单个 PCM 的主机 pin](images/splitter-bad.png)

        在这种情况下，AudioEndpointBuilder 将发现一个桥接，并将路径跟踪回 PCM 主机的 pin，设置默认值，然后创建并激活扬声器终结点。 当 AudioEndpointBuilder 发现下一个桥接 pin 时，它会将路径跟踪回同一个 PCM 主机 pin，设置默认值，然后创建并激活一个 SPDIF 终结点。 但是，尽管这两个终结点都已初始化并已激活，但流式传输到其中一个终结点使得无法同时流式传输到另一个终结点;换言之，它们是互相排斥的终结点。

        下图显示了此拓扑的重新设计，其中存在单独的连接。 这种设计使 AudioEndpointBuilder 可以针对两个桥接插回每个桥接的 PCM 主机的路径。

        ![此图说明了在主机 pin 和端点之间具有可跟踪路径的推荐拓扑，左侧有两个 Pcm](images/splitter-good.png)

-   终结点格式。 当音频引擎在共享模式下运行时，终结点的格式会假定安装时 INF 文件所指示的特定设置。 例如，音频设备的音频驱动程序使用其关联的 INF 文件将默认终结点设置为 44.1 kHz、16位、立体声 PCM 格式。 安装完成后，必须使用 "控制面板" 或第三方应用程序更改终结点格式。

-   默认设备。 在安装时，将使用 INF 文件中的信息选择设置为默认设备的终结点。 安装完成后，必须使用 "控制面板" 或第三方应用程序选择另一个终结点作为默认终结点。

**注意**   如果 INF 文件未选择在安装过程中将终结点设置为默认值，则客户端应用程序可以使用 MMDevice API 来选择终结点。 该 API 根据窗体因数排名以及终结点是呈现器还是捕获终结点来选择它。 下表显示了选择顺序。
<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">呈现排名</th>
<th align="left">捕获排名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>扬声器</p></td>
<td align="left"><p>麦克风</p></td>
</tr>
<tr class="even">
<td align="left"><p>行输出</p></td>
<td align="left"><p>行</p></td>
</tr>
<tr class="odd">
<td align="left"><p>后部</p></td>
<td align="left"><p>后部</p></td>
</tr>
</tbody>
</table>

 

 

如果使用 MMDevice API 来选择默认终结点，并且可用终结点的排名相同，则 MMDevice API 会按字母顺序排列终结点 Id，以确定选择哪个终结点作为默认终结点。 例如，如果某个音频适配器同时具有线路输出和线路输入连接器，并且关联的 INF 文件在安装时没有选择默认设置为默认值，则 MMDevice API 将标识第一个按字母顺序排列的终结点 Id 并将该连接器设置为默认值。 此选择将在您重新启动系统后保持，因为终结点 Id 是永久性的。 但是，如果 (更高排名的终结点，则所选内容不会保留（例如，具有麦克风连接器的第二个适配器) 出现在系统中。

 

