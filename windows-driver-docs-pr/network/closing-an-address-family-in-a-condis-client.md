---
title: 关闭 CoNDIS 客户端中的地址系列
description: 关闭 CoNDIS 客户端中的地址系列
keywords:
- 客户端关闭的 AFs WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27c86ae4b3831a9993d98b9cc0ff043cc95d0687
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817627"
---
# <a name="closing-an-address-family-in-a-condis-client"></a>关闭 CoNDIS 客户端中的地址系列





若要关闭 AFs，CoNDIS 客户端必须提供 [**ProtocolClNotifyCloseAf**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_notify_close_af) 函数。 独立调用管理器或 MCM 分别调用 [**NdisCmNotifyCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmnotifycloseaddressfamily)函数或 [**NdisMCmNotifyCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmnotifycloseaddressfamily)函数时，NDIS 调用 *ProtocolClNotifyCloseAf* 。

在 *ProtocolClNotifyCloseAf* 中，客户端完成关闭指定的 AF，或返回 NDIS \_ 状态 \_ "挂起" 并调用 [**NdisClNotifyCloseAddressFamilyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclnotifycloseaddressfamilycomplete) 函数以完成操作。 客户端调用 **NdisClNotifyCloseAddressFamilyComplete** 后，NDIS 会调用 [**ProtocolCmNotifyCloseAfComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_notify_close_af_complete) 函数来通知调用管理器客户端关闭了 AF。

若要关闭 AF，客户端应：

1.  如果客户端具有活动的 multipoint 连接，则根据需要调用 [**NdisClDropParty**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty) 函数多次，直到每个 multipoint 虚拟连接上只有一个参与方处于活动状态 (VC) 。

2.  尽可能多地调用 [**NdisClCloseCall**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall) 函数，以关闭仍处于打开状态且与地址族关联的所有调用。

3.  尽可能多地调用 [**NdisClDeregisterSap**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclderegistersap) 函数，以便取消注册 (sap) 的所有服务访问点，使客户端向调用管理器注册。

4.  调用 [**NdisClCloseAddressFamily**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily) 函数关闭 AF。

 

