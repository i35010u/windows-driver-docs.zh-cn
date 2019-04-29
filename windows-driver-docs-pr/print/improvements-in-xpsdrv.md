---
title: XPSDrv 的改进
description: 本主题提供有关对 XPSDrv 呈现体系结构所做的更新的信息。
ms.assetid: 5D76ECA2-C5F6-47E4-BC05-B5137AD4196B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bdc1c53f3a8d5505ecfc23271229e8f6e93c5ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390566"
---
# <a name="improvements-in-xpsdrv"></a>XPSDrv 的改进


本主题提供有关对 XPSDrv 呈现体系结构所做的更新的信息。

**XPS 格式**

XPS 打印 API 和/或打印筛选器管道会将转换之间无缝[Microsoft Xml 纸张规范 1.0](https://msdn.microsoft.com/windows/hardware/gg463375) (MS XPS) 和[OpenXPS](http://www.ecma-international.org/publications/standards/Ecma-388.htm) (ECMA 388)。 除非另行指定，否则 v4 打印驱动程序默认为使用 MS XPS。 使用清单指令 XpsFormat，可以选择驱动程序以支持一个或两个可用的 XPS 格式。 有关 OpenXPS 支持的详细信息，请参阅[Windows 中的 OpenXPS 支持](https://msdn.microsoft.com/library/windows/hardware/br259130)。

**XPS 光栅化服务的改进**

若要使用的图形处理单元 (GPU) 提供更快的 XPS 光栅化的 Windows 8 中改进了 XPS 光栅化服务。 使用 Windows 显示器驱动程序模型 (WDDM) 1.2 的 Gpu 具有 Windows 8 系统上提供了这些性能改进。 XPS 呈现筛选器不需要进行任何修改才能利用此项改进，并且它将适用于 v3 和 v4 打印驱动程序。

XPS 光栅化服务还可以提供多个像素格式，包括以下新的、 高精度格式光栅化。 结果是，使用 XPS 光栅化服务的打印驱动程序现在可以针对在 8 位、 16 位和 32 位 / 通道的颜色精度。 像素格式的详细信息，请参阅[本机像素格式概述](https://msdn.microsoft.com/library/windows/hardware/ee719797.aspx)。 支持这些新的像素格式[ **XPSRaterizationFactory1::CreateRasterizer1** ](https://msdn.microsoft.com/library/windows/hardware/hh802468)方法。 下表显示了 XPS 光栅化服务像素格式。

| 值                                | 通道计数 | 每个通道的位 | 每像素位数 | 存储类型 |
|--------------------------------------|---------------|------------------|----------------|--------------|
| GUID\_WICPixelFormat32bppPBGRA       | 4             | 8                | 32             | UINT         |
| GUID\_WICPixelFormat64bppPRGBAHalf   | 4             | 16               | 64             | 浮点        |
| GUID\_WICPixelFormat128bppPRGBAFloat | 4             | 32               | 128            | 浮点        |

 

**IPrintCoreHelperUni2**

[IPrintCoreHelperUni2](https://msdn.microsoft.com/library/windows/hardware/hh406580)以支持从 GPD 文件的命令字符串中检索的 Windows 8 中引入了接口。 该接口是相同[IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)，除了其他**GetNamedCommand**方法。

## <a name="related-topics"></a>相关主题
[IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)  
[IPrintCoreHelperUni2](https://msdn.microsoft.com/library/windows/hardware/hh406580)  
[Microsoft Xml 纸张规范 1.0](https://msdn.microsoft.com/windows/hardware/gg463375)  
[本机像素格式概述](https://msdn.microsoft.com/library/windows/hardware/ee719797.aspx)  
[OpenXPS](http://www.ecma-international.org/publications/standards/Ecma-388.htm)  
[Windows 中的 OpenXPS 支持](https://msdn.microsoft.com/library/windows/hardware/br259130)  
[V4 打印机驱动程序呈现体系结构](v4-driver-rendering-architecture.md)  
[**XPSRaterizationFactory1::CreateRasterizer1**](https://msdn.microsoft.com/library/windows/hardware/hh802468)  



