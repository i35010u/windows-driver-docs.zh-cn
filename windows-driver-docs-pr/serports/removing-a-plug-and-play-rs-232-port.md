---
title: 删除插 RS-232 端口
description: 删除插 RS-232 端口
ms.assetid: b439dc51-09f2-4149-a562-2e376bb504c5
keywords:
- RS-232 端口 WDK 串行设备
- Serenum 驱动程序 WDK，插设备
- 即插即用串行设备 WDK
- 串行设备 WDK，插
- 删除 RS-232 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ea89439b59d7b1f35b1f7d3194e3e0ed5403af2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534495"
---
# <a name="removing-a-plug-and-play-rs-232-port"></a>删除插 RS-232 端口





插管理器中的删除请求发送到 RS-232 端口堆栈的顶部移除 RS-232 端口。 Serenum 传递设备堆栈的下层请求、 在端口堆栈中移除筛选器执行操作和删除关联的 PDO，如果存在一个。 删除 RS-232 端口还会删除串行设备连接到端口。

 

 




