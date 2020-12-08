---
title: 生物识别驱动程序的硬件注意事项
description: 生物识别驱动程序的硬件注意事项
keywords:
- 生物识别驱动程序 WDK，硬件注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 064a590bf671f9576f33e3215ee79e294475dfd4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798627"
---
# <a name="hardware-considerations-for-biometric-drivers"></a>生物识别驱动程序的硬件注意事项


使用 WBDI 框架的生物识别设备应满足以下要求：

-   基于 WBDI 的驱动程序应遵循终端服务重定向的 [DEVFUND-0010 指导原则](/windows-hardware/test/hlk/) 。

    此要求表明设备及其驱动程序必须支持通过 PnP 设备重定向框架通过终端服务会话重定向。

-   生物识别设备应该具有足够大的内部缓冲区，以便缓存完全电源和挂起模式下的完全扫描。

    较大的缓冲区大小可能意味着在常规扫描处理期间依赖时间更少，在系统恢复过程中，还可以扫描处理。

-   设备应能够进入捕获模式并在扫描过程中进行内部状态转换，而无需主机的额外命令。

 

