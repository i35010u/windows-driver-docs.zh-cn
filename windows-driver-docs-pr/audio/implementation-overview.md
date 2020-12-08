---
title: 实现概述
description: 本主题概述了在为能够处理硬件卸载音频流的音频适配器开发驱动程序时必须注意的实现关键点。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fca19abf18e9552b269ebbf6536fdf4aa2e519fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784767"
---
# <a name="implementation-overview"></a>实现概述


本主题概述了在为能够处理硬件卸载音频流的音频适配器开发驱动程序时必须注意的实现关键点。

## <a name="span-idthe_new_ks_filter_topologyspanspan-idthe_new_ks_filter_topologyspanspan-idthe_new_ks_filter_topologyspanthe-new-ks-filter-topology"></a><span id="The_New_KS_Filter_Topology"></span><span id="the_new_ks_filter_topology"></span><span id="THE_NEW_KS_FILTER_TOPOLOGY"></span>新的 KS 筛选器拓扑


在 Windows 8 及更高版本的操作系统中，已为一种新类型的音频适配器提供支持，可以使用板载硬件音频引擎来处理音频流。 开发此类音频适配器时，关联的音频驱动程序必须以特定方式向用户模式音频系统公开此事实，以便音频系统能够发现、使用和正确公开此适配器及其驱动程序的功能。

为了使音频驱动程序可以公开这些新音频适配器的硬件功能，Windows 8 引入了驱动程序必须使用的新的 KS 筛选器拓扑：

![新的 ks 筛选器拓扑，其中显示了主机进程输入插针、卸载的音频输入插针和环回输出插针。 音频处理适用于来自卸载的音频和主机进程 pin 的音频流。环回路径取自最终处理阶段的输出，并直接从 ks 筛选器拓扑中产生。 其他两个流流过了 dac 和 ks 筛选器拓扑。](images/audio-engine-ksftopology.png)

如上图所示，一个 KS 筛选器拓扑表示通过硬件的数据路径，并且还显示这些路径上可用的函数。 对于可以处理卸载音频的音频适配器，有以下输入和输出 (在 KS 筛选器上) 称为 pin：

-   一个主机进程 pin。 这表示从软件音频引擎到 KS 筛选器的输入。

-   一个环回 pin。 这表示硬件音频引擎到 Windows 音频会话 API (WASAPI) 层的输出。

-   许多卸载音频 pin。 尽管此图仅显示此类型的一个 pin，但 IHV 可以自由地实现任何数量 (n) 的 pin。

有关此新类型的 KS 筛选器拓扑中的 pin 的详细信息，请参阅 [体系结构概述](architectural-overview.md)。
用户模式音频系统中的实际服务（"领导" 音频适配器及其驱动程序的发现）是 AudioEndpointBuilder。 AudioEndpointBuilder 服务会监视 **KSCATEGORY \_ 音频** 类，寻找设备接口到达和删除。 当音频设备驱动程序注册 **KSCATEGORY \_ 音频** 设备接口类的新实例时，将激发设备接口到达通知。 AudioEndpointBuilder 服务检测到设备接口到达通知，并使用算法检查系统中音频设备的拓扑，使其可以采取适当的措施。

因此，当你开发音频驱动程序来支持能够处理卸载音频的适配器时，你的驱动程序必须使用新定义的 [**KSNODETYPE \_ 音频 \_ 引擎**](./ksnodetype-audio-engine.md) 音频终结点来公开硬件音频引擎的功能。 有关音频终结点发现过程的详细信息，请参阅 [音频终结点生成器算法](audio-endpoint-builder-algorithm.md)。

## <a name="span-iduser_interface_considerationsspanspan-iduser_interface_considerationsspanspan-iduser_interface_considerationsspanuser-interface-considerations"></a><span id="User_Interface_Considerations"></span><span id="user_interface_considerations"></span><span id="USER_INTERFACE_CONSIDERATIONS"></span>用户界面注意事项


开发音频驱动程序的目的是控制能够处理卸载音频的音频适配器的基本硬件功能。 这意味着，你的驱动程序具有有关如何控制适配器功能的最佳知识。 因此，你必须开发 UI，将适配器的功能以他们可以选择、启用和/或禁用的选项形式向最终用户公开。

不过，如果你已有一个用于控制音频处理对象的 UI (你开发的) ，则可以将此 UI 扩展为与新的音频适配器一起使用。 在这种情况下，对 UI 的扩展将为该适配器的 "用户" 和 "硬件控制" 提供软件控制。

## <a name="span-idapplication_impactspanspan-idapplication_impactspanspan-idapplication_impactspanapplication-impact"></a><span id="Application_Impact"></span><span id="application_impact"></span><span id="APPLICATION_IMPACT"></span>应用程序影响


UWP 应用可以通过 WASAPI、媒体基础、媒体引擎或 HTML 5 音频标记来使用此新的音频适配器类型及其关联的驱动程序所描述的功能 &lt; &gt; 。 请注意，不能使用波形和 DSound，因为它们不可用于 UWP 应用。 另请注意，桌面应用程序不能使用支持硬件卸载音频的音频适配器的卸载功能。 这些应用程序仍然可以呈现音频，但只能通过主机插针使用软件音频引擎。

如果 UWP 应用对媒体内容进行流式处理，并使用媒体基础、媒体引擎或 HTML 5 &lt; 音频 &gt; 标记，只要为流设置了正确的音频类别，就会自动为硬件卸载选择该应用。 硬件卸载的选择加入是根据每个流来完成的。

使用 WASAPI 或流式处理通信的 UWP 应用必须明确选择加入硬件卸载。

 

