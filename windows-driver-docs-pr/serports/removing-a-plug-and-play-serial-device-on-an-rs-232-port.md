---
title: 删除 RS-232 端口上的即插即用串行设备
description: 删除 RS-232 端口上的即插即用串行设备
keywords:
- RS-232 端口 WDK 串行设备
- Serenum driver WDK，即插即用设备
- 即插即用串行设备 WDK
- 串行设备 WDK，即插即用
- 删除即插即用设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b730147ef07734f4d9b412e32d60183c5d0485e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804981"
---
# <a name="removing-a-plug-and-play-serial-device-on-an-rs-232-port"></a>删除 RS-232 端口上的即插即用串行设备





即插即用 manager 通过将删除请求发送到串行设备堆栈的顶部来删除串行设备。 Serenum 收到串行设备的删除请求后，它会删除设备的 PDO 并完成请求。 Serenum 不会将请求传递给 RS-232 端口堆栈，因为 RS-232 端口是已删除的串行设备的父设备。

 

 




