---
title: 转发 DRM 内容 Id
description: 转发 DRM 内容 Id
ms.assetid: 62bcc44f-303a-4e72-8140-4b9bee59c252
keywords:
- 数字权限管理 WDK 音频、 安全的数据路径
- DRM WDK 音频、 安全的数据路径
- 内容 Id WDK 音频
- 标识符 WDK 音频
- 转发内容 Id
- 译码内容 WDK 音频
- 数字权限管理 WDK 音频，则内容 Id
- DRM WDK 音频，则内容 Id
- 将数字转换为模拟
- 进行身份验证 DRM 内容 Id WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 327c4b69ffb80849e4f7ecd28a68ad7ad91019a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546388"
---
# <a name="forwarding-drm-content-ids"></a>转发 DRM 内容 Id


## <span id="forwarding_drm_content_ids"></span><span id="FORWARDING_DRM_CONTENT_IDS"></span>


[DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver)对进行译码包含受保护的内容的音频播放流。 DRMK 实现采用包含经过编码的数据的输入的流时，对其进行译码并被破解的流馈送到数据路径中包含的一定数量的驻留在内核中的模块的 KS 筛选器。 这些模块可以是 KS 筛选器或其他类型的驱动程序。 将数字内容转换为模拟信号可以通过扬声器播放的音频呈现设备中通常结束的数据路径。

允许要输入的数据路径的被破解的内容之前, DRMK 验证的数据路径安全。 为此，请 DRMK 进行身份验证数据路径中的每个模块从上游数据路径末尾处的模块开始，然后将移动到的数据路径的另一端的下游。 下图说明了此过程。

![说明安全数据路径的关系图](images/securepath.png)

在上图中，实线箭头表示数据路径和虚线的箭头表示必须验证数据路径是安全的通信。 仅 DRMK 完成对所有在该路径中的模块进行身份验证后，被破解的数据输入的路径。

DRMK 进行身份验证的每个模块后，该模块提供 DRMK 有关信息的数据路径中的下一个模块，以便它可以也进行身份验证。 每个模块是通过身份验证后，它将接收的 DRM 内容 ID，用于标识该流。

从上游的安全数据路径结束时，DRMK 将转发到模块的又将转发到模块 B.的内容 ID 的内容 ID此过程持续的内容 ID 转发到模块 Z，安全的数据路径中的最后一个模块。

下图显示一对相邻的模块中的数据路径。

![说明转发内容 id 的关系图](images/forwardid.png)

