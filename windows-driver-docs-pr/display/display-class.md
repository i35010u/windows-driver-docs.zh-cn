---
title: 显示类
description: 类 DDIs 显示线程处理和同步的第一个级别中。
ms.assetid: 439263ec-b28f-41ca-9c69-095216d63f38
keywords:
- 显示驱动程序 WDK Windows，显示类
- 线程处理和同步的第一个级别
ms.date: 04/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 33102ec6c3443929e4b18c6e26d8139376749522
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522231"
---
# <a name="display-class"></a>显示类

Windows 显示驱动程序模型 (WDDM) 不允许为一个显示类函数的调用可重入的方式。 它最，一个线程可以运行中的以下函数之一在给定时间：

-   [*DxgkDdiSetTargetGamma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetgamma)

-   [*DxgkDdiSetTargetContentType*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetcontenttype)

-   [*DxgkDdiSetTargetAnalogCopyProtection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetanalogcopyprotection)

-   [*DxgkDdiSetTargetAdjustedColorimetry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_settargetadjustedcolorimetry)
