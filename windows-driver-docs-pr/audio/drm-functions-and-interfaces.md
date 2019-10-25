---
title: DRM 函数和接口
description: DRM 函数和接口
ms.assetid: 62c739da-91e8-428e-b76c-ec9621b12597
keywords:
- 数字 Rights Management WDK 音频、功能
- DRM WDK 音频，函数
- 数字 Rights Management WDK 音频，接口
- DRM WDK 音频，接口
- 接口 WDK DRM
- 函数 WDK DRM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 627e3a0fd72b8a0a06608bc5600cecc7cb8a0e48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833794"
---
# <a name="drm-functions-and-interfaces"></a>DRM 函数和接口


## <span id="drm_functions_and_interfaces"></span><span id="DRM_FUNCTIONS_AND_INTERFACES"></span>


系统驱动程序组件*Drmk*和*Portcls*实现一系列 DRM 函数和接口，驱动程序使用该集合来管理内核流式传输音频内容的数字版权。 *Drmk*组件实现了许多**DrmXxx**函数， *PORTCLS*实现了特定于 DRM 的一组**PcXxx**函数，同时还实现了[IDrmPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)和[IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2)接口。

以下 DRM 函数可用：

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmaddcontenthandlers)

为系统提供驱动程序接口，该接口由用于处理受保护内容的函数列表组成。
[**DrmCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmcreatecontentmixed)

创建 DRM 内容 ID 以标识包含多个输入流中的混合内容的 KS 音频流。
[**DrmDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmdestroycontent)

删除 DRM 内容 ID。
[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttodeviceobject)

对驱动程序进行身份验证，并向其发送系统已分配到包含受保护内容的流的 DRM 内容 ID 和内容权限。
[**DrmForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttofileobject)

过时的函数。
[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttointerface)

对驱动程序对象进行身份验证，并向其发送系统已分配到包含受保护内容的流的 DRM 内容 ID 和内容权限。
[**DrmGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmgetcontentrights)

检索系统分配给 DRM 内容 ID 的 DRM 内容权限。
此列表中的函数在头文件 Drmk 中声明。 内核模式[DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver)DRMK 将导出这些函数的入口点。

在 Windows XP 和更高版本中，PortCls 系统驱动程序 Portcls 为同一组 DRM 函数导出一组不同的入口点。 PortCls 函数的名称类似于前面列表中的函数名称，不同之处在于它们使用前缀 Pc 而不是 Drm：

[**PcAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddcontenthandlers)

[**PcCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccreatecontentmixed)

[**PcDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdestroycontent)

[**PcForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttodeviceobject)

[**PcForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttofileobject)

[**PcForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttointerface)

[**PcGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetcontentrights)

这些函数名在头文件 Portcls 中声明。 Portcls 中的入口点除了调用 Drmk 中的相应函数外，不执行任何操作。 提供 PortCls 入口点只是为了方便，因此已连接到 Portcls 的音频驱动程序无需显式加载 Drmk。

在 Windows XP 和更高版本中，同一组函数也作为[IDrmPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)和[IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2)接口中的方法公开：

[**IDrmPort2::AddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport2-addcontenthandlers)

[**IDrmPort::CreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-createcontentmixed)

[**IDrmPort：:D estroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-destroycontent)

[**IDrmPort2::ForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport2-forwardcontenttodeviceobject)

[**IDrmPort::ForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-forwardcontenttofileobject)

[**IDrmPort::ForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-forwardcontenttointerface)

[**IDrmPort::GetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-getcontentrights)

**IDrmPort**和**IDrmPort2**接口在头文件 Portcls 中声明，并在 Portcls 中实现。 这些方法只是在 Drmk 中调用相应的函数。 微型端口驱动程序*通过查询该接口的端口驱动程序，获取对*IDrmPort * * * x*接口的引用。使用 **IDrmPort * * * x*接口而不是相应 Drm*xxx*或 Pc*xxx*函数的优点在于，驱动程序可以使用此查询在运行时确定操作系统版本是否支持 Drm。 这简化了撰写单个驱动程序的任务，该驱动程序可以在支持 DRM 的较新版本的 Windows 中运行，也可以在不支持 DRM 的旧版本中运行。 **IDrmPort2**派生自**IDrmPort** ，提供两个附加方法。

WaveCyclic 和 WavePci 端口驱动程序将使用[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)接口（如果相应的微型端口驱动程序支持它）。 端口驱动程序调用[**IDrmAudioStream：： SetContentId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-idrmaudiostream-setcontentid)方法将 DRM 保护分配给音频流中的数字内容。

"[**定义\_DRMRIGHTS\_" 默认**](https://docs.microsoft.com/previous-versions/ff536254(v=vs.85))"宏（在头文件 Drmk 中定义）将[**DRMRIGHTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights)结构的成员初始化为其默认值。

 

 




