---
title: 802.11 WLAN 适配器重置
description: 802.11 WLAN 适配器重置
ms.assetid: 1f993977-b4a1-42ec-8de3-2f4855db93a7
keywords:
- WDK 802.11 WLAN 适配器重置
- WLAN 适配器 WDK，重置
- 重置 WLAN 适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b2d432301a48e205aa7b662157fd54d8f722cba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575627"
---
# <a name="80211-wlan-adapter-reset"></a>802.11 WLAN 适配器重置




 

操作系统调用[ *Dot11ExtIhvAdapterReset* ](https://msdn.microsoft.com/library/windows/hardware/ff547434)只要有必要还原到其已初始化状态的无线 LAN (WLAN) 适配器。 出现以下事件之一时，操作系统将调用此函数。

-   将 WLAN 适配器执行断开连接操作。 有关此操作的详细信息，请参阅[断开连接操作](disconnection-operations.md)。

-   操作系统将本机 802.11 微型端口驱动程序，它管理的适配器，通过设置请求的重置[OID\_DOT11\_重置\_请求](https://msdn.microsoft.com/library/windows/hardware/ff569409)。

当[ *Dot11ExtIhvAdapterReset* ](https://msdn.microsoft.com/library/windows/hardware/ff547434)是调用，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须将其状态还原到相同的状态后处于[ *Dot11ExtIhvInitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547469)调用函数。 DLL 将 WLAN 适配器上配置专用设置，则其必须还原到它们后所处的相同状态的这些设置*Dot11ExtIhvInitAdapter*调用。

-   如果 IHV 扩展 DLL 具有一个挂起的预关联操作，这通过调用启动[ *Dot11ExtIhvPerformPreAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547499) IHV 处理程序函数，必须调用 DLL [**Dot11ExtPreAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547538)取消该操作。 在此情况下，设置 DLL *dwWin32Error*的参数**Dot11ExtPreAssociateCompletion**错误\_已取消。

    有关预关联操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   如果 DLL 具有挂起的后期关联操作，通过调用已启动[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492) IHV 处理程序函数，必须调用 DLL [ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)取消该操作。 在此情况下，设置 DLL *dwWin32Error*的参数**Dot11ExtPostAssociateCompletion**错误\_已取消。

    有关后关联操作的详细信息，请参阅[后期关联操作](post-association-operations.md)。

 

 





