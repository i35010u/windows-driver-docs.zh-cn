---
title: XPSDrv 的改进
description: 本主题提供有关对 XPSDrv 呈现体系结构进行的更新的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86284bc1d723ed8f8fd49c1ccf93930b21d0f5ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796753"
---
# <a name="improvements-in-xpsdrv"></a>XPSDrv 的改进

本主题提供有关对 XPSDrv 呈现体系结构进行的更新的信息。

## <a name="xps-format"></a>XPS 格式

XPS 打印 API 和/或打印筛选器管道将在 [MICROSOFT XML 纸张规范 1.0](/previous-versions/windows/hardware/design/dn614032(v=vs.85)) (MS xp) 和 [OpenXPS](https://www.ecma-international.org/publications/standards/Ecma-388.htm) (ECMA-388) 之间无缝转换。 除非另行指定，否则 v4 打印驱动程序默认使用 MS XP。 使用清单指令 XpsFormat，驱动程序可能会选择支持一种或两种可用的 XPS 格式。 有关 OpenXPS 支持的详细信息，请参阅 [Windows 中的 OpenXPS 支持](./driver-support-for-openxps.md)。

## <a name="xps-rasterization-service-improvements"></a>XPS 光栅化服务改进

Windows 8 中已改进 XPS 光栅化服务，可以使用图形处理单元 (GPU) 提供更快的 XPS 光栅化。 这些性能改进在具有使用 Windows 显示驱动程序模型 (WDDM) 1.2 的 Gpu 的 Windows 8 系统上可用。 XPS 呈现筛选器不需要任何修改即可利用此改进，并且它将可用于 v3 和 v4 打印驱动程序。

XPS 光栅化服务还可以提供多种像素格式的光栅化，其中包括以下新的高精度格式。 因此，使用 XPS 光栅化服务的打印驱动程序现在可以将颜色精度设定为每通道8位、16位和32位。 有关像素格式的详细信息，请参阅 [本机像素格式概述](/windows/desktop/wic/-wic-codec-native-pixel-formats)。 [**XPSRaterizationFactory1：： CreateRasterizer1**](/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))方法支持这些新的像素格式。 下表显示了 XPS 光栅化服务像素格式。

| “值”                                | 通道计数 | 每通道位数 | 每像素位数 | 存储类型 |
|--------------------------------------|---------------|------------------|----------------|--------------|
| GUID \_ WICPixelFormat32bppPBGRA       | 4             | 8                | 32             | UINT         |
| GUID \_ WICPixelFormat64bppPRGBAHalf   | 4             | 16               | 64             | Float        |
| GUID \_ WICPixelFormat128bppPRGBAFloat | 4             | 32               | 128            | Float        |

## <a name="iprintcorehelperuni2"></a>IPrintCoreHelperUni2

Windows 8 中引入了 [IPrintCoreHelperUni2](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni2) 接口，以支持从 GPD 文件中检索命令字符串。 除了附加的 **GetNamedCommand** 方法以外，接口与 [IPrintCoreHelperUni](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)完全相同。

## <a name="related-topics"></a>相关主题

[IPrintCoreHelperUni](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)  

[IPrintCoreHelperUni2](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni2)  

[Microsoft XML 纸张规范1。0](/previous-versions/windows/hardware/design/dn614032(v=vs.85))  

[本机像素格式概述](/windows/desktop/wic/-wic-codec-native-pixel-formats)  

[OpenXPS](https://www.ecma-international.org/publications/standards/Ecma-388.htm)  

[Windows 中的 OpenXPS 支持](./driver-support-for-openxps.md)  

[V4 打印机驱动程序渲染体系结构](./v4-driver-rendering-architecture.md)  

[**XPSRaterizationFactory1::CreateRasterizer1**](/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))
