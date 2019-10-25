---
title: 使用状态刷新回调函数
description: 使用状态刷新回调函数
ms.assetid: fadd2edb-776b-4ef1-b663-cc004522f8ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e88c4be26f1108e8e841a1c92b2a63ff6db5e3b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825365"
---
# <a name="using-the-state-refresh-callback-functions"></a>使用状态刷新回调函数


用户模式显示驱动程序可以使用[Direct3D 运行时版本10状态刷新回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)来实现无状态驱动程序或生成命令缓冲区前导数据。

Direct3D 运行时提供指向其状态刷新回调函数的指针，这些函数位于 D3D10DDIARG 的**pUMCallbacks**成员的[**D3D10DDI\_CORELAYER\_DEVICECALLBACKS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)结构中[ **\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构指向对[**CreateDevice （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数的调用中的。

例如，当驱动程序在对驱动程序的[**IaSetIndexBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setindexbuffer)函数的调用中时，用户模式显示驱动程序可能会调用[**pfnStateIaIndexBufCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ia_indexbuf_cb)状态刷新回调函数。 此调用是可能的，尤其是因为用户模式显示驱动程序可以使用**pfnStateIaIndexBufCb**回调函数构建前导码，而对*IaSetIndexBuffer*的调用可能会耗尽命令缓冲区的大小，导致平. 对于这种情况，调用**pfnStateIaIndexBufCb**会传递与对*IaSetIndexBuffer*的原始调用相同的 "新" 绑定信息。 这种情况会导致更好的前导码。

 

 





