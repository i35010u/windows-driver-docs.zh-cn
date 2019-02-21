---
title: RS-232 端口上的 Plug and Play 串行设备中删除
description: RS-232 端口上的 Plug and Play 串行设备中删除
ms.assetid: a9019445-3013-49b2-94fd-1ab8a85c3d7a
keywords:
- RS-232 端口 WDK 串行设备
- Serenum 驱动程序 WDK，插设备
- 即插即用串行设备 WDK
- 串行设备 WDK，插
- 删除插设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64492606b8f580092d74d96175b1d7e2b7aafc53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541550"
---
# <a name="removing-a-plug-and-play-serial-device-on-an-rs-232-port"></a>RS-232 端口上的 Plug and Play 串行设备中删除





插管理器删除串行设备的删除请求发送到串行设备堆栈的顶部。 Serenum 收到串行设备的删除请求后，它会删除设备的 PDO，完成请求。 Serenum 不会向 RS-232 端口堆栈传递请求，因为 RS-232 端口是父设备中删除的串行设备。

 

 




