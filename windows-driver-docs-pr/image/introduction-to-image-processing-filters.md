---
title: 图像处理筛选器简介
description: 图像处理筛选器简介
ms.assetid: 59fc1bc1-c783-43df-9778-ea4306f6dd50
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22cc0c7372512dbf7339029b162a070a6e4a486f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358885"
---
# <a name="introduction-to-image-processing-filters"></a>图像处理筛选器简介





图像处理筛选器是 WIA 扩展。 图像处理筛选器有两个主要用途：

-   若要允许从驱动程序分隔图像处理代码。 例如，若要修改的亮度和对比度的一个映像，并执行噪和旋转，则可以使用图像处理筛选器。 图像处理筛选器是在其自己的 DLL，独立于用户模式驱动程序 DLL 中。 图像处理筛选器从其执行筛选的驱动程序接收未筛选的图像处理数据。

-   若要启用精确的实时预览。 图像处理筛选器用于从一个新的 Windows Vista WIA 预览组件 （Microsoft Windows SDK 文档中所述），提供准确的实时预览。 在此上下文中，"实时"意味着应用程序无需更改一些属性设置，对此进行讨论在本部分中的更高版本后重新获取扫描程序中的映像。 预览是准确的因为实际的预览图像上的供应商组件而不是只在完全独立的映像是随机筛选器的实际执行筛选。

为了提供准确的预览，筛选器应实现[**亮度**](https://msdn.microsoft.com/library/windows/hardware/ff552567)并[**对比度**](https://msdn.microsoft.com/library/windows/hardware/ff552573)最少的属性。 这是因此常见 UI 向用户提供亮度和对比度控件，可以显示准确的预览。

扫描图像时，始终执行图像处理筛选器。 因此没有应用程序获取扫描程序从映像，而无需图像处理第一次应用筛选器方法。 不需要应用程序不需要注意的筛选器。

Microsoft 提供了缓存的扫描程序从获取的原始、 未筛选的预览图像的 WIA 预览组件。 预览组件使可能应用筛选器而无需重新获取映像扫描程序从多个时间图像。 WIA 预览组件通常用于预览图像时应用程序允许用户更改设置，如对比度和亮度。 虽然用户可以更改设置，该应用程序可以连续显示生成的映像在预览窗格中而无需重新扫描图像。

图像处理筛选器是一个 WIA 扩展，运行为进程内 COM 组件。 与分段的筛选器，不同应用程序通常不会创建图像处理筛选器本身的实例通过调用**IWiaItem2::GetExtension** （Windows SDK 文档中所述）。 相反，应用程序将创建 WIA 预览组件，这反过来将加载实际图像处理筛选器使用的实例**IWiaItem2::GetExtension**方法。 当应用程序调用，也会自动调用图像处理筛选器**IWiaTransfer::Download**。

图像处理筛选器是与驱动程序，并且通常与驱动程序一起分发。 WIA 预览组件现已推出 sti.dll，并附带了操作系统。

下图显示了图像处理筛选器由 WIA 组件加载到应用程序的进程。 请注意，可能是在应用程序的进程中加载在同一时间，因此必须谨慎这对筛选器写入的图像处理筛选器的多个实例。 例如，如果当使用全局 （静态） 变量时，筛选器编写器必须确保正确的同步。

![说明通过 wia 组件加载到应用程序的进程的图像处理筛选器的关系图](images/wia-components-app-process.png)

 

 




