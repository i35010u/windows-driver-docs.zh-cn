---
title: XPSDrv 的改进
description: 本主题提供有关对 XPSDrv 呈现体系结构所做的更新的信息。
ms.assetid: 5D76ECA2-C5F6-47E4-BC05-B5137AD4196B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e04029b4557c9e9908e6c044d7e8590dcd1265c3
ms.sourcegitcommit: 444ae04cb8f6da8964eef89524a5671c1e949f7f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2019
ms.locfileid: "67416493"
---
# <a name="improvements-in-xpsdrv"></a>XPSDrv 的改进

本主题提供有关对 XPSDrv 呈现体系结构所做的更新的信息。

## <a name="xps-format"></a>XPS 格式

XPS 打印 API 和/或打印筛选器管道会将转换之间无缝[Microsoft Xml 纸张规范 1.0](https://docs.microsoft.com/en-us/previous-versions/windows/hardware/design/dn614032(v=vs.85)) (MS XPS) 和[OpenXPS](http://www.ecma-international.org/publications/standards/Ecma-388.htm) (ECMA 388)。 除非另行指定，否则 v4 打印驱动程序默认为使用 MS XPS。 使用清单指令 XpsFormat，可以选择驱动程序以支持一个或两个可用的 XPS 格式。 有关 OpenXPS 支持的详细信息，请参阅[Windows 中的 OpenXPS 支持](https://docs.microsoft.com/windows-hardware/drivers/print/driver-support-for-openxps)。

## <a name="xps-rasterization-service-improvements"></a>XPS 光栅化服务的改进

若要使用的图形处理单元 (GPU) 提供更快的 XPS 光栅化的 Windows 8 中改进了 XPS 光栅化服务。 使用 Windows 显示器驱动程序模型 (WDDM) 1.2 的 Gpu 具有 Windows 8 系统上提供了这些性能改进。 XPS 呈现筛选器不需要进行任何修改才能利用此项改进，并且它将适用于 v3 和 v4 打印驱动程序。

XPS 光栅化服务还可以提供多个像素格式，包括以下新的、 高精度格式光栅化。 结果是，使用 XPS 光栅化服务的打印驱动程序现在可以针对在 8 位、 16 位和 32 位 / 通道的颜色精度。 像素格式的详细信息，请参阅[本机像素格式概述](https://docs.microsoft.com/windows/desktop/wic/-wic-codec-native-pixel-formats)。 支持这些新的像素格式[ **XPSRaterizationFactory1::CreateRasterizer1** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))方法。 下表显示了 XPS 光栅化服务像素格式。

| ReplTest1                                | 通道计数 | 每个通道的位 | 每像素位数 | 存储类型 |
|--------------------------------------|---------------|------------------|----------------|--------------|
| GUID\_WICPixelFormat32bppPBGRA       | 4             | 8                | 32             | UINT         |
| GUID\_WICPixelFormat64bppPRGBAHalf   | 4             | 16               | 64             | 浮点        |
| GUID\_WICPixelFormat128bppPRGBAFloat | 4             | 32               | 128            | 浮点        |

## <a name="iprintcorehelperuni2"></a>IPrintCoreHelperUni2

[IPrintCoreHelperUni2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni2)以支持从 GPD 文件的命令字符串中检索的 Windows 8 中引入了接口。 该接口是相同[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)，除了其他**GetNamedCommand**方法。

## <a name="related-topics"></a>相关主题

[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)  

[IPrintCoreHelperUni2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni2)  

[Microsoft Xml 纸张规范 1.0](https://docs.microsoft.com/en-us/previous-versions/windows/hardware/design/dn614032(v=vs.85))  

[本机像素格式概述](https://docs.microsoft.com/windows/desktop/wic/-wic-codec-native-pixel-formats)  

[OpenXPS](http://www.ecma-international.org/publications/standards/Ecma-388.htm)  

[Windows 中的 OpenXPS 支持](https://docs.microsoft.com/windows-hardware/drivers/print/driver-support-for-openxps)  

[V4 打印机驱动程序呈现体系结构](https://docs.microsoft.com/windows-hardware/drivers/print/v4-driver-rendering-architecture)  

[**XPSRaterizationFactory1::CreateRasterizer1**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))  
