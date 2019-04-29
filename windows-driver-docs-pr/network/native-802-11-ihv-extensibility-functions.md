---
title: 本机 802.11 IHV 扩展性函数
description: 本部分介绍为本机 802.11 IHV 扩展 DLL 的本机 802.11 IHV 扩展性函数
keywords:
- 本机 802.11 IVH 扩展性函数
- 本机 802.11 IHV 扩展 DLL 可扩展性函数
- WDK 本机 802.11 IVH 扩展性函数
ms.assetid: 0E7CC153-5434-459D-9773-8CCAFBACD016
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f6fcbe43c6bce7fc63bbae4bed1cb7923851124
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382629"
---
# <a name="native-80211-ihv-extensibility-functions"></a>本机 802.11 IHV 扩展性函数

> [!IMPORTANT]
> [本机 802.11 无线 LAN](native-802-11-wireless-lan4.md)接口已弃用 Windows 10 及更高版本。 请改为使用 WLAN 设备驱动程序接口 (WDI)。 WDI 有关详细信息，请参阅[WLAN 通用 Windows 驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)。

本机 802.11 IHV 扩展性函数由操作系统提供，并由 IHV 扩展 DLL，执行以下调用：

- 分配和释放本机 802.11 框架中使用的缓冲区。
- 发送数据包，如定义的身份验证算法，通过 IHV 的无线 LAN (WLAN) 适配器的数据包。
- IHV WLAN 适配器配置任何身份验证和支持的 IHV 扩展 DLL 的密码算法的各种安全设置。
- IHV UI 扩展 DLL （如果已安装） 进程的事件通知的接口。 例如，IHV 扩展 DLL 可以通知 IHV UI 扩展 DLL 中的基本服务集 (BSS) 网络连接所涉及的各种阶段。 

IHV UI 扩展 DLL 的详细信息，请参阅[本机 802.11 IHV UI 扩展 DLL](native-802-11-ihv-ui-extensions-dll2.md)。

