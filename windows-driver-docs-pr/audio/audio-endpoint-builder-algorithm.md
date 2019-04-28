---
title: 音频终结点生成器算法
description: 音频终结点生成器算法
ms.assetid: 2338bca7-5743-42c3-9baf-ac4a54cf0393
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aac4c8b70594f341c51b2109aa17e185c59d3ec7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331514"
---
# <a name="audio-endpoint-builder-algorithm"></a>音频终结点生成器算法


在 Windows Vista 和更高版本的 Windows，AudioEndpointBuilder 是枚举，初始化，并在系统中激活的音频的终结点的系统服务。 本主题概述 AudioEndpointBuilder 服务使用的算法。

AudioEndpointBuilder 服务使用算法来发现和枚举终结点。 该算法旨在简化多路复用 (MUXed) 捕获设备以及帮助使用的拓扑中涉及多个主机插针和多个桥 pin，或两者的系统访问权限。

在 Windows XP 中，音频模型使用的术语音频设备来指代概念在插树中 (PnP) 设备。 在 Windows Vista 和更高版本的 Windows 中，将音频设备概念经过重新设计，更好地表示用户以物理方式与之交互的设备。

使用在 Windows Vista 中，两个新的 Api [MMDevice API](https://go.microsoft.com/fwlink/p/?linkid=130863)并[wasapi 就可以了](https://go.microsoft.com/fwlink/p/?linkid=130864)，可以访问和处理这些新的音频设备。 MMDevice API 将新的音频设备称为终结点。

AudioEndpointBuilder 服务监视器[ **KSCATEGORY\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff548261)设备接口到达和删除的类。 音频设备驱动程序时注册的新实例 KSCATEGORY\_音频设备界面类，AudioEndpointBuilder 服务检测到设备接口通知，以及使用算法来检查中的音频设备的拓扑系统并采取相应操作。

以下列表总结了由 AudioEndpointBuilder 算法的工作方式：

1.  查找未连接的桥销。

2.  创建未连接的桥销的终结点。 例如，当 AudioEndpointBuilder 查找未连接的桥 pin 与 pin 类别 GUID 的 KSNODETYPE\_演讲者，它会创建此桥 pin 的演讲者终结点。 详细了解 KSNODETYPE\_演讲者和其他 pin 类别 GUID，请参阅在 WinDDK Ksmedia.h\\&lt;生成号&gt;\\inc\\api。

3.  设置终结点的默认属性。 例如，AudioEndpointBuilder 设置名称、 图标和外形规格。

4.  确定是否支持脉冲编码调制 (PCM) 的主机 pin 从终结点的路径，则为音频编解码器-3 (AC3) 或 Windows media 视频 (WMV)。 主机 pin 是一种 KSPIN 结构通过其通信成员设置为 KSPIN\_通信\_接收器或 KSPIN\_通信\_两者。 KSPIN 结构的详细信息，请参阅[ **KSPIN**](https://msdn.microsoft.com/library/windows/hardware/ff563483)。

5.  填充属性中的信息的注册表项的音频设备接口的终结点 PropertyStore。

6.  设置终结点的状态。 终结点的状态可以是以下三个值之一：

    -   活动。 这表示路径存在在步骤 4 中所述。

    -   拔出。 如果音频设备支持 jack 检测，此状态指示路径存在终结点，并且是 jack 是从音频适配器上的物理连接器拔出。

    -   不存在。 此状态指示在步骤 4 中找不到路径，此终结点不支持 jack 检测。

7.  如果关联的 INF 文件中指定的内容，请将此终结点设置为默认终结点。

终结点之后，客户端的音频系统操作它们使用新的 Windows Vista Api （如先前所示） 来直接或间接批，如使用更熟悉的 Api [DShow](https://go.microsoft.com/fwlink/p/?linkid=130871)或[DirectSound。](https://go.microsoft.com/fwlink/p/?linkid=130872) 提供了新的 API 方法，这样音频客户端可以启动与终结点的 MMDevice ID 和访问的同一个终结点批或 DirectSound ID。

当您使用的终结点时，可以享受以下好处：

-   无论何种频率重新启动你的计算机提供同一个全局唯一 ID (GUID)。 拥有此永久性 GUID 是比保存 waveOut ID 或终结点的友好名称更可靠。

-   同一 PropertyStore 是无论何种频率重新启动计算机。 音频设备有关的元数据保存在 PropertyStore 的终结点。

-   多路复用 (MUX) 和取消多路复用 （多路分解器） pin 自动管理，并枚举 AudioEndpointBuilder 服务。

如果您开发自己的音频设备驱动程序和要处理您的音频设备，并制订和 / 或音频的应用程序的 INF 文件，最好要注意以下问题和最佳做法。 在开发驱动程序和应用程序使用记住这些建议时，会构建驱动程序、 INF 文件和更有效地处理 AudioEndpointBuilder 的音频客户端。

-   命名约定。 对终结点使用的命名约定基于桥 pin 的友好名称。 但是，在演讲者终结点的情况下名称已被硬编码为"发言人"，并且您的驱动程序或第三方应用程序不能更改。

-   非最优拓扑。 某些拓扑被视为由于 AudioEndpointBuilder 用于枚举终结点的算法而不是最佳。 例如，在创建这些非最优拓扑时，您将创建具有隐藏终结点，并且无法查看的 AudioEndpointBuilder 或 AudioEndpointBuilder 不能链接到其关联的主机的 pin 的拆分 （拆分终结点） 的主机 pin。

    -   **隐藏的终结点**

        在下图中，KS 筛选器显示具有两个连接到单个桥 pin （演讲者） 的主机 pin。

        ![说明有问题的拓扑显示 ac-3 主机 pin 与隐藏的终结点的关系图](images/hidden-endpoint-bad.png)

        当 AudioEndpointBuilder 发现此桥 pin 时，它跟踪返回到主机引脚之一的路径、 设置桥 pin 的默认值、 创建和激活演讲者的终结点，并发现其他桥 pin 将继续。 因此，其他主机 pin 保持从 AudioEndpointBuilder 隐藏状态。

        ![说明与主机的 pin 和终结点之间的可跟踪路径建议的拓扑结构的关系图](images/hidden-endpoint-good.png)

        在上图中，有问题的拓扑进行了重新设计，使 AudioEndpointBuilder 可发现的两个主机的 pin (PCM 并 ac-3 / PCM) 因为它现在可以看到两个桥 pin （演讲者和 SPDIF）。

    -   **拆分器**

        一个主机插针连接到多个桥 pin 时，创建另一种类型的非最优的拓扑。 下图显示了在其中 PCM 主机 pin 将连接到扬声器桥 pin 和 SPDIF 桥 pin 的拓扑。

        ![连接到一台主机 pin 的说明有问题的拓扑显示两个终结点的关系图](images/splitter-bad.png)

        在这种情况下 AudioEndpointBuilder 发现一个桥插针和跟踪返回到 PCM 主机 pin 的路径、 设置默认值，创建并激活一个演讲者终结点。 时 AudioEndpointBuilder 可发现下一步的桥 pin，它跟踪返回到相同的 PCM 主机 pin 的路径、 设置默认值，然后创建并激活 SPDIF 终结点。 但是，尽管这两个终结点已初始化并激活，流式传输到其中一个就不可能到流到另一次;换而言之，它们是互斥的终结点。

        下图显示了重新设计的此拓扑中存在单独的连接。 这种设计使 AudioEndpointBuilder 来跟踪两个桥 pin 的每个 PCM 主机 pin 返回到的路径。

        ![说明与主机的 pin 和终结点之间的可跟踪路径建议的拓扑结构的关系图](images/splitter-good.png)

-   终结点的格式。 时音频引擎运行在共享模式下，终结点的格式将假定特定设置，在安装时的指导下 INF 文件。 例如，音频设备的音频驱动程序使用其关联的 INF 文件为 44.1 kHz、 16 位立体声 PCM 格式设置的默认终结点。 安装完成后，必须使用控制面板或第三方应用程序终结点格式更改。

-   默认设备。 设置为默认设备的终结点是在安装时选择使用 INF 文件中的信息。 安装完成后，必须使用控制面板或第三方应用程序选择另一个终结点为默认终结点。

**请注意**   INF 文件不会选择终结点以在安装过程中设置为默认值，如果客户端应用程序可以使用 MMDevice API 以选择一个终结点。 API 将基于窗体因素排名和终结点是否呈现或捕获终结点访问其所选内容。 下表显示了选择顺序。
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
<td align="left"><p>行扩展</p></td>
<td align="left"><p>行中</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SPDIF</p></td>
<td align="left"><p>SPDIF</p></td>
</tr>
</tbody>
</table>

 

 

如果您使用 MMDevice API 选择默认终结点和可用的终结点进行排名相同，MMDevice API 将按字母顺序的终结点 Id 来确定哪些终结点，以选择为默认值。 例如，如果音频适配器具有行外和行中连接器和相关联的 INF 文件不会选择要在安装时默认两者中任何一个，MMDevice API 标识哪些终结点 Id 是第一个按字母排序并将其设置连接器作为默认值。 因为终结点 Id 是持久的重新启动系统后，仍存在此选择。 但是，如果出现在系统中更高级别的终结点 （例如，具有麦克风连接器的第二个适配器），也不会保留所选内容。

 

 




