---
title: XPSDrv 的改进
description: 本主题提供有关对 XPSDrv 呈现体系结构进行的更新的信息。
ms.assetid: 5D76ECA2-C5F6-47E4-BC05-B5137AD4196B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb8e4d193c6638a321bfc49e9034e6b7f581a324
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881882"
---
# <a name="improvements-in-xpsdrv"></a>XPSDrv 的改进

本主题提供有关对 XPSDrv 呈现体系结构进行的更新的信息。

## <a name="xps-format"></a>XPS 格式

XPS 打印 API 和/或打印筛选器管道将在[MICROSOFT XML 纸张规范 1.0](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614032(v=vs.85)) （MS xp）和[OpenXPS](https://www.ecma-international.org/publications/standards/Ecma-388.htm) （ECMA-388）之间无缝转换。 除非另行指定，否则 v4 打印驱动程序默认使用 MS XP。 使用清单指令 XpsFormat，驱动程序可能会选择支持一种或两种可用的 XPS 格式。 有关 OpenXPS 支持的详细信息，请参阅[Windows 中的 OpenXPS 支持](https://docs.microsoft.com/windows-hardware/drivers/print/driver-support-for-openxps)。

## <a name="xps-rasterization-service-improvements"></a>XPS 光栅化服务改进

Windows 8 中已改进了 XPS 光栅化服务，以利用图形处理单元（GPU）提供更快的 XPS 光栅化。 这些性能改进在具有使用 Windows 显示驱动程序模型（WDDM）1.2 的 Gpu 的 Windows 8 系统上可用。 XPS 呈现筛选器不需要任何修改即可利用此改进，并且它将可用于 v3 和 v4 打印驱动程序。

XPS 光栅化服务还可以提供多种像素格式的光栅化，其中包括以下新的高精度格式。 因此，使用 XPS 光栅化服务的打印驱动程序现在可以将颜色精度设定为每通道8位、16位和32位。 有关像素格式的详细信息，请参阅[本机像素格式概述](https://docs.microsoft.com/windows/desktop/wic/-wic-codec-native-pixel-formats)。 [**XPSRaterizationFactory1：： CreateRasterizer1**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))方法支持这些新的像素格式。 下表显示了 XPS 光栅化服务像素格式。

| Value                                | 通道计数 | 每通道位数 | 每像素位数 | 存储类型 |
|--------------------------------------|---------------|------------------|----------------|--------------|
| GUID\_WICPixelFormat32bppPBGRA       | 4             | 8                | 32             | UINT         |
| GUID\_WICPixelFormat64bppPRGBAHalf   | 4             | 16               | 64             | 浮点        |
| GUID\_WICPixelFormat128bppPRGBAFloat | 4             | 32               | 128            | 浮点        |

## <a name="iprintcorehelperuni2"></a>IPrintCoreHelperUni2

Windows 8 中引入了[IPrintCoreHelperUni2](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni2)接口，以支持从 GPD 文件中检索命令字符串。 除了附加的**GetNamedCommand**方法以外，接口与[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)完全相同。

## <a name="related-topics"></a>相关主题

[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)  

[IPrintCoreHelperUni2](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni2)  

[Microsoft XML 纸张规范1。0](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614032(v=vs.85))  

[本机像素格式概述](https://docs.microsoft.com/windows/desktop/wic/-wic-codec-native-pixel-formats)  

[OpenXPS](https://www.ecma-international.org/publications/standards/Ecma-388.htm)  

[Windows 中的 OpenXPS 支持](https://docs.microsoft.com/windows-hardware/drivers/print/driver-support-for-openxps)  

[V4 打印机驱动程序呈现体系结构](https://docs.microsoft.com/windows-hardware/drivers/print/v4-driver-rendering-architecture)  

[**XPSRaterizationFactory1::CreateRasterizer1**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))  
