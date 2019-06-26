---
title: 接收操作
description: 接收操作
ms.assetid: 9ec2ba38-36dd-42d2-b0a8-0abe4d1bb847
keywords:
- 接收操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c4bdf4b006a9f2fde7b2350905efd99d9f0b405
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368467"
---
# <a name="receive-operations"></a>接收操作




 

执行后关联操作时，通过调用发起[ *Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)，操作系统调用[ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)通过无线 LAN (WLAN) 适配器接收函数来将数据包转发到 HV 扩展 DLL。 有关后关联操作的详细信息，请参阅[后期关联操作](post-association-operations.md)。

若要接收数据包，IHV 扩展 DLL 必须调用[ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)注册一个或多个 IEEE EtherTypes 的列表。 使用此列表中的条目匹配 EtherType 收到数据包时，操作系统将调用[ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)函数，并将传递到函数的数据包缓冲区*pvInBuffer*参数。

**请注意**  IHV 扩展 DLL 必须调用[ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) DLL 完成预关联操作之前。 有关此操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

 

当[ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)调用时， *pvInBuffer*参数指向包含整个 802.11 数据包，操作系统分配的缓冲区其中包括媒体访问控制 (MAC) 标头、 LLC 封装 （如有必要） 和有效负载数据。

IHV 扩展 DLL 可以发送到在调用中从接收到的数据包的响应[ *Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)。 在此情况下，该 DLL 必须遵循中所述的准则[发送操作](send-operations.md)。

 

 





