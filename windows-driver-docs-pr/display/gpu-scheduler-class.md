---
title: GPU 计划程序类
description: GPU 计划程序类
ms.assetid: 39d38787-588d-483b-9b36-14a3bc16df7c
keywords:
- GPU 计划程序类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c203c7e97016a344d92f3f85661e21c0ce68eff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520972"
---
# <a name="gpu-scheduler-class"></a>GPU 计划程序类


Windows 显示器驱动程序模型 (WDDM) 不允许为一个 GPU 计划程序加载程序类函数的调用可重入的方式。 它最，一个线程可以运行中的以下函数之一在给定时间：

-   [*DxgkDdiBuildPagingBuffer*](https://msdn.microsoft.com/library/windows/hardware/ff559587)

-   [*DxgkDdiPatch*](https://msdn.microsoft.com/library/windows/hardware/ff559737)

-   [*DxgkDdiPreemptCommand*](https://msdn.microsoft.com/library/windows/hardware/ff559741)

-   [*DxgkDdiSubmitCommand*](https://msdn.microsoft.com/library/windows/hardware/ff560790)

 

 





