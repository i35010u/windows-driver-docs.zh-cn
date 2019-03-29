---
title: VPE 和内核模式视频传输体系结构
description: VPE 和内核模式视频传输体系结构
ms.assetid: 7264932a-7fe9-4ffe-bd25-b5cd605739fa
keywords:
- 绘制内核模式视频传输 WDK DirectDraw，体系结构
- DirectDraw 内核模式视频传输 WDK Windows 2000 显示，体系结构
- 内核模式视频传输 WDK DirectDraw，体系结构
- 视频传输内核模式 WDK DirectDraw，体系结构
- 视频捕获 WDK 视频传输内核模式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cd23ec90f61319e2cf5a6df301f6d9ccf610685
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576807"
---
# <a name="vpe-and-kernel-mode-video-transport-architecture"></a>VPE 和内核模式视频传输体系结构


## <span id="ddk_vpe_and_kernel_mode_video_transport_architecture_gg"></span><span id="DDK_VPE_AND_KERNEL_MODE_VIDEO_TRANSPORT_ARCHITECTURE_GG"></span>


本部分提供一些有关 Windows 2000 和更高版本的视频端口扩展 (VPE) 和内核模式下在 DirectX 5.0 和更高版本的视频传输体系结构的详细信息。 内核模式视频传输体系结构基于 Microsoft 添加为独立于设备的代码的新函数。 内核模式视频传输组成[ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364) DirectDraw，过程中提供的函数[微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)，以及提供的 COM 接口方法作为 DirectDraw 的一部分。

### <a name="span-idwindows2000andlaterspanspan-idwindows2000andlaterspanwindows-2000-and-later"></a><span id="windows_2000_and_later"></span><span id="WINDOWS_2000_AND_LATER"></span>Windows 2000 及更高版本

在 Windows 2000 及更高版本下, 图中所示，DxApi 回调属于[微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)。

![演示 windows 2000 内核模式视频传输体系结构的关系图](images/ddfg011.png)

有关 DxApi 回调的详细信息，请参阅[DxApi 微型端口驱动程序函数对于 Windows 2000 和更高版本](dxapi-miniport-driver-functions-for-windows-2000-and-later.md)。

上图显示了与 （虚线表示内核转换） 的其他内核模式和用户模式组件相关的内核模式视频传输体系结构。 在此体系结构，DirectShow （或另一个用户模式下客户端） 调用[IDirectDrawKernel](https://msdn.microsoft.com/library/windows/hardware/ff567398)并[IDirectDrawSurfaceKernel](https://msdn.microsoft.com/library/windows/hardware/ff567409) DirectDraw COM 界面，可获取的句柄 DirectDraw 对象和图面上的对象。

**请注意**  此体系结构还支持 PCI 总线用于 MPEG 设备和 VGA 设备之间的数据流。

 

在 Windows 2000 及更高版本，客户端然后将这些句柄传递给微型端口驱动程序。 内核模式视频传输到的调用中指定了这些句柄。 下图显示了在用户和内核模式视频传输过程中传递的句柄的简单版本。

![说明在 windows 2000 视频传输过程中传递的句柄的关系图](images/ddfg012.png)

 

 





