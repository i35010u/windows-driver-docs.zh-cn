---
title: 实现概述
description: 本主题是你必须是开发能够处理硬件卸载音频流的音频适配器驱动程序时考虑的实现关键点的概述。
ms.assetid: B93B9A6D-7317-482B-A0B8-298CE8F21193
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9337df0a6e845d2971a7f4ea62fe8e63d73bb619
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359946"
---
# <a name="implementation-overview"></a>实现概述


本主题是你必须是开发能够处理硬件卸载音频流的音频适配器驱动程序时考虑的实现关键点的概述。

## <a name="span-idthenewksfiltertopologyspanspan-idthenewksfiltertopologyspanspan-idthenewksfiltertopologyspanthe-new-ks-filter-topology"></a><span id="The_New_KS_Filter_Topology"></span><span id="the_new_ks_filter_topology"></span><span id="THE_NEW_KS_FILTER_TOPOLOGY"></span>在新的 KS 筛选拓扑


在 Windows 8 和更高版本操作系统中，支持提供了可使用板载硬件音频引擎处理音频流的音频适配器为新类型。 当开发这样的音频适配器时，关联的音频驱动程序必须以特定方式公开到用户模式音频系统这一事实，以便音频系统可以发现、 使用和正确公开此适配器和其驱动程序的功能。

若要使音频驱动程序来公开这些新的音频适配器的硬件功能，Windows 8 引入了新的驱动程序必须使用 KS 筛选器拓扑：

![在新 ks 筛选器的拓扑，显示在主机进程输入插针、 卸载音频输入插针和环回输出插针。 音频处理从卸载音频应用到音频流和主机进程 pins.the 环回路径的最后一个处理阶段的输出中获取并直接从 ks 筛选器拓扑的潜在顾客。 其他两种流式处理通过 dac 和流出 ks 筛选器拓扑。](images/audio-engine-ksftopology.png)

您可以看到在上图中，KS 筛选器拓扑表示通过硬件使用的数据路径，并还显示了这些路径可用的函数。 对于可以处理卸载的音频的音频适配器，有以下输入和输出 （称为插针） KS 筛选器：

-   一个主机进程插针。 这表示软件音频引擎到 KS 筛选器的输入。

-   一个 Loopback 插针。 这表示从硬件音频引擎 Windows 音频会话 API （wasapi 就可以了） 层到一个输出。

-   Offloaded 音频的 pin 数。 尽管图显示了此类型的一个 pin，IHV 可以自由地实现任意数量 (n) 的 pin。

有关此新类型的筛选器的 KS 拓扑中的 pin 的详细信息，请参阅[体系结构概述](architectural-overview.md)。
"会导致"发现音频适配器及其驱动程序的用户模式音频系统中的实际服务是 AudioEndpointBuilder。 AudioEndpointBuilder 服务监视器**KSCATEGORY\_音频**设备接口到达和删除的类。 音频设备驱动程序时注册的新实例**KSCATEGORY\_音频**设备接口类设备接口到达通知触发。 AudioEndpointBuilder 服务将检测设备接口到达通知并会使用一种算法，以便它可以采取相应的操作在系统中检查的音频设备的拓扑。

因此，您的驱动程序开发时音频驱动程序以支持可以处理卸载音频的适配器，必须使用新定义[ **KSNODETYPE\_音频\_引擎**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-engine)音频终结点公开硬件音频引擎的功能。 有关音频终结点发现过程的详细信息，请参阅[音频终结点生成器算法](audio-endpoint-builder-algorithm.md)。

## <a name="span-iduserinterfaceconsiderationsspanspan-iduserinterfaceconsiderationsspanspan-iduserinterfaceconsiderationsspanuser-interface-considerations"></a><span id="User_Interface_Considerations"></span><span id="user_interface_considerations"></span><span id="USER_INTERFACE_CONSIDERATIONS"></span>用户界面的注意事项


开发音频驱动程序来控制能够处理卸载音频的音频适配器的基础硬件功能。 这意味着您的驱动程序具有有关如何控制适配器的功能的最好的知识。 因此必须开发一个用户界面，将公开给最终用户在窗体的选项，他们可以选择、 启用和/或禁用适配器的功能。

但是，您已经有一个用户界面，用于控制音频处理对象 (Apo) 开发的如果无法扩展此 UI，可以使用新的音频适配器。 在这种情况下，你的扩展 ui 将提供软件控制的软和硬件控制适配器。

## <a name="span-idapplicationimpactspanspan-idapplicationimpactspanspan-idapplicationimpactspanapplication-impact"></a><span id="Application_Impact"></span><span id="application_impact"></span><span id="APPLICATION_IMPACT"></span>应用程序的影响


此新类型的音频适配器和其关联的驱动程序，所述的功能可由通过 wasapi 就可以了，Media Foundation、 媒体引擎或 HTML 5 的 UWP 应用&lt;音频&gt;标记。 请注意，不能使用批和 DSound，因为它们不是适用于 UWP 应用。 另请注意，桌面应用程序不能使用支持硬件卸载音频的音频适配器的卸载功能。 这些应用程序仍可以呈现音频，但只能通过该协议使用软件音频引擎主机 pin。

如果 UWP 应用流式传输媒体内容，并使用媒体基础、 媒体引擎或 HTML 5&lt;音频&gt;标记，该应用是自动选择的项硬件卸载，只要正确音频类别已设置为的流。 在选择加入的硬件在每个流的基础上完成卸载。

使用 wasapi 就可以了或流式处理通信的 UWP 应用程序必须显式选择加入的硬件卸载。

 

 




