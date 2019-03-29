---
title: 802.11 WLAN 适配器移除
description: 802.11 WLAN 适配器移除
ms.assetid: 2181d284-7987-48db-b7a4-d1296d8313ed
keywords:
- 适配器 WDK 802.11 WLAN，删除
- WLAN 适配器 WDK，删除
- 删除 WLAN 适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abfa024708dfd0713da3120bc44f88f258cb142d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575620"
---
# <a name="80211-wlan-adapter-removal"></a>802.11 WLAN 适配器移除




 

删除或禁用操作系统调用无线 LAN (WLAN) 适配器时[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)通知适配器的删除 IHV 扩展 DLL。 操作系统还会调用*Dot11ExtIhvDeinitAdapter*函数为每个适配器之前的操作系统卸载该 DLL 由 IHV 扩展 DLL。

当[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)是调用，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须释放 WLAN 适配器的任何已分配的资源。 具体而言，所有内存都分配通过调用[ **Dot11ExtAllocateBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff547419)必须通过调用释放[ **Dot11ExtFreeBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff547422).

-   操作系统引用 WLAN 适配器将不再有效时使用的句柄[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)调用。 操作系统将其句柄传递给通过 IHV 扩展 DLL *hDot11SvcHandle*参数时[ *Dot11ExtIhvInitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547469)调用。

    在调用*Dot11ExtIhvDeinitAdapter*函数，并从调用返回之后, DLL 未时必须使用句柄值调用任何 IHV 扩展性函数声明*hDot11SvcHandle*参数，如[ **Dot11ExtSendPacket**](https://msdn.microsoft.com/library/windows/hardware/ff547563)。

-   如果 IHV 扩展 DLL 具有一个挂起的预关联操作，这通过调用启动[ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499) IHV 处理程序函数，操作系统方面操作为已取消通过调用[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)函数。 在调用中 DLL 必须在内部取消预关联操作，但不能调用[ **Dot11ExtPreAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547538)完成预关联操作。

    有关预关联操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   如果 IHV 扩展 DLL 具有挂起的后期关联操作，通过调用已启动[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492) IHV 处理程序函数，操作系统取消通过调用该操作[ *Dot11ExtIhvStopPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547521)函数调用之前[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452).

    有关后关联操作的详细信息，请参阅[后期关联操作](post-association-operations.md)。

-   操作系统调用[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)函数为每个适配器之前的操作系统卸载该 DLL 由 IHV 扩展 DLL。 在此情况下，操作系统将调用[ *Dot11ExtIhvDeinitService* ](https://msdn.microsoft.com/library/windows/hardware/ff547457) IHV 处理程序函数后通过调用已暂停了最后一个 WLAN 适配器*Dot11ExtIhvDeinitAdapter*。

    有关此操作的详细信息，请参阅[DLL 停止操作](dll-stop-operations.md)。

 

 





