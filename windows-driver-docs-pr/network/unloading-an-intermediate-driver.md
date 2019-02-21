---
title: 卸载中间驱动程序
description: 卸载中间驱动程序
ms.assetid: e3c1dad4-4262-4449-8dcd-2e2f5d6c8e25
keywords:
- NDIS 中间层驱动程序 WDK，卸载
- 驱动程序 WDK 的中间连接网络、 卸载
- 正在卸载中间驱动程序
- 清理后安装或卸载 WDK NDIS 中间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7e81ce362d82f746476f9db8fa277cf080bf8bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541029"
---
# <a name="unloading-an-intermediate-driver"></a>卸载中间驱动程序





NDIS 调用[ *MiniportDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff559378)函数以卸载中间驱动程序。 中间驱动程序必须执行中的相同操作*MiniportDriverUnload*作为其他微型端口驱动程序。 除了调用[ **NdisMDeregisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563578)函数，中间驱动程序还会调用[ **NdisDeregisterProtocolDriver**](https://msdn.microsoft.com/library/windows/hardware/ff561743). *MiniportDriverUnload*还应执行任何必要的清理操作，例如正在解除分配的任何协议驱动程序资源。

若要卸载中间驱动程序之前，请执行清理操作，中间驱动程序可以注册[ *ProtocolUninstall* ](https://msdn.microsoft.com/library/windows/hardware/ff570279)函数。 例如，可能需要中间驱动程序的协议下边缘*ProtocolUninstall*函数。 中间驱动程序可以释放在其协议边缘资源*ProtocolUninstall* NDIS 调用前其*MiniportDriverUnload*函数。

中间微型端口驱动程序调用**NdisMDeregisterMiniportDriver**两次，一次针对其物理设备接口，再次其虚拟设备接口。

 

 





