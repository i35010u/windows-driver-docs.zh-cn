---
title: 访问 PCMCIA 设备的属性内存的要求
description: 访问 PCMCIA 设备的属性内存的要求
ms.assetid: 8af41eb0-c057-43c9-a50f-b7d88e1bed6a
keywords:
- 属性内存 WDK PCMCIA 总线，要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab5842d6563c014284cc57311aaaa2192af397df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566721"
---
# <a name="requirements-for-accessing-attribute-memory-of-a-pcmcia-device"></a>访问 PCMCIA 设备的属性内存的要求





本部分介绍以下类型的访问的属性的 PCMCIA 设备内存的要求：

<a href="" id="query-device-information"></a>**查询设备信息**  
驱动程序通常查询以下设备信息：

-   设备标识

-   设备参数，例如容量或驱动程序用于配置设备的速度

-   静态数据，如 MAC 地址

信息的查询将通常只读的并执行频率相对较低。

<a href="" id="configure-a-device"></a>**配置设备**  
某些驱动程序需要具有到配置注册表属性内存中的写入权限。

驱动程序通常很少会配置设备。

请注意 PCMCIA 总线驱动程序管理标准 PCMCIA 配置注册表属性内存中。 驱动程序必须向这些寄存器写入内容。 如果是这样，则可能出现无法预料的系统行为。 系统设置和插管理器支持 INF 文件指令-例如，则[ **INF LogConfig 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547448) -必须用于配置这些寄存器。

<a href="" id="operate-a-device"></a>**运行设备**  
某些 PCMCIA 设备使用控制寄存器位于属性内存中。 通常，驱动程序必须直接访问这些寄存器中 ISR. 此类型的访问可在频率相对较高，且需要快速直接内存访问。

 

 





