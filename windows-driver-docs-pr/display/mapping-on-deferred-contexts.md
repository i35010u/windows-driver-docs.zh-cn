---
title: 延迟上下文中的映射
description: 延迟上下文中的映射
ms.assetid: 29c44639-ea5e-4255-8e8c-f6d5e3af0dfb
keywords:
- Direct3D 版本 11 WDK Windows 7 显示，延迟上下文，映射
- Direct3D 版本 11 WDK Windows Server 2008 R2 显示，延迟上下文，映射
- 延迟上下文中的映射 WDK Windows 7 显示
- 延迟上下文中的映射 WDK Windows Server 2008 R2 显示，不包括 DDI 函数
- 延迟的上下文 WDK Windows 7 显示，映射
- 延迟的上下文 WDK Windows Server 2008 R2 显示，映射
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d4476c6c8e3be137235a0b949a0c4a9132ac35
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840577"
---
# <a name="mapping-on-deferred-contexts"></a>延迟上下文中的映射


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

运行时可以在延迟的上下文中映射动态资源（通过对驱动程序的[**windows.applicationmodel.resources.core.resourcemap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcemap)函数的调用），因为 Direct3D 版本 11 API 可确保第一次使用映射的动态资源来丢弃以前的内容。 最佳选择是在每次使用原始动态资源的情况中，在每次丢弃时创建新的动态资源。 必须创建此别名资源，才能允许在延迟上下文的时间线中对虚拟动态资源执行的操作，而不会影响在即时时间线中对虚拟动态资源执行的操作。快捷. 请记住，延迟的上下文只是记录在调用驱动程序的[**CommandListExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)函数期间最终 actualized 的操作。 使用动态资源时，将保留应用程序的原始意图，并向应用程序提供写入和 GPU 可访问的内存（也就是说，内存针对单使用 CPU 上传进行了优化）。

每个资源映射可以直接向别名资源提供指针。 实现此类型的别名需要额外负担延迟的上下文记录。 例如，延迟的上下文记录可能需要为有别名的纹理创建新视图。 需要与驱动程序别名集成，这似乎变得合理。 执行命令列表时，最后一个上下文本地创建的资源（用于满足映射丢弃调用）必须被替换为 "当前" 资源，该资源将为即时上下文支持动态资源，依此类推。

对驱动程序的[**ResourceCopy**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcecopy)函数的调用，若要将资源复制到动态资源，还必须同时在延迟的上下文、映射丢弃调用之后以及在调用驱动程序的[**CommandListExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11ddi_commandlistexecute)之后的即时上下文中同时受到支持。函数，其中本地延迟的上下文资源理想情况下交换为 "当前" 资源的直接上下文版本。 不经常使用对包含动态资源目标的驱动程序的**ResourceCopy**函数的调用，因此应使用写入时复制机制。 如果调用**ResourceCopy** ，这将影响延迟上下文中的动态资源（在映射-丢弃调用之后），或在将命令列表本地资源保留为当前的即时上下文上，应将新资源概念地分配给提供副本的新目标，并且必须将旧资源复制到新资源（如果操作是[**ResourceCopyRegion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_resourcecopyregion)）。

 

 





