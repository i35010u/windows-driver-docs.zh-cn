---
title: 覆盖 DDI 编程注意事项
description: 覆盖 DDI 编程注意事项
ms.assetid: 887624a7-0293-4add-94a7-d490ebd93205
keywords:
- 覆盖 DDI WDK Windows 7 显示，编程注意事项
- 覆盖 DDI WDK Server 2008 R2 显示，编程注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c68740fcc93537b1e12559968ad049326a9a039b
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734081"
---
# <a name="overlay-ddi-programming-considerations"></a>覆盖 DDI 编程注意事项


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

在用户模式显示驱动程序中实现 [覆盖 DDI](overlay-ddi.md) 时，应考虑以下编程技巧：

-   如果驱动程序支持覆盖 DDI，则必须 \_ 在[D3DCAPS9](/windows/win32/api/d3d9caps/ns-d3d9caps-d3dcaps9)结构的**CAP**成员中设置 D3DCAPS 覆盖位。 DirectX 9.0 SDK 文档中介绍了 D3DCAPS9 结构。 驱动程序将 D3DCAPS \_ 覆盖位设置为响应对其[**GetCaps**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数的调用，其中在 \_ *D3DDDIARG*参数指向的[**GetCaps \_ pData**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的**Type**成员中设置 D3DDDICAPS GETD3D9CAPS 值。

-   如果显示格式为64位而不是32位 (例如，当 DWM 在 \_ 显示模式) 使用[**D3DDDIFORMAT**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举中的 D3DDDIFMT A16B16G16R16F 值时，Direct3D 运行时会将覆盖颜色键的低32位置于[**D3DDDI \_ OVERLAYINFO**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)结构的**DstColorKeyLow**成员32和**DstColorKeyHigh \_ **D3DDDI 的**OVERLAYINFO**成员中。

