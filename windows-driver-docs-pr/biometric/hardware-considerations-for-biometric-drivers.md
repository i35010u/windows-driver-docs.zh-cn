---
title: 生物识别驱动程序的硬件注意事项
description: 生物识别驱动程序的硬件注意事项
ms.assetid: 07b16cfb-d3aa-4458-b6e3-acb76afe9b19
keywords:
- 生物识别驱动程序 WDK，硬件注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6078cc591e97111c05150c36511d7c013d3143
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522173"
---
# <a name="hardware-considerations-for-biometric-drivers"></a>生物识别驱动程序的硬件注意事项


使用 WBDI 框架的生物识别设备应满足以下要求：

-   基于 WBDI 的驱动程序应遵循[说明 0010 准则](https://go.microsoft.com/fwlink/p/?linkid=26140)终端服务重定向。

    此要求规定在设备和其驱动程序必须通过即插即用设备重定向框架支持通过终端服务会话重定向。

-   生物识别设备应具有足够大，缓存中完整功能完全扫描，并挂起模式的内部缓冲区。

    更大的缓冲区大小可能意味着较少的依赖关系以及在系统恢复期间处理的扫描中处理的常规扫描期间的时间安排。

-   设备应该能够输入捕获模式，而无需额外的命令在扫描期间从主机使内部状态过渡。

 

 





