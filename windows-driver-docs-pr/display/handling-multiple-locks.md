---
title: 处理多个锁
description: 处理多个锁
ms.assetid: d62b9577-d78f-431d-a5bf-c06c9be345c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a497b7b1047d99ed757a8cee62b43d852563be02
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359337"
---
# <a name="handling-multiple-locks"></a>处理多个锁


使用 Direct3D 的运行时，您可以允许具有多个锁未完成的顶点和索引缓冲区。 用户模式显示驱动程序必须处理多个锁中的运行时一样[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)。

用户模式显示驱动程序不得失败调用其[ **LockAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)函数已被锁定的资源。 也就是说，驱动程序不能故障对任何调用其*LockAsync*后第一次调用函数的特定资源及其*LockAsync*函数成功锁定该资源。 同样，该驱动程序不能故障对任何调用其[**锁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)后第一次调用函数的特定资源及其*锁*函数成功锁定，资源。 在运行时匹配对驱动程序的每次调用*LockAsync*驱动程序的调用函数[ **UnlockAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)函数。 在运行时还将匹配对驱动程序的每次调用*锁*驱动程序的调用函数[**解锁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)函数。

用户模式显示驱动程序不能故障调用其[ **UnlockAsync** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)作用，除非该资源的[ **D3DDDIARG\_UNLOCKASYNC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_unlockasync)结构描述实际上未被该驱动程序的以前调用锁定*LockAsync*函数。 同样，该驱动程序不能故障调用其[**解锁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)作用，除非该资源的[ **D3DDDIARG\_解锁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_unlock)结构描述实际上未被该驱动程序的以前调用锁定*锁*函数。 在其中资源被不以前锁定的情况下*UnlockAsync*并*解锁*返回 E\_INVALIDARG。

 

 