> [!NOTE]
> IHV 扩展 DLL 调用通过函数指针的成员与相关联的每个本机 802.11 IHV 扩展性函数[DOT11EXT_APIS](https://msdn.microsoft.com/library/windows/hardware/ff547617)结构。 当操作系统将调用[Dot11ExtIhvInitService](https://msdn.microsoft.com/library/windows/hardware/ff547470) IHV 处理程序函数，它将传递的指针的列表到 IHV 扩展性函数通过*pDot11ExtAPI*参数。
 
下表列出了可由 IHV 扩展 DLL 调用本机 802.11 IHV 扩展性函数。 每个 IHV 扩展性函数只能在这些情况下调用。


- **在服务初始化之后调用**  
IHV 扩展性函数只能调用后[Dot11ExtIhvInitService](https://msdn.microsoft.com/library/windows/hardware/ff547470)调用 IHV 处理程序函数以初始化 IHV 扩展 DLL。 此外，扩展 DLL 不能调用 IHV 扩展性函数之后， [Dot11ExtIhvDeinitService](https://msdn.microsoft.com/library/windows/hardware/ff547457)调用 IHV 处理程序函数。
- **适配器在初始化之后调用**  
IHV 扩展性函数只能调用后[Dot11ExtIhvInitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547469)调用 IHV 处理程序函数来初始化 IHV WLAN 适配器的接口。  
IHV 扩展性函数要求有句柄，标识将 WLAN 适配器。 当*Dot11ExtIhvInitAdapter*是调用，IHV 扩展 DLL 传递通过此句柄*hDot11SvcHandle*参数。  
扩展 DLL 不能调用 IHV 扩展性函数之后， [Dot11ExtIhvDeinitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547452)调用 IHV 处理程序函数。
- **在预关联之后调用**  
IHV 扩展性函数只能调用后[Dot11ExtIhvPerformPreAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547499)调用 IHV 处理程序函数以启动预关联操作与基本的服务集 (BSS) 网络。  
IHV 扩展性函数要求有句柄，标识 BSS 网络连接。 当*Dot11ExtIhvPerformPreAssociate*是调用，IHV 扩展 DLL 传递通过此句柄*hConnection*参数。  
扩展 DLL 不能调用 IHV 扩展性函数之后， [Dot11ExtIhvDeinitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547452)或[Dot11ExtIhvAdapterReset](https://msdn.microsoft.com/library/windows/hardware/ff547434)已调用 IHV 处理程序函数。
- **在后关联后调用**  
IHV 扩展性函数只能调用后[Dot11ExtIhvPerformPostAssociate](https://msdn.microsoft.com/library/windows/hardware/ff547492)调用 IHV 处理程序函数以启动后关联操作与基本的服务集 (BSS) 网络。  
IHV 扩展性函数要求有句柄，它标识与 BSS 网络连接的安全会话。 当*Dot11ExtIhvPerformPostAssociate*是调用，IHV 扩展 DLL 传递通过此句柄*hSecuritySessionID*参数。  
扩展 DLL 不能调用 IHV 扩展性函数之后， [Dot11ExtIhvDeinitAdapter](https://msdn.microsoft.com/library/windows/hardware/ff547452)或[Dot11ExtIhvAdapterReset](https://msdn.microsoft.com/library/windows/hardware/ff547434)已调用 IHV 处理程序函数。

| 函数 | 在服务初始化之后调用 | 适配器在初始化之后调用 | 在预关联之后调用 | 在后关联后调用 |
| --- | --- | --- | --- | --- |
| [Dot11ExtAllocateBuffer](https://msdn.microsoft.com/library/windows/hardware/ff547419) | X |   |   |   |
| [Dot11ExtFreeBuffer](https://msdn.microsoft.com/library/windows/hardware/ff547422) | X |   |   |   |
| [Dot11ExtGetProfileCustomUserData](https://msdn.microsoft.com/library/windows/hardware/ff547430) |   |   | X |   | 
| [Dot11ExtNicSpecificExtension](https://msdn.microsoft.com/library/windows/hardware/ff547526) |   | X |   |   |
| [Dot11ExtStartOneX](https://msdn.microsoft.com/library/windows/hardware/ff547610) |   |   |   | X |
| [Dot11ExtStopOneX](https://msdn.microsoft.com/library/windows/hardware/ff547614) |   |   |   | X |
| [Dot11ExtPostAssociateCompletion](https://msdn.microsoft.com/library/windows/hardware/ff547530) |   |   |   | X |
| [Dot11ExtPreAssociateCompletion](https://msdn.microsoft.com/library/windows/hardware/ff547538) |   |   | X |   |
| [Dot11ExtProcessOneXPacket](https://msdn.microsoft.com/library/windows/hardware/ff547541) |   |   |   | X |
| [Dot11ExtQueryVirtualStationProperties](https://msdn.microsoft.com/library/windows/hardware/ff547544) |   | X |   |   |
| [Dot11ExtReleaseVirtualStation](https://msdn.microsoft.com/library/windows/hardware/ff547549) |   | X |   |   |
| [Dot11ExtRequestVirtualStation](https://msdn.microsoft.com/library/windows/hardware/ff547556) |   | X |   |   |
| [Dot11ExtSendNotification](https://msdn.microsoft.com/library/windows/hardware/ff547560) |   | X |   |   |
| [Dot11ExtSendUIRequest](https://msdn.microsoft.com/library/windows/hardware/ff547567) |   | X |   |   |
| [Dot11ExtSetAuthAlgorithm](https://msdn.microsoft.com/library/windows/hardware/ff547571) |   | X |   |   |
| [Dot11ExtSetCurrentProfile](https://msdn.microsoft.com/library/windows/hardware/ff547574) |   |   | X |   |
| [Dot11ExtSetDefaultKey](https://msdn.microsoft.com/library/windows/hardware/ff547578) |   | X |   |   |
| [Dot11ExtSetDefaultKeyId](https://msdn.microsoft.com/library/windows/hardware/ff547584)|   | X |   |   |
| [Dot11ExtSetEtherTypeHandling](https://msdn.microsoft.com/library/windows/hardware/ff547587) |   | X |   |   |
| [Dot11ExtSetExcludeUnencrypted](https://msdn.microsoft.com/library/windows/hardware/ff547589) |   | X |   |   |
| [Dot11ExtSetKeyMappingKey](https://msdn.microsoft.com/library/windows/hardware/ff547597) |   | X |   |   |
| [Dot11ExtSetMulticastCipherAlgorithm](https://msdn.microsoft.com/library/windows/hardware/ff547599) |   | X |   |   |
| [Dot11ExtSetProfileCustomUserData](https://msdn.microsoft.com/library/windows/hardware/ff547603) |   | X |   |   |
| [Dot11ExtSetUnicastCipherAlgorithm](https://msdn.microsoft.com/library/windows/hardware/ff547606) |   | X |   |   |
| [Dot11ExtSetVirtualStationAPProperties](https://msdn.microsoft.com/library/windows/hardware/ff547609) |   |   | X |   | 

有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](native-802-11-ihv-handler-functions.md)。


