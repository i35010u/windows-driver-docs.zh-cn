---
title: 接收通知
description: 接收通知
ms.assetid: 852243b2-35b0-4c94-9b3b-9855ed1a678a
keywords:
- 通知 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5a800e8383a95d1992b9520e07a28d1bbedc777
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216938"
---
# <a name="receiving-notifications"></a>接收通知




 

操作系统通过调用 [*Dot11ExtIhvReceiveIndication*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication) 函数从本机802.11 微型端口驱动程序转发特定于 IHV 的指示。 有关驱动程序如何进行这种类型的指示的详细信息，请参阅 [特定于 IHV 的指示](/previous-versions/windows/hardware/wireless/ihv-specific-indications)。

调用 [*Dot11ExtIhvReceiveIndication*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication) 函数时，将向 *pvBuffer* 参数传递一个指向缓冲区的指针，该缓冲区包含由 IHV 定义的格式的数据。

 

 