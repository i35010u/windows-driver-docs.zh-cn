---
title: 接收通知
description: 接收通知
ms.assetid: 852243b2-35b0-4c94-9b3b-9855ed1a678a
keywords:
- 通知 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c97b6fd40e8b8f5b977ca10527c93b51bb8cccaa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385421"
---
# <a name="receiving-notifications"></a>接收通知




 

操作系统将通过调用转发从本机 802.11 微型端口驱动程序的特定于 IHV 的迹象[ *Dot11ExtIhvReceiveIndication* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_indication)函数。 有关如何驱动程序将指示此类型的详细信息，请参阅[IHV 特定指示](ihv-specific-indications.md)。

当[ *Dot11ExtIhvReceiveIndication* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_indication)调用函数时， *pvBuffer*参数传递给包含 IHV 定义的格式中的数据的缓冲区的指针。

 

 





