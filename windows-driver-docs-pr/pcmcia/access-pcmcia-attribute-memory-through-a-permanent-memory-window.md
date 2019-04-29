---
title: 访问内存通过永久内存窗口
description: 通过永久内存窗口访问 PCMCIA 属性内存
ms.assetid: 866851b9-8e39-4480-9f22-dc2a2eb80ce0
keywords:
- 属性内存 WDK PCMCIA 总线，永久分配的内存窗口
- 永久内存窗口 WDK PCMCIA 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49e8abfe5a1cffe684580cc30607f967abf28ebd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391575"
---
# <a name="access-pcmcia-attribute-memory-through-a-permanent-memory-window"></a>通过永久内存窗口访问 PCMCIA 属性内存





本部分介绍如何 PC 卡或 CardBus 卡驱动程序可以使用永久分配的内存窗口访问属性内存。

驱动程序应使用此方法以支持 PCMCIA 设备可实现属性内存中的设备注册。 在这种情况下，驱动程序的 ISR 通常 IRQL DIRQL 在运行时需要设备注册快速直接访问。

IRQL DIRQL 在运行时，驱动程序可以使用此方法。

安装程序和插管理器支持[ **INF DDInstall.LogConfigOverride 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547339)，这可以强制即插即用和播放使用资源管理器中指定**PcCardConfig**条目。 **LogConfigOverride**部分指定包含的日志配置节**PcCardConfig**条目。 中的字段**PcCardConfig**条目指定所需的内存资源，并为属性内存使用的内存资源。

 

 





