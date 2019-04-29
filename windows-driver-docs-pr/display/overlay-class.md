---
title: 覆盖类
description: 覆盖类
ms.assetid: 698eb8af-ff9a-4c11-b764-6e5773886aaa
keywords:
- 覆盖类 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82cb57a4a957ab75a5de2efc53946a2f86b34c22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358343"
---
# <a name="overlay-class"></a>覆盖类


Windows 显示器驱动程序模型 (WDDM) 不允许为一个覆盖类函数的调用可重入的方式。 它最，一个线程可以运行中的以下函数之一在给定时间：

-   [*DxgkDdiCreateOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559616)

-   [*DxgkDdiDestroyOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559642)

-   [*DxgkDdiFlipOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff559655)

-   [*DxgkDdiUpdateOverlay*](https://msdn.microsoft.com/library/windows/hardware/ff560804)

 

 





