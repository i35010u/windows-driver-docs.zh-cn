---
title: DirectDraw
description: DirectDraw
ms.assetid: b7f1194e-0f5e-444e-a71c-6a4a836547d9
keywords:
- DirectDraw WDK Windows 2000 显示
- Windows 2000 显示器驱动程序模型 WDK、 DirectDraw
- 显示器驱动程序模型 WDK Windows 2000 DirectDraw
- 头文件 WDK DirectDraw
- DirectDraw WDK Windows 2000 显示，标头文件
- 绘制 WDK DirectDraw
- 绘制 WDK DirectDraw，标头文件
- 显示图形 WDK Windows 2000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d450f33a45a569e407a702eff00301cffe34cce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541451"
---
# <a name="directdraw"></a>DirectDraw


## <span id="ddk_directdraw_gg"></span><span id="DDK_DIRECTDRAW_GG"></span>


本部分介绍 Microsoft DirectDraw 界面和体系结构，并为 DirectDraw 驱动程序编写器提供实现指导原则。 指导原则是 Microsoft Windows 2000 和更高版本编写的。 读者应熟悉 DirectDraw Api，并具有牢固掌握 Windows 2000 的显示驱动程序模型。

对于要创建 Microsoft DirectDraw 驱动程序适用于 Microsoft Windows 2000 及更高版本的驱动程序编写人员应使用以下标头文件：

-   *ddrawint.h*包含基本类型、 常量和 DirectDraw 驱动程序的结构。

-   *ddraw.h*包含基本类型、 常量和使用应用程序和驱动程序的结构。

-   *dvp.h*时驱动程序支持 DirectDraw 视频端口扩展 (VPE) 使用。

-   *dxmini.h*微型端口驱动程序包括对内核模式视频传输，DxApi 接口的支持时，将使用 (指定的函数[ **DXAPI\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff557395)结构)。

-   *ddkmapi.h*视频捕获驱动程序用于访问[ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364)函数。 DirectDraw，反过来，调用 DxApi 接口。

-   *dmemmgr.h*时驱动程序想要执行其自身内存管理，而不是依靠 DirectDraw 运行时使用。

-   *ddkernel.h*时驱动程序支持内核模式下使用。

-   *dx95type.h*允许驱动程序编写人员轻松地移植现有 Windows 98 / 我为 Windows 2000 和更高版本的驱动程序。 此标头文件将在两个平台不同的名称映射。

*Ddraw.h*标头文件随 Windows SDK; 将使用 Windows Driver Kit (WDK) 包含所有其他头文件。 Windows 驱动程序开发工具包 (DDK) 还包含 DirectDraw 驱动程序中的示例代码*p3samp*视频显示目录。

对于 DirectDraw 驱动程序函数，回叫，页参考和结构可在[DirectDraw 驱动程序函数](https://msdn.microsoft.com/library/windows/hardware/ff553825)并[DirectDraw 驱动程序结构](https://msdn.microsoft.com/library/windows/hardware/ff553831)。

DirectDraw 有关详细信息，请参阅 Windows SDK。 DirectDraw 驱动程序编写人员可以通过电子邮件发送到发送问题和提出的意见<em>directx@microsoft.com</em>。

 

 





