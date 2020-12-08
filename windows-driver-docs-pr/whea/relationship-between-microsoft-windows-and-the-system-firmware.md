---
title: Microsoft Windows 和系统固件之间的关系
description: Microsoft Windows 和系统固件之间的关系
keywords:
- Windows 硬件错误体系结构 WDK、Windows 和固件
- WHEA WDK、Windows 和固件
- 硬件错误 WDK WHEA、Windows 和固件
- 错误 WDK WHEA、Windows 和固件
- 固件 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 185fbb5228fb0e19c21612bc24006d2c8247f0c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832039"
---
# <a name="relationship-between-microsoft-windows-and-the-system-firmware"></a>Microsoft Windows 和系统固件之间的关系


Microsoft Windows 操作系统和系统固件在硬件错误处理中扮演着重要的角色。 Windows 硬件错误体系结构 (WHEA) 改善了两种方法，这些方法可影响硬件错误处理的任务。 通过 WHEA，硬件平台供应商可以确定固件或操作系统是否拥有关键的硬件错误资源。 此外，通过 WHEA，固件可以在适当的时候将硬件错误资源的控制权传递给操作系统。

操作系统应该拥有尽可能多的硬件错误资源。 但是，由于缺少硬件错误资源标准化，系统固件必须继续管理其中一些资源。 随着越来越多的硬件错误报告标准的定义和采用，Microsoft 相信，可以将更多的硬件错误处理机制置于操作系统控制之下。

 

 




