---
title: 删除即插即用 RS-232 端口
description: 删除即插即用 RS-232 端口
keywords:
- RS-232 端口 WDK 串行设备
- Serenum driver WDK，即插即用设备
- 即插即用串行设备 WDK
- 串行设备 WDK，即插即用
- 删除 RS-232 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dc66d4a9375b583b4f5abced0d8ffa1f15d5fef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811977"
---
# <a name="removing-a-plug-and-play-rs-232-port"></a>删除即插即用 RS-232 端口





即插即用 manager 通过向 RS-232 端口堆栈顶部发送删除请求来删除 RS-232 端口。 Serenum 向下传递请求，删除端口堆栈中的筛选器，并删除关联的 PDO （如果存在）。 删除 RS-232 端口还会删除连接到该端口的串行设备。

 

 




