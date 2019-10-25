---
title: 转发 DRM 内容 ID
description: 转发 DRM 内容 ID
ms.assetid: 62bcc44f-303a-4e72-8140-4b9bee59c252
keywords:
- 数字 Rights Management WDK 音频，安全数据路径
- DRM WDK 音频，安全数据路径
- 内容 Id WDK 音频
- 标识符 WDK 音频
- 转发内容 Id
- unscrambling 内容 WDK 音频
- 数字 Rights Management WDK 音频，内容 Id
- DRM WDK 音频，内容 Id
- 将数字转换为模拟
- 对 DRM 内容 Id 进行身份验证 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dab7a390a87f0071113b3075298b627f500d690
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833384"
---
# <a name="forwarding-drm-content-ids"></a>转发 DRM 内容 ID


## <span id="forwarding_drm_content_ids"></span><span id="FORWARDING_DRM_CONTENT_IDS"></span>


[DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver)unscrambles 音频播放流，其中包含受保护的内容。 DRMK 实现了一个 KS 筛选器，该筛选器采用包含经过编码的数据（unscrambles）的输入流，并将 unscrambled 流馈送到由一些内核驻留模块组成的数据路径中。 这些模块可以是 KS 筛选器或其他类型的驱动程序。 数据路径通常以音频呈现设备结束，该设备将数字内容转换为可通过扬声器播放的模拟信号。

在允许 unscrambled 内容输入数据路径之前，DRMK 会验证数据路径是否安全。 为此，DRMK 将对数据路径中的每个模块进行身份验证，从数据路径上游端的模块开始，并向数据路径的另一端移动。 下图说明了此过程。

![说明安全数据路径的关系图](images/securepath.png)

在上图中，实心箭头表示数据路径，虚线箭头表示验证数据路径是否安全所需的通信。 仅当 DRMK 对该路径中的所有模块完成身份验证后，unscrambled 数据才会进入该路径。

DRMK 对每个模块进行身份验证后，该模块会向 DRMK 提供有关数据路径中下一个模块的信息，以便还可以对其进行身份验证。 在对每个模块进行身份验证时，它将接收标识该流的 DRM 内容 ID。

从安全数据路径的上游端开始，DRMK 将内容 ID 转发给模块 A，后者又将内容 ID 转发给模块 B。此过程将一直继续，直到将内容 ID 转发到模块 Z，即安全数据路径中的最后一个模块。

下图显示了数据路径中的相邻模块对。

![说明转发内容 id 的关系图](images/forwardid.png)

上游端的模块调用以下[DRM 函数](https://docs.microsoft.com/windows-hardware/drivers/audio/drm-functions)之一，为 DRMK 提供有关下游模块的信息并将内容 ID 转发到该模块：

[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttodeviceobject)

[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttointerface)

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmaddcontenthandlers)

其中每个 "转发" 函数都向 DRMK 提供 DRM 内容 ID，该 ID 用于标识受保护的流，以及 DRMK 需要对下游模块进行身份验证的信息。 选择这三个函数中的哪一个取决于在管理受保护内容传输时，两个相邻模块用于彼此通信的接口类型：

1.  如果上游模块调用[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)来与下游模块通信，则下游模块是 WDM 驱动程序的一部分。 在这种情况下，上游模块调用**DrmForwardContentToDeviceObject**为 DRMK 提供表示下游模块的设备对象。 DRMK 使用设备对象对下游模块进行身份验证。

2.  如果这两个模块通过下游模块实现的 COM 接口进行通信，则上游模块将调用**DrmForwardContentToInterface**。 此调用为 DRMK 提供指向下游模块的 COM 接口的指针。 DRMK 只调用此接口中的**IUnknown**方法，并不对其他方法进行任何假设，尽管这两个模块本身必须同意这些方法的作用。 DRMK 验证接口中每个方法的入口点是否属于已经过身份验证的模块。 如果入口点分布在多个模块中，DRMK 将对所有这些模块进行身份验证。

