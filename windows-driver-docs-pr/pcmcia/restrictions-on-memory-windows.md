---
title: Windows 上的内存限制
description: Windows 上的内存限制
keywords:
- PCMCIA WDK 总线，内存窗口
- 内存 Windows WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7988910661dd444d6735ce589aae943f6fbf09a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812485"
---
# <a name="restrictions-on-memory-windows"></a>Windows 上的内存限制





本部分介绍了 Windows 2000 和更高版本的 Windows 和更高版本的操作系统在 PCMCIA 内存卡的内存窗口中的限制。

PCMCIA 内存卡的资源要求通常由总线驱动程序在即插即用 manager 请求枚举设备时指定。 还可以在设备驱动程序的 INF 文件的 [**Inf DDInstall. LogConfigOverride 部分**](../install/inf-ddinstall-logconfigoverride-section.md) 中指定特定内存窗口。 PCMCIA 内存卡最多可请求两个内存窗口。

 

