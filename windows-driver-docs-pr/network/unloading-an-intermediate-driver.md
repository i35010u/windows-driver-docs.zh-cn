---
title: 卸载中间驱动程序
description: 卸载中间驱动程序
keywords:
- NDIS 中间驱动程序 WDK，卸载
- 中间驱动程序 WDK 网络，卸载
- 卸载中间驱动程序
- 安装或卸载 WDK NDIS 中间安装后进行清理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cc102b9d937e65ac05d484f66332149a5e4f787
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839419"
---
# <a name="unloading-an-intermediate-driver"></a>卸载中间驱动程序





NDIS 调用 [*MiniportDriverUnload*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload) 函数来卸载中间驱动程序。 中间驱动程序必须在 *MiniportDriverUnload* 中执行与其他微型端口驱动程序相同的操作。 除了调用 [**NdisMDeregisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) 函数外，中间驱动程序还会调用 [**NdisDeregisterProtocolDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver)。 *MiniportDriverUnload* 还应执行任何必要的清理操作，如解除分配任何协议驱动程序资源。

若要在卸载中间驱动程序之前执行清理操作，中间驱动程序可以注册 [*ProtocolUninstall*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_uninstall) 函数。 例如，中间驱动程序的协议下边缘可能需要 *ProtocolUninstall* 函数。 中间驱动程序可以在 NDIS 调用其 *MiniportDriverUnload* 函数之前，释放其在 *ProtocolUninstall* 中的协议边缘资源。

微型端口中间驱动程序调用 **NdisMDeregisterMiniportDriver** 两次，一次针对其物理设备接口，并再次用于虚拟设备接口。

 

