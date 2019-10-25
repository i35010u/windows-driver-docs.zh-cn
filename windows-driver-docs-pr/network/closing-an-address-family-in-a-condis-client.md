---
title: 关闭 CoNDIS 客户端中的地址系列
description: 关闭 CoNDIS 客户端中的地址系列
ms.assetid: 06e8128a-f3da-48f2-a045-6c4be5f85889
keywords:
- 客户端关闭的 AFs WDK CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a490fdb618858ba06a32cccce63e2a3d7bc4da6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838198"
---
# <a name="closing-an-address-family-in-a-condis-client"></a>关闭 CoNDIS 客户端中的地址系列





若要关闭 AFs，CoNDIS 客户端必须提供[**ProtocolClNotifyCloseAf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cl_notify_close_af)函数。 独立调用管理器或 MCM 分别调用[**NdisCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmnotifycloseaddressfamily)函数或[**NdisMCmNotifyCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmnotifycloseaddressfamily)函数时，NDIS 调用*ProtocolClNotifyCloseAf* 。

在*ProtocolClNotifyCloseAf*中，客户端完成关闭指定的 AF，或返回 NDIS\_状态\_挂起，并调用[**NdisClNotifyCloseAddressFamilyComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclnotifycloseaddressfamilycomplete)函数来完成操作。 客户端调用**NdisClNotifyCloseAddressFamilyComplete**后，NDIS 会调用[**ProtocolCmNotifyCloseAfComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_notify_close_af_complete)函数来通知调用管理器客户端关闭了 AF。

若要关闭 AF，客户端应：

1.  如果客户端具有活动的 multipoint 连接，则根据需要调用[**NdisClDropParty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscldropparty)函数多次，直到每个 multipoint 虚拟连接（VC）上只有一个参与方处于活动状态。

2.  尽可能多地调用[**NdisClCloseCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclclosecall)函数，以关闭仍处于打开状态且与地址族关联的所有调用。

3.  尽可能多地调用[**NdisClDeregisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclderegistersap)函数，以取消注册客户端向呼叫管理器注册的所有服务访问点（sap）。

4.  调用[**NdisClCloseAddressFamily**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclcloseaddressfamily)函数关闭 AF。

 

 





