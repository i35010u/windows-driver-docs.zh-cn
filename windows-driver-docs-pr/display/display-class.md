---
title: 显示类
description: 在线程和同步第一级别中显示类 DDIs。
ms.assetid: 439263ec-b28f-41ca-9c69-095216d63f38
keywords:
- 显示驱动程序 WDK 窗口，显示类
- 线程和同步优先级别
ms.date: 04/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62ff92b01e0b0ca6d0cba3516d61faa177813b3e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838994"
---
# <a name="display-class"></a>显示类

Windows 显示驱动程序模型（WDDM）不允许以可重入方式调用某个显示类函数。 这就是，在给定时间，一个线程最多可以在下列函数之一中运行：

-   [*DxgkDdiSetTargetGamma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetgamma)

-   [*DxgkDdiSetTargetContentType*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetcontenttype)

-   [*DxgkDdiSetTargetAnalogCopyProtection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_settargetanalogcopyprotection)

-   [*DxgkDdiSetTargetAdjustedColorimetry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_settargetadjustedcolorimetry)
