---
title: 使用状态刷新回调函数
description: 使用状态刷新回调函数
ms.assetid: fadd2edb-776b-4ef1-b663-cc004522f8ae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 328ec8fafc9fe67614c644e1e045f2bea263e3f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377371"
---
# <a name="using-the-state-refresh-callback-functions"></a>使用状态刷新回调函数


用户模式显示驱动程序可以使用[Direct3D 运行时版本 10 状态刷新回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)要实现无状态的驱动程序或者构建命令缓冲区前导码数据。

Direct3D 运行时会提供在其状态刷新回调函数的指针[ **D3D10DDI\_CORELAYER\_DEVICECALLBACKS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddi_corelayer_devicecallbacks)结构**pUMCallbacks**的成员[ **D3D10DDIARG\_CREATEDEVICE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)结构在调用指向[ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)函数。

用户模式显示驱动程序可能会调用，例如， [ **pfnStateIaIndexBufCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_state_ia_indexbuf_cb)状态刷新回调函数，该驱动程序时，驱动程序的调用中[ **IaSetIndexBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_ia_setindexbuffer)函数。 此调用是很有可能，特别是因为用户模式显示驱动程序可能会使用**pfnStateIaIndexBufCb**构建一个前导码和调用的回调函数*IaSetIndexBuffer*可能用完可用抵命令缓冲区的大小，并导致刷新。 此类情况下，调用**pfnStateIaIndexBufCb**将同一"新"的绑定信息作为对原始调用传递*IaSetIndexBuffer*。 这种情况下会导致更优的前导码。

 

 





