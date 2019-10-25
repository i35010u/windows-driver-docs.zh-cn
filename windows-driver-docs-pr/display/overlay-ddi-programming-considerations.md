---
title: 覆盖 DDI 编程注意事项
description: 覆盖 DDI 编程注意事项
ms.assetid: 887624a7-0293-4add-94a7-d490ebd93205
keywords:
- 覆盖 DDI WDK Windows 7 显示，编程注意事项
- 覆盖 DDI WDK Server 2008 R2 显示，编程注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31390ab118f7999bce950a3cf374cdf994f41211
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829892"
---
# <a name="overlay-ddi-programming-considerations"></a>覆盖 DDI 编程注意事项


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

在用户模式显示驱动程序中实现[覆盖 DDI](overlay-ddi.md)时，应考虑以下编程技巧：

-   如果驱动程序支持覆盖 DDI，则必须在[D3DCAPS9](https://go.microsoft.com/fwlink/p/?linkid=122122)结构的**cap**成员中设置 D3DCAPS\_覆盖位。 DirectX 9.0 SDK 文档中介绍了 D3DCAPS9 结构。 驱动程序将 D3DCAPS\_覆盖位设置为响应对其[**GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数的调用，其中 D3DDDICAPS\_GETD3D9CAPS 值在[**D3DDDIARG\_GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的**类型**成员中进行设置，在*pData*参数指向。

-   当显示格式为64位而不是32位时（例如，当 DWM 使用[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举中的 D3DDDIFMT\_A16B16G16R16F 值进行显示模式）时，Direct3D 运行时会将覆盖颜色键的低32位置于**D3DDDI\_OVERLAYINFO**的**DstColorKeyHigh**成员中的[**D3DDDI\_OVERLAYINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)结构和上限32位的**DstColorKeyLow**成员。

 

 





