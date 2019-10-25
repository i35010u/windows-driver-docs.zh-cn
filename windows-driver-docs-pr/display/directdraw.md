---
title: DirectDraw
description: DirectDraw
ms.assetid: b7f1194e-0f5e-444e-a71c-6a4a836547d9
keywords:
- DirectDraw WDK Windows 2000 显示
- Windows 2000 显示器驱动程序型号 WDK，DirectDraw
- 显示驱动程序模型 WDK Windows 2000，DirectDraw
- 标头文件 WDK DirectDraw
- DirectDraw WDK Windows 2000 显示，头文件
- 绘制 WDK DirectDraw
- 绘制 WDK DirectDraw，头文件
- 图形 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4264ba68e863c72f99df4da5f97451a8d0e0e639
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839735"
---
# <a name="directdraw"></a>DirectDraw


## <span id="ddk_directdraw_gg"></span><span id="DDK_DIRECTDRAW_GG"></span>


本部分介绍 Microsoft DirectDraw 接口和体系结构，并为 DirectDraw 驱动程序编写器提供实现准则。 本指南专为 Microsoft Windows 2000 及更高版本编写。 读者应该熟悉 DirectDraw Api，并对 Windows 2000 显示器驱动程序模型进行牢固的理解。

正在为 Microsoft Windows 2000 和更高版本创建 Microsoft DirectDraw 驱动程序的驱动程序编写器应使用以下头文件：

-   *ddrawint*包含 DirectDraw 驱动程序的基本类型、常量和结构。

-   *ddraw*包含应用程序和驱动程序使用的基本类型、常量和结构。

-   当驱动程序支持 DirectDraw 视频端口扩展（VPE）时，将使用*dvp。*

-   当视频微型端口驱动程序包括对内核模式视频传输（ [**DxApi\_接口**](https://docs.microsoft.com/windows/desktop/api/dxmini/ns-dxmini-_dxapi_interface)结构指定的函数）的支持时，将使用*dxmini。*

-   视频捕获驱动程序使用*ddkmapi*来访问[**DxApi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)函数。 DirectDraw 又会调用 DxApi 接口。

-   当驱动程序要执行其自己的内存管理，而不是依赖于 DirectDraw 运行时，将使用*dmemmgr。*

-   当驱动程序包含内核模式支持时，将使用*ddkernel。*

-   *dx95type*使驱动程序编写者可以轻松地将现有 windows 98/Me 驱动程序移植到 windows 2000 和更高版本。 此标头文件映射两个平台上不同的名称。

*Ddraw*头文件随 Windows SDK 一起提供;所有其他标头文件都包含在 Windows 驱动程序工具包（WDK）中。 Windows 驱动程序开发工具包（DDK）还在*p3samp* video 显示目录中包含 DirectDraw 驱动程序的示例代码。

Directdraw 驱动程序函数、回调和结构的引用页可以在[Directdraw 驱动程序函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)和[Directdraw 驱动程序结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)中找到。

有关 DirectDraw 的详细信息，请参阅 Windows SDK。 DirectDraw 驱动程序作者可以通过电子邮件向<em>directx@microsoft.com</em>发送问题和评论。

 

 





