---
title: 接收通知
description: 接收通知
ms.assetid: 852243b2-35b0-4c94-9b3b-9855ed1a678a
keywords:
- 通知 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 567766b766b06467ff7c4bb875b54fc1ca4bbe5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842103"
---
# <a name="receiving-notifications"></a>接收通知




 

操作系统通过调用[*Dot11ExtIhvReceiveIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication)函数从本机802.11 微型端口驱动程序转发特定于 IHV 的指示。 有关驱动程序如何进行这种类型的指示的详细信息，请参阅[特定于 IHV 的指示](ihv-specific-indications.md)。

调用[*Dot11ExtIhvReceiveIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication)函数时，将向*pvBuffer*参数传递一个指向缓冲区的指针，该缓冲区包含由 IHV 定义的格式的数据。

 

 





