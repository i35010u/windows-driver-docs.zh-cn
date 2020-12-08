---
title: 使用状态刷新回调函数
description: 使用状态刷新回调函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0451d4deabf520b316ac9fbc845512ece4035dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815433"
---
# <a name="using-the-state-refresh-callback-functions"></a>使用状态刷新回调函数


用户模式显示驱动程序可以使用 [Direct3D 运行时版本 10 State-Refresh 回调函数](/windows-hardware/drivers/ddi/index) 来实现无状态驱动程序或生成命令缓冲区前导数据。

Direct3D 运行时提供指向其状态刷新回调函数的指针，这些函数位于 [**D3D10DDI \_ CORELAYER \_ DEVICECALLBACKS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)结构中， [**D3D10DDIARG \_ CREATEDEVICE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构的 **pUMCallbacks** 成员在调用 [**CREATEDEVICE (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数时指向该函数。

例如，当驱动程序在对驱动程序的 [**IaSetIndexBuffer**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setindexbuffer)函数的调用中时，用户模式显示驱动程序可能会调用 [**pfnStateIaIndexBufCb**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ia_indexbuf_cb)状态刷新回调函数。 此调用是可能的，尤其是因为用户模式显示驱动程序可以使用 **pfnStateIaIndexBufCb** 回调函数来生成前导码，而对 *IaSetIndexBuffer* 的调用可能会耗尽命令缓冲区的大小并导致刷新。 对于这种情况，调用 **pfnStateIaIndexBufCb** 会传递与对 *IaSetIndexBuffer* 的原始调用相同的 "新" 绑定信息。 这种情况会导致更好的前导码。

 

