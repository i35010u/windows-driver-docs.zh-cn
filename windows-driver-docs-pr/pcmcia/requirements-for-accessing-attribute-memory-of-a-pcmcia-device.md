---
title: 访问 PCMCIA 设备的属性内存的要求
description: 访问 PCMCIA 设备的属性内存的要求
keywords:
- 属性内存 WDK PCMCIA 总线，要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76955cf2df6f5d7e2eda8b588ea1ce40475605a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812489"
---
# <a name="requirements-for-accessing-attribute-memory-of-a-pcmcia-device"></a>访问 PCMCIA 设备的属性内存的要求





本部分介绍对 PCMCIA 设备的属性内存的以下访问类型的要求：

<a href="" id="query-device-information"></a>**查询设备信息**  
驱动程序通常会查询以下设备信息：

-   设备的标识

-   设备参数，如驱动程序用于配置设备的容量或速度

-   静态数据，如 MAC 地址

信息查询通常是只读的，并且会相对较少的执行。

<a href="" id="configure-a-device"></a>**配置设备**  
某些驱动程序要求对属性内存中的配置寄存器具有写入访问权限。

驱动程序通常不经常配置设备。

请注意，PCMCIA 总线驱动程序管理属性内存中的标准 PCMCIA 配置注册。 驱动程序不得写入这些寄存器。 如果出现这种情况，则可能会出现不可预知的系统行为。 系统设置和即插即用管理器支持 INF 文件指令（例如，必须使用 [**Inf LogConfig 指令**](../install/inf-logconfig-directive.md) 来配置这些寄存器）。

<a href="" id="operate-a-device"></a>**操作设备**  
某些 PCMCIA 设备使用属性内存中的控制寄存器。 驱动程序通常必须直接在 ISR 内访问这些寄存器。 此类访问权限的频率相对较高，需要快速的直接内存访问。

 

