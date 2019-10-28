---
title: GPU 计划程序类
description: GPU 计划程序类
ms.assetid: 39d38787-588d-483b-9b36-14a3bc16df7c
keywords:
- GPU 计划程序类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 752a168d0ed4dc6cd43130d353281c4196c6cc0b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838928"
---
# <a name="gpu-scheduler-class"></a>GPU 计划程序类


Windows 显示驱动程序模型（WDDM）不允许以可重入方式调用某个 GPU 计划程序加载器类函数。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

-   [*DxgkDdiBuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)

-   [*DxgkDdiPatch*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)

-   [*DxgkDdiPreemptCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_preemptcommand)

-   [*DxgkDdiSubmitCommand*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)

 

 





