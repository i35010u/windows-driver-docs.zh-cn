---
title: VPE 和内核模式视频传输体系结构
description: VPE 和内核模式视频传输体系结构
keywords:
- 绘制内核模式视频传输 WDK DirectDraw、体系结构
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示，体系结构
- 内核模式视频传输 WDK DirectDraw，体系结构
- 视频传输内核模式 WDK DirectDraw，体系结构
- 视频捕获 WDK 视频传输内核模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eda721d2dd4b0ac21bf5be612ca1dad6fbce375
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812533"
---
# <a name="vpe-and-kernel-mode-video-transport-architecture"></a>VPE 和内核模式视频传输体系结构

本部分提供了有关在 DirectX 5.0 及更高版本中 (VPE) 和内核模式视频传输的视频端口扩展的 Windows 2000 和更高版本体系结构的一些详细信息。 内核模式视频传输的体系结构基于 Microsoft 添加为与设备无关的代码的新函数。 内核模式视频传输包含 [**DxApi**](/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi) 函数，该函数作为 directdraw 的一部分、 [视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)和作为 directdraw 的一部分提供的 COM 接口方法提供。

## <a name="windows-2000-and-later"></a>Windows 2000 及更高版本

在 Windows 2000 和更高版本中，如下图所示，DxApi 回调是 [视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)的一部分。

![阐释 windows 2000 内核模式视频传输体系结构的关系图](images/ddfg011.png)

有关 DxApi 回调的详细信息，请参阅 [适用于 Windows 2000 和更高版本的 DxApi 微型端口驱动程序功能](dxapi-miniport-driver-functions-for-windows-2000-and-later.md)。

上图显示了与其他内核模式和用户模式组件相关的内核模式视频传输体系结构， (虚线表示内核转换) 。 在此体系结构中，DirectShow (或其他用户模式客户端) 调用 [IDirectDrawKernel](/windows/win32/api/ddkernel/nn-ddkernel-idirectdrawkernel) 和 [IDirectDrawSurfaceKernel](/windows/win32/api/ddkernel/nn-ddkernel-idirectdrawsurfacekernel) DirectDraw COM 接口，以获取 DirectDraw 对象和 surface 对象的句柄。

> [!NOTE]
> 此体系结构还支持在 MPEG 设备和 VGA 设备之间使用 PCI 总线进行数据流。

在 Windows 2000 和更高版本中，客户端随后将这些句柄传递到微型端口驱动程序。 这些句柄在对内核模式视频传输的调用中指定。 下图显示了如何在用户和内核模式视频传输中传递句柄的简单版本。

![说明 windows 2000 视频传输中的句柄传递的关系图](images/ddfg012.png)
