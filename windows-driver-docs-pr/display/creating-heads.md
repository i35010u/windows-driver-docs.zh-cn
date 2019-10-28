---
title: 创建头
description: 创建头
ms.assetid: 0b6d4aa0-e3c9-45df-998d-d6dfca5ab720
keywords:
- 机头 WDK DirectX 9。0
- 多头硬件 WDK DirectX 9.0，创建磁头
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c90b9baa1566ebd0f2a1c51fa138198218486d56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839774"
---
# <a name="creating-heads"></a>创建头


## <span id="ddk_creating_heads_gg"></span><span id="DDK_CREATING_HEADS_GG"></span>


Microsoft DirectX 9.0 驱动程序为每个多头卡创建一个 Microsoft Direct3D 上下文，并为每个多头卡上的每个头创建一个 Microsoft DirectDraw 对象。 因此，多个 head 卡的创建过程具有一个打印头部分和一个十字。 每个磁头的部分大致对应于 DirectDraw DDI 调用，这是对 Direct3D DDI 调用的交叉点。

各个机头间的连接点是由驱动程序的[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)函数创建的 Direct3D 句柄。 该驱动程序将每个表面的唯一 Direct3D 句柄分配给该组中的所有头。 主头上的 Direct3D 上下文会管理所有这些句柄，并可面向在任何头上创建的任何呈现器目标，最值得注意的是从属头上翻转链中的后台缓冲区。 每个从属标题的**D3dCreateSurfaceEx**函数必须能够更新由主 head 管理的句柄查找表。 然后，这些句柄仅用于主机头的对驱动程序的[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数的调用。

驱动程序仅在主头上创建纹理和其他资源。

驱动程序将创建并使用标题，如以下序列中所述：

1.  对于每个 head，将执行以下操作来设置显示模式和主翻转曲面：
    -   运行时设置显示模式。
    -   运行时创建 DirectDraw 对象。
    -   运行时将创建一个主翻转链，并可能创建一个 Z 缓冲区。 运行时在每个图面（包括 Z 缓冲区）的[**DDSCAPS2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))结构的**dwCaps2**成员中指定**DDSCAPS2\_ADDITIONALPRIMARY** （0x80000000）功能位，以指示多头卡。 运行时调用驱动程序的[*DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))函数。
    -   运行时首先为主节点和由**AdapterOrdinalInGroup**为从属项定义的顺序调用驱动程序的[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)函数。 在此调用中，运行时传递的 Direct3D 句柄保证在组中的所有头中是唯一的。 驱动程序可以在从属标头的句柄查找表中插入引用。 但是，由于 Direct3D 上下文不是在从属标题上创建的，因此不会向任何从属头发出[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)命令。 因此，不需要插入此引用。
    -   在运行时对所有 head （包括 master）调用[*DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))后，将对主 Head 的 DirectDraw 对象上的每个从属 head 翻转链进行进一步的[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)调用。 驱动程序会在主头的句柄查找表中输入每个从属标头的每个正面、背面和深度/模具缓冲区。

2.  运行时仅为主头上的 DirectDraw 对象调用驱动程序的[*D3dContextCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)函数。 这是在应用程序运行时唯一使用的上下文。

3.  当应用程序请求创建纹理和资源时，运行时会通过主头调用驱动程序的[*DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))和[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)函数。

4.  当应用程序进行呈现调用时，运行时会使用适当的操作代码在主头上调用驱动程序的[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数。

    当应用程序执行其他操作时，会将以下调用路由到主头和从属头：

    -   如步骤1中所述， [**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)调用可为驱动程序提供每个从属 head 翻转链的句柄。 当应用程序将帧呈现到一个从属头交换链的后台缓冲区时，这些句柄通常与**D3DDP2OP\_SETRENDERTARGET**操作代码标记一起使用。
    -   运行时在每个 head （主节点和从属节点）上调用驱动程序的[*DdFlip*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_flip)函数，以将缓冲区显示给这些磁头的主表面。 此调用绝不会从一个磁头向另一个头的主要表面呈现后台缓冲区。 每个头上的翻转链都是完全独立的。
    -   运行时可能会调用驱动程序的[*DdBlt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)函数，将后台缓冲区复制到任何头的前端缓冲区。 此调用绝不会将后台缓冲区从一个头复制到另一个头的前端缓冲区。
    -   运行时可以在任何 head 上调用驱动程序的[*DdGetScanLine*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getscanline)函数，因为此调用与监视器的状态相关，而不与 Direct3D 上下文相关。
    -   运行时可以对任何头的后台缓冲区调用驱动程序的[*DdLock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)函数。

    应用程序可以为每个头分配一个 Z 缓冲区，也可以分配一个 Z 缓冲区以便按顺序使用每个头。 在前一种情况下，运行时调用驱动程序的[*DdCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))函数，如步骤1中所述。 在后一种情况下，运行时仅对主头调用驱动程序的*DdCreateSurface*函数。 在这两种情况下，运行时都调用驱动程序的[**D3dCreateSurfaceEx**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)函数，以便为所有在组中都是唯一的 Z 缓冲区提供句柄。

 

 





