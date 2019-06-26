---
title: DRM 函数和接口
description: DRM 函数和接口
ms.assetid: 62c739da-91e8-428e-b76c-ec9621b12597
keywords:
- 数字权限管理 WDK 音频，函数
- DRM WDK 音频，函数
- 数字权限管理 WDK 音频，接口
- DRM WDK 音频，接口
- 接口 WDK DRM
- WDK DRM 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07bc3ba5b2b55c9511024e43015a75310fdf5668
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360099"
---
# <a name="drm-functions-and-interfaces"></a>DRM 函数和接口


## <span id="drm_functions_and_interfaces"></span><span id="DRM_FUNCTIONS_AND_INTERFACES"></span>


系统驱动程序组件*Drmk.sys*并*Portcls.sys*实现 DRM 函数和驱动程序使用的内核流式处理音频内容的数字权限管理的接口的集合。 *Drmk.sys*组件实现了若干**DrmXxx**函数，并*Portcls.sys*实现特定于 DRM 的一系列**PcXxx**函数，并还[IDrmPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport)并[IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport2)接口。

可用以下 DRM 函数包括：

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmaddcontenthandlers)

为系统提供驱动程序界面，包含用于处理受保护的内容的函数的列表。
[**DrmCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmcreatecontentmixed)

创建一个 DRM 内容 ID 来标识包含混合的内容的几个输入流的 KS 音频流。
[**DrmDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmdestroycontent)

删除 DRM 内容 id。
[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttodeviceobject)

对驱动程序进行身份验证，并将其发送的 DRM 内容 ID 和系统已分配给包含受保护的内容的流的内容权利。
[**DrmForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttofileobject)

已过时的函数。
[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttointerface)

进行身份验证的驱动程序对象，并将其发送的 DRM 内容 ID 和系统已分配给包含受保护的内容的流的内容权利。
[**DrmGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmgetcontentrights)

检索的 DRM 内容权限的系统具有分配给 DRM 内容 id。
标头文件 Drmk.h 中声明此列表中的函数。 内核模式[DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver)，Drmk.sys，导出这些函数的入口点。

在 Windows XP 及更高版本，PortCls 系统驱动程序 Portcls.sys，将导出一组不同的相同的 DRM 函数集的入口点。 只不过它们使用前缀 Pc 而不是 Drm PortCls 函数的名称是类似于上面列表中：

[**PcAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcaddcontenthandlers)

[**PcCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pccreatecontentmixed)

[**PcDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcdestroycontent)

[**PcForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcforwardcontenttodeviceobject)

[**PcForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcforwardcontenttofileobject)

[**PcForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcforwardcontenttointerface)

[**PcGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcgetcontentrights)

标头文件 Portcls.h 中声明这些函数名称。 多个在 Drmk.sys 中调用相应的函数，则在 Portcls.sys 的入口点不执行任何操作。 只是为方便起见，提供了 PortCls 入口点，因此已连接到 Portcls.sys 的音频驱动程序不需要显式加载 Drmk.sys。

在 Windows XP 及更高版本，相同的函数集还会显示为中的方法[IDrmPort](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport)并[IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-idrmport2)接口：

[**IDrmPort2::AddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport2-addcontenthandlers)

[**IDrmPort::CreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport-createcontentmixed)

[**IDrmPort::DestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport-destroycontent)

[**IDrmPort2::ForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport2-forwardcontenttodeviceobject)

[**IDrmPort::ForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport-forwardcontenttofileobject)

[**IDrmPort::ForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport-forwardcontenttointerface)

[**IDrmPort::GetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport-getcontentrights)

**IDrmPort**并**IDrmPort2**接口在标头文件 Portcls.h 中声明并在 Portcls.sys 中实现。 多个在 Drmk.sys 中调用相应的函数，则这些方法不执行任何操作。 微型端口驱动程序将获取对的引用 **IDrmPort * * * x*通过查询此接口及其端口驱动程序的接口。使用的优点 **IDrmPort * * * x*接口而不是相应 Drm*Xxx*或 Pc*Xxx*函数是驱动程序，可以使用此查询在运行时确定的操作系统版本支持 DRM。 这简化了编写单个驱动程序可在较新版本的 Windows 支持 DRM 的和不这样做的较旧版本中运行的任务。 **IDrmPort2**派生自**IDrmPort** ，并提供两种其他方法。

WaveCyclic 和 WavePci 端口驱动程序使用[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nn-drmk-idrmaudiostream)如果相应的微型端口驱动程序支持的接口。 端口驱动程序调用[ **IDrmAudioStream::SetContentId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-idrmaudiostream-setcontentid)要分配给的音频流中的数字内容的 DRM 保护的方法。

[**定义\_DRMRIGHTS\_默认**](https://docs.microsoft.com/previous-versions/ff536254(v=vs.85))宏，标头文件 Drmk.h 中定义，初始化的成员[ **DRMRIGHTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/ns-drmk-tagdrmrights)为其默认值的结构。

 

 




