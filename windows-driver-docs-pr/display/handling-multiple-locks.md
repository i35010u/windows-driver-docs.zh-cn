---
title: 处理多个锁
description: 处理多个锁
ms.assetid: d62b9577-d78f-431d-a5bf-c06c9be345c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d9a3c2be3abe614cb8b6f8187646bdc84157181
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839659"
---
# <a name="handling-multiple-locks"></a>处理多个锁


使用 Direct3D 运行时，可以允许顶点和索引缓冲区有多个未完成的锁。 用户模式显示驱动程序必须与[Windows 2000 显示驱动程序模型](windows-2000-display-driver-model-design-guide.md)中的运行时相同的方式处理多个锁。

对于已锁定的资源，用户模式显示驱动程序不能对其[**LockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lockasync)函数调用失败。 也就是说，在首次调用其*LockAsync*函数后，该驱动程序将无法通过对其*LockAsync*函数的任何调用成功地锁定该资源。 同样，驱动程序在第一次调用其*lock*函数后，对其[**lock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)函数的任何调用在锁定该资源的情况下将无法失败。 运行时通过调用驱动程序的[**UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)函数，使其对驱动程序的*LockAsync*函数进行的每个调用都匹配。 运行时还会将对驱动程序的*锁*函数所做的每个调用与对驱动程序的[**Unlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)函数的调用进行匹配。

用户模式显示驱动程序无法对其[**UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlockasync)函数进行调用，除非[**D3DDDIARG\_UnlockAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_unlockasync)结构描述的资源实际上未被先前对驱动*程序的调用*锁定才能. 同样，驱动程序也不能对[**解除锁定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_unlock)的函数进行调用，除非[ **\_D3DDDIARG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_unlock)的锁定结构所描述的资源实际被先前对驱动程序的*锁定*函数的调用锁定。 在以前未锁定资源的情况下， *UnlockAsync*和*Unlock*返回 E\_INVALIDARG。

 

 





