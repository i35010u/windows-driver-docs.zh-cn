---
title: 处理端口停用 PnP 事件
description: 处理端口停用 PnP 事件
ms.assetid: 0e3b10a7-5ab5-48e1-a5cc-c7bc6ce26410
keywords:
- 端口 WDK NDIS，即插即用事件通知
- NDIS 端口 WDK，即插即用事件通知
- 即插即用事件通知 WDK NDIS 端口
- 停用的即插即用事件 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bd47e09d1e1e783d6384e112096f06963ee8d45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568375"
---
# <a name="handling-the-port-deactivation-pnp-event"></a>处理端口停用 PnP 事件





过量驱动程序必须处理**NetEventPortDeactivation**微型端口驱动程序会停用的 NDIS 端口即插即用事件。 若要通知有关端口停用事件的基础驱动程序，NDIS 传播端口停用从基础的微型端口驱动程序的即插即用事件。

协议驱动程序完成端口停用的即插即用事件的处理之前，必须确保已完成所有未完成的 OID 请求和与端口相关联的发送请求。 协议驱动程序完成即插即用事件后，该驱动程序必须确保它不会发出任何 OID 请求或该端口的发送请求。

微型端口驱动程序指定**NetEventPortDeactivation** PnP 中的事件代码[ **NET\_PNP\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff568752)结构的*NetPnPEvent*参数对的调用中指向[ **NdisMNetPnPEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563616)报表的某些端口已被函数停用。 微型端口驱动程序指定数组的 NDIS\_端口\_数字值，若要列出的已停用的端口。 有关数组的端口号的详细信息，请参阅[Deactivating NDIS 端口](deactivating-an-ndis-port.md)。

 

 