3.  如果这两个模块既不使用 COM 接口，也不使用**IoCallDriver**函数进行通信，则上游模块会调用**DRMADDCONTENTHANDLERS**来向 DRMK 提供在下游模块。 DRMK 不会调用内容处理程序，也不会对其执行的函数进行假设。 不过，DRMK 将对入口点所在的模块（或模块）进行身份验证。

经过身份验证后，下游模块需要以下信息：

-   用于标识包含受保护内容的流的 DRM 内容 ID。 此模块需要此 ID 来通知 DRMK 要向其发送受保护内容的任何模块。

-   与受保护的内容关联的 DRM 内容权限。 此模块需要内容权限才能强制实施适当的安全级别。

这三个转发函数中的每一个都以略有不同的方式向模块提供此信息：

1.  **DrmForwardContentToDeviceObject**函数将[**KSPROPERTY\_DRMAUDIOSTREAM\_id 为**](https://docs.microsoft.com/previous-versions/ff537351(v=vs.85))设置-属性请求发送到下游模块的设备对象。 此请求将流的内容 ID 和内容权限转发到下游模块。

2.  **DrmForwardContentToInterface**函数在下游模块的 COM 接口上查询[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)接口。 如果查询成功，则该函数将调用[**IDrmAudioStream：： SetContentId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-idrmaudiostream-setcontentid)方法将内容 ID 和内容权限转发到下游模块。

3.  对于**DrmAddContentHandlers**函数，调用方（上游模块）负责将流的内容 ID 和内容权限转发到下游模块。 **DrmAddContentHandlers**返回后，如果成功代码指示下游模块已通过身份验证，则上游模块会通过调用其内容处理程序之一向下游模块传递内容 ID 和内容权限。

如果上游模块是 WaveCyclic 或 WavePci 微型端口驱动程序，则它可以通过以下方法之一间接调用适当的 DRM 函数：

[**IDrmPort2::ForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport2-forwardcontenttodeviceobject)

[**IDrmPort::ForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-forwardcontenttointerface)

[**IDrmPort2::AddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport2-addcontenthandlers)

有关详细信息，请参阅[DRM 函数](https://docs.microsoft.com/windows-hardware/drivers/audio/drm-functions)。

为简单起见，上述讨论假定数据路径中的每个模块都接受来自单个源的流，并将该流转发到最多一个下游模块。 事实上，模块可以将流转发到两个或更多下游模块，但必须首先通过调用三个转发函数之一来对每个下游模块进行身份验证。 同样，模块可以将多个输入流组合在一起，但它必须遵循输入流的内容权限，方法是向混合输出流提供适当的保护级别。 有关详细信息，请参阅[内容 id 和内容权限](content-ids-and-content-rights.md)中的[**DrmCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmcreatecontentmixed)函数讨论。

典型的安全数据路径包含[KMixer 系统驱动程序](kernel-mode-wdm-audio-components.md#kmixer_system_driver)，后跟一个表示音频呈现设备的波形筛选器。 筛选器将作为 WaveCyclic 或 WavePci 微型端口驱动程序与相应的端口驱动程序一起实现。 若要验证数据路径是否安全，DRMK 将内容 ID 转发给 KMixer，后者又将内容 ID 转发给筛选器。 用于实现通用筛选器功能的端口驱动程序接收内容 ID 并将其转发到微型端口驱动程序。 具体而言，端口驱动程序会调用**DrmForwardContentToInterface**函数，以将内容 ID 转发给微型端口驱动程序已经实例化的流对象，以表示音频呈现设备上的波形输出插针。 此调用的参数值之一是指向流对象的[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)或[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)接口的指针。 通过此接口，函数将为其**IDrmAudioStream**接口查询流对象，并调用该接口的**SetContentId**方法。

有关详细信息，请参阅 Microsoft Windows 驱动程序工具包（WDK）中的 sb16 和 msvad 示例驱动程序中的**SetContentId**方法的实现。

 

 




