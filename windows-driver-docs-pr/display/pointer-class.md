---
title: 指针类
description: 指针类
ms.assetid: c988535a-d218-48de-bdc2-56a620bbe4a2
keywords:
- 指针类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17075ddeae45ba9c361bc55feef9d821777f8eee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829784"
---
# <a name="pointer-class"></a>指针类


Windows 显示驱动程序模型（WDDM）不允许以可重入方式调用某个指针类函数。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

-   [*DxgkDdiSetPointerPosition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointerposition)

-   [*DxgkDdiSetPointerShape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointershape)

 

 





