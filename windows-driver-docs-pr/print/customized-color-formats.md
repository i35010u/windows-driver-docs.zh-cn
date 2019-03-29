---
title: 自定义的颜色格式
description: 自定义的颜色格式
ms.assetid: 309d33e8-6338-4c32-8e03-d6cbf3371e16
keywords:
- Unidrv，颜色格式
- 颜色格式 WDK Unidrv
- 自定义的颜色格式 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f2940f05a625320c5effb4e8dd87441d3d6ca27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562836"
---
# <a name="customized-color-formats"></a>自定义的颜色格式





Unidrv 支持中列出的若干颜色格式[处理颜色格式](handling-color-formats.md)。 对于这些格式，Unidrv GDI 位图将转换为正确的格式将其发送到打印机之前。 如果您的打印机接受不受 Unidrv 的格式，必须提供插件的呈现实现[ **IPrintOemUni::ImageProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff554261)方法。

如果你实现了[ **IPrintOemUni::ImageProcessing**](https://msdn.microsoft.com/library/windows/hardware/ff554261)，如果用户选择颜色格式 （ColorMode 选项） Unidrv 无法处理，则每次 GDI 位图数据的缓冲区，并已准备好进行打印，Unidrv 调用的方法，并将位图的地址传递作为输入参数。 该方法必须将位图转换为指定的格式，请执行[自定义半色调](customized-halftoning.md)操作，如有必要，并调用[ **IPrintOemDriverUni::DrvWriteSpoolBuf** ](https://msdn.microsoft.com/library/windows/hardware/ff553138)方法以将修改后的位图发送到打印后台处理程序。 它还必须调用[ **IPrintOemDriverUni::DrvXMoveTo** ](https://msdn.microsoft.com/library/windows/hardware/ff553141)并[ **IPrintOemDriverUni::DrvYMoveTo** ](https://msdn.microsoft.com/library/windows/hardware/ff553144)方法来更新游标位置。 有关这些操作的详细信息，请参阅的说明**IPrintOemUni::ImageProcessing**。

如果呈现插件实现[ **IPrintOemUni::ImageProcessing**](https://msdn.microsoft.com/library/windows/hardware/ff554261)，它可以实现[ **IPrintOemUni::MemoryUsage**](https://msdn.microsoft.com/library/windows/hardware/ff554264)。

 

 




