---
title: 通过永久内存窗口访问内存
description: 通过永久内存窗口访问 PCMCIA 属性内存
keywords:
- 属性内存 WDK PCMCIA 总线，永久分配内存窗口
- 永久性内存窗口 WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c716c3045daf6cfdae8b30d48f48bdc3064a636b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812521"
---
# <a name="access-pcmcia-attribute-memory-through-a-permanent-memory-window"></a>通过永久内存窗口访问 PCMCIA 属性内存





本部分介绍如何使用永久性分配的内存窗口来访问属性内存。

驱动程序应使用此方法来支持在属性内存中实现设备寄存器的 PCMCIA 设备。 在这种情况下，驱动程序的 ISR 通常需要在 IRQL DIRQL 运行时快速直接访问设备寄存器。

驱动程序在以 IRQL DIRQL 运行时可以使用此方法。

安装程序和即插即用管理器支持 [**INF DDInstall. LogConfigOverride 部分**](../install/inf-ddinstall-logconfigoverride-section.md)，该部分可强制即插即用管理器使用 **PcCardConfig** 项中指定的资源。 **LogConfigOverride** 节指定包含 **PcCardConfig** 条目的日志配置节。 **PcCardConfig** 项中的字段指定所需的内存资源，内存资源用于属性内存。

 

