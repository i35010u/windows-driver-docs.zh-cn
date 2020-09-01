---
title: 卸载中间驱动程序
description: 卸载中间驱动程序
ms.assetid: e3c1dad4-4262-4449-8dcd-2e2f5d6c8e25
keywords:
- NDIS 中间驱动程序 WDK，卸载
- 中间驱动程序 WDK 网络，卸载
- 卸载中间驱动程序
- 安装或卸载 WDK NDIS 中间安装后进行清理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc9224cc86f0ef284dc787b7c30c6281d475537a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214304"
---
# <a name="unloading-an-intermediate-driver"></a>卸载中间驱动程序





NDIS 调用 [*MiniportDriverUnload*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload) 函数来卸载中间驱动程序。 中间驱动程序必须在 *MiniportDriverUnload* 中执行与其他微型端口驱动程序相同的操作。 除了调用 [**NdisMDeregisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) 函数外，中间驱动程序还会调用 [**NdisDeregisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver)。 *MiniportDriverUnload* 还应执行任何必要的清理操作，如解除分配任何协议驱动程序资源。

若要在卸载中间驱动程序之前执行清理操作，中间驱动程序可以注册 [*ProtocolUninstall*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_uninstall) 函数。 例如，中间驱动程序的协议下边缘可能需要 *ProtocolUninstall* 函数。 中间驱动程序可以在 NDIS 调用其*MiniportDriverUnload*函数之前，释放其在*ProtocolUninstall*中的协议边缘资源。

微型端口中间驱动程序调用 **NdisMDeregisterMiniportDriver** 两次，一次针对其物理设备接口，并再次用于虚拟设备接口。

 

