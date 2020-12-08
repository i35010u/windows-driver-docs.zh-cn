---
title: 接收通知
description: 接收通知
keywords:
- 通知 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c76fd5c7c74c31d739417dd314be976fda0903c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782177"
---
# <a name="receiving-notifications"></a>接收通知




 

操作系统通过调用 [*Dot11ExtIhvReceiveIndication*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication) 函数从本机802.11 微型端口驱动程序转发特定于 IHV 的指示。 有关驱动程序如何进行这种类型的指示的详细信息，请参阅 [特定于 IHV 的指示](/previous-versions/windows/hardware/wireless/ihv-specific-indications)。

调用 [*Dot11ExtIhvReceiveIndication*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication) 函数时，将向 *pvBuffer* 参数传递一个指向缓冲区的指针，该缓冲区包含由 IHV 定义的格式的数据。

 

 
