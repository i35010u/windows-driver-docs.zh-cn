---
title: 延迟上下文中的映射
description: 延迟上下文中的映射
ms.assetid: 29c44639-ea5e-4255-8e8c-f6d5e3af0dfb
keywords:
- Direct3D 11 WDK Windows 7 显示版本，延迟的上下文映射
- Direct3D 11 WDK Windows Server 2008 R2 显示版本，延迟的上下文映射
- 延迟的上下文 WDK Windows 7 的显示器上映射
- 在延迟的上下文 WDK Windows Server 2008 R2，不包括 DDI 函数映射
- 显示延迟的上下文 WDK Windows 7，请映射
- 显示延迟的上下文 WDK Windows Server 2008 R2，请映射
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48f9aa515f6d60a1ce5681a6ab39b12c900e0890
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370129"
---
# <a name="mapping-on-deferred-contexts"></a>延迟上下文中的映射


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

在运行时可以映射动态资源 (通过在驱动程序调用[ **ResourceMap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)函数) 延迟上下文和 Direct3D 11 版 API 可确保首次使用映射的动态资源是放弃以前的内容。 最好是通过不断地使用原始的动态资源上每个弃元创建新的动态资源。 允许对延迟的上下文不会影响到最接近的时间线中的虚拟动态资源完成的操作的时间线中的虚拟动态资源执行的操作所需的此别名资源创建上下文。 请记住，延迟的上下文只要录制操作最终 actualized 到驱动程序的调用期间[ **CommandListExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)函数。 当使用动态资源、 应用程序的原始意图会保留，并写入组合 GPU 可访问的内存提供给应用程序时 (即，内存优化的一次性 CPU 上传)。

每个资源映射可以提供直接指向别名资源的指针。 推迟的上下文记录来实现这种类型的别名中没有额外的负担。 例如，推迟的上下文记录可能需要为使用别名纹理创建新视图。 所需的驱动程序别名与集成和看起来合理执行。 执行命令列表时，必须作为备份即时上下文等的动态资源的"当前"资源替换最后一个上下文的本地创建资源 （以满足映射放弃调用）。

驱动程序的调用[**资源将**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcecopy)推迟的上下文之后映射放弃调用, 和即时上下文后，必须仍支持函数以将资源复制到动态资源对驱动程序的调用[ **CommandListExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)函数，其中本地推迟的上下文资源理想情况下切换到"current"的资源的即时上下文版本。 驱动程序的调用**资源将**函数和动态资源目标不经常使用，因此您应使用写入时复制机制。 如果**资源将**调用的将影响任一动态资源映射放弃调用后推迟的上下文或保留为当前新的资源的命令列表本地资源的即时上下文应为从概念上讲分配以提供新的目标位置的副本，并必须将旧的资源复制到新的资源 (如果操作[ **ResourceCopyRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcecopyregion))。

 

 