在上游端模块调用下列任一[DRM 函数](https://msdn.microsoft.com/library/windows/hardware/ff536356)DRMK 提供有关下游模块的信息，并将转发的内容 ID 到该模块：

[**DrmForwardContentToDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff536351)

[**DrmForwardContentToInterface**](https://msdn.microsoft.com/library/windows/hardware/ff536353)

[**DrmAddContentHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff536347)

每个"转发"函数提供 DRMK 使用 DRM 内容 ID，用于标识受保护的流和 DRMK 需要进行身份验证的下游模块的信息。 其中的这三个函数调用的选择取决于两个相邻模块用来相互通信，因为它们管理的受保护的内容传输接口的类型：

1.  如果上游模块调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)以与下游模块进行通信，下游模块是 WDM 驱动程序的一部分。 在这种情况下，上游模块调用**DrmForwardContentToDeviceObject** DRMK 提供表示下游模块的设备对象。 DRMK 使用的设备对象进行身份验证的下游模块。

2.  如果两个模块通信通过 COM 接口的下游模块实现，调用上游模块**DrmForwardContentToInterface**。 此调用为 DRMK 提供了指向下游模块的 COM 接口的指针。 仅调用 DRMK **IUnknown**此接口中的方法并不会假设即将其他方法，尽管本身的两个模块必须同意这些方法执行的操作。 DRMK 验证接口中的每个方法的入口点属于已经过身份验证模块。 如果入口点分布在多个模块之间，DRMK 进行身份验证的所有这些模块。

3.  如果两个模块使用都不是 COM 接口和**IoCallDriver**函数进行通信、 上游模块调用**DrmAddContentHandlers** DRMK 提供入口点的"内容列表处理程序"，在下游模块中实现。 DRMK 不调用内容处理程序，并且不会假设有关函数执行。 DRMK，但是，进行身份验证模块 （或模块） 的入口点也位于。

在进行身份验证后下游模块需要以下信息：

-   标识包含受保护的内容的流的 DRM 内容 ID。 模块需要此 ID，下游，通知的任何模块，进一步 DRMK 它计划要发送受保护的内容。

-   受保护的内容与关联的 DRM 内容权限。 模块需要内容的权限，才能强制实施适当的安全级别。

三个转发函数的每个略有不同的方式提供此信息的模块：

1.  **DrmForwardContentToDeviceObject**函数发送[ **KSPROPERTY\_DRMAUDIOSTREAM\_CONTENTID** ](https://msdn.microsoft.com/library/windows/hardware/ff537351)集属性请求到下游模块的设备对象。 此请求将转发的流内容 ID 和对下游模块内容的权限。

2.  **DrmForwardContentToInterface**函数将查询的下游模块的 COM 接口[IDrmAudioStream](https://msdn.microsoft.com/library/windows/hardware/ff536568)接口。 如果查询成功，则函数调用[ **IDrmAudioStream::SetContentId** ](https://msdn.microsoft.com/library/windows/hardware/ff536570)方法以将内容 ID 和内容权限的下游模块转发。

3.  情况下**DrmAddContentHandlers**函数，调用方 （上游模块） 是负责转发的流内容 ID 和对下游模块内容的权限。 一次**DrmAddContentHandlers**与下游模块已经过身份验证、 上游模块会将内容 ID 和到下游的模块的内容权利传递通过调用之一，该值指示一个成功代码返回其内容处理程序。

如果上游模块 WaveCyclic 或 WavePci 微型端口驱动程序，它可以调用相应 DRM 函数间接通过以下方法之一：

[**IDrmPort2::ForwardContentToDeviceObject**](https://msdn.microsoft.com/library/windows/hardware/ff536579)

[**IDrmPort::ForwardContentToInterface**](https://msdn.microsoft.com/library/windows/hardware/ff536586)

[**IDrmPort2::AddContentHandlers**](https://msdn.microsoft.com/library/windows/hardware/ff536575)

有关详细信息，请参阅[DRM 函数](https://msdn.microsoft.com/library/windows/hardware/ff536356)。

为简单起见，上述讨论假设数据路径中的每个模块接受来自单个源的流，并将转发到最多一个下游模块该流。 实际上，模块可以转发到两个或多个下游模块的流，但它必须首先进行身份验证的每个下游模块通过调用三个转发函数之一。 同样，模块可以混合在一起的几个输入的流，但它必须遵守的输入流内容的权限，通过提供适当级别的保护混合的输出流。 有关详细信息，请参阅的讨论[ **DrmCreateContentMixed** ](https://msdn.microsoft.com/library/windows/hardware/ff536348)函数，在[内容 Id 和内容的权限](content-ids-and-content-rights.md)。

典型的安全数据路径组成[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)跟表示音频渲染设备的批筛选器。 筛选器作为 WaveCyclic 或 WavePci 微型端口驱动程序结合了相应的端口驱动程序实现。 若要验证的数据路径安全，DRMK KMixer，又将转发到筛选器的内容 ID 到将转发的内容 ID。 端口驱动程序，可以实现普通筛选器功能，接收的内容 ID，并将其转发给微型端口驱动程序。 具体而言，端口驱动程序调用**DrmForwardContentToInterface**函数将转发到的流对象实例化微型端口驱动程序来表示批输出插针音频呈现设备上的内容 ID. 对于此调用是指向流对象的其中一个参数的值[IMiniportWaveCyclicStream](https://msdn.microsoft.com/library/windows/hardware/ff536715)或[IMiniportWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536725)接口。 通过此接口，该函数将查询的流对象及其**IDrmAudioStream**接口，并调用该接口**SetContentId**方法。

有关详细信息，请参阅的实现**SetContentId** sb16 和 msvad 示例驱动程序中 Microsoft Windows Driver Kit (WDK) 中的方法。

 

 




