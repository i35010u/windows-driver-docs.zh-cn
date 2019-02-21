---
title: 在延迟上下文上的映射
description: 在延迟上下文上的映射
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
ms.openlocfilehash: 4ac25dd17ef160c9352011c6c21154f0d3791a52
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520265"
---
# <a name="mapping-on-deferred-contexts"></a>在延迟上下文上的映射


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

在运行时可以映射动态资源 (通过在驱动程序调用[ **ResourceMap** ](https://msdn.microsoft.com/library/windows/hardware/ff569492)函数) 延迟上下文和 Direct3D 11 版 API 可确保首次使用映射的动态资源是放弃以前的内容。 最好是通过不断地使用原始的动态资源上每个弃元创建新的动态资源。 允许对延迟的上下文不会影响到最接近的时间线中的虚拟动态资源完成的操作的时间线中的虚拟动态资源执行的操作所需的此别名资源创建上下文。 请记住，延迟的上下文只要录制操作最终 actualized 到驱动程序的调用期间[ **CommandListExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff539476)函数。 当使用动态资源、 应用程序的原始意图会保留，并写入组合 GPU 可访问的内存提供给应用程序时 (即，内存优化的一次性 CPU 上传)。

每个资源映射可以提供直接指向别名资源的指针。 推迟的上下文记录来实现这种类型的别名中没有额外的负担。 例如，推迟的上下文记录可能需要为使用别名纹理创建新视图。 所需的驱动程序别名与集成和看起来合理执行。 执行命令列表时，必须作为备份即时上下文等的动态资源的"当前"资源替换最后一个上下文的本地创建资源 （以满足映射放弃调用）。

驱动程序的调用[**资源将**](https://msdn.microsoft.com/library/windows/hardware/ff569489)推迟的上下文之后映射放弃调用, 和即时上下文后，必须仍支持函数以将资源复制到动态资源对驱动程序的调用[ **CommandListExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff539476)函数，其中本地推迟的上下文资源理想情况下切换到"current"的资源的即时上下文版本。 驱动程序的调用**资源将**函数和动态资源目标不经常使用，因此您应使用写入时复制机制。 如果**资源将**调用的将影响任一动态资源映射放弃调用后推迟的上下文或保留为当前新的资源的命令列表本地资源的即时上下文应为从概念上讲分配以提供新的目标位置的副本，并必须将旧的资源复制到新的资源 (如果操作[ **ResourceCopyRegion**](https://msdn.microsoft.com/library/windows/hardware/ff569490))。

 

 





