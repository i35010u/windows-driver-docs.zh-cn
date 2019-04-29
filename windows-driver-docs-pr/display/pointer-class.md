---
title: 指针类
description: 指针类
ms.assetid: c988535a-d218-48de-bdc2-56a620bbe4a2
keywords:
- 指针类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 969e92d6642e483a9e4f57f0fc262cf847e1f6c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358447"
---
# <a name="pointer-class"></a>指针类


Windows 显示器驱动程序模型 (WDDM) 不允许为一个指针类函数的调用可重入的方式。 它最，一个线程可以运行中的以下函数之一在给定时间：

-   [*DxgkDdiSetPointerPosition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointerposition)

-   [*DxgkDdiSetPointerShape*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_setpointershape)

 

 





