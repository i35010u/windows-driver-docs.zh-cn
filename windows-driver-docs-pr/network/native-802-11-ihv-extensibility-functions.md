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
ms.openlocfilehash: d0ae755feda5de44a86eeb1129bbbb3d77ea7d7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379405"
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
> IHV 扩展 DLL 调用通过函数指针的成员与相关联的每个本机 802.11 IHV 扩展性函数[DOT11EXT_APIS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_apis)结构。 当操作系统将调用[Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV 处理程序函数，它将传递的指针的列表到 IHV 扩展性函数通过*pDot11ExtAPI*参数。
 
下表列出了可由 IHV 扩展 DLL 调用本机 802.11 IHV 扩展性函数。 每个 IHV 扩展性函数只能在这些情况下调用。


- **在服务初始化之后调用**  
IHV 扩展性函数只能调用后[Dot11ExtIhvInitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_service)调用 IHV 处理程序函数以初始化 IHV 扩展 DLL。 此外，扩展 DLL 不能调用 IHV 扩展性函数之后， [Dot11ExtIhvDeinitService](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_service)调用 IHV 处理程序函数。
- **适配器在初始化之后调用**  
IHV 扩展性函数只能调用后[Dot11ExtIhvInitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_adapter)调用 IHV 处理程序函数来初始化 IHV WLAN 适配器的接口。  
IHV 扩展性函数要求有句柄，标识将 WLAN 适配器。 当*Dot11ExtIhvInitAdapter*是调用，IHV 扩展 DLL 传递通过此句柄*hDot11SvcHandle*参数。  
扩展 DLL 不能调用 IHV 扩展性函数之后， [Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)调用 IHV 处理程序函数。
- **在预关联之后调用**  
IHV 扩展性函数只能调用后[Dot11ExtIhvPerformPreAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)调用 IHV 处理程序函数以启动预关联操作与基本的服务集 (BSS) 网络。  
IHV 扩展性函数要求有句柄，标识 BSS 网络连接。 当*Dot11ExtIhvPerformPreAssociate*是调用，IHV 扩展 DLL 传递通过此句柄*hConnection*参数。  
扩展 DLL 不能调用 IHV 扩展性函数之后， [Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)或[Dot11ExtIhvAdapterReset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)已调用 IHV 处理程序函数。
- **在后关联后调用**  
IHV 扩展性函数只能调用后[Dot11ExtIhvPerformPostAssociate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)调用 IHV 处理程序函数以启动后关联操作与基本的服务集 (BSS) 网络。  
IHV 扩展性函数要求有句柄，它标识与 BSS 网络连接的安全会话。 当*Dot11ExtIhvPerformPostAssociate*是调用，IHV 扩展 DLL 传递通过此句柄*hSecuritySessionID*参数。  
扩展 DLL 不能调用 IHV 扩展性函数之后， [Dot11ExtIhvDeinitAdapter](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)或[Dot11ExtIhvAdapterReset](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)已调用 IHV 处理程序函数。

| 函数 | 在服务初始化之后调用 | 适配器在初始化之后调用 | 在预关联之后调用 | 在后关联后调用 |
| --- | --- | --- | --- | --- |
| [Dot11ExtAllocateBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_allocate_buffer) | X |   |   |   |
| [Dot11ExtFreeBuffer](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_free_buffer) | X |   |   |   |
| [Dot11ExtGetProfileCustomUserData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data) |   |   | X |   | 
| [Dot11ExtNicSpecificExtension](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension) |   | X |   |   |
| [Dot11ExtStartOneX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_onex_start) |   |   |   | X |
| [Dot11ExtStopOneX](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_onex_stop) |   |   |   | X |
| [Dot11ExtPostAssociateCompletion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) |   |   |   | X |
| [Dot11ExtPreAssociateCompletion](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion) |   |   | X |   |
| [Dot11ExtProcessOneXPacket](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_process_onex_packet) |   |   |   | X |
| [Dot11ExtQueryVirtualStationProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_query_virtual_station_properties) |   | X |   |   |
| [Dot11ExtReleaseVirtualStation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_release_virtual_station) |   | X |   |   |
| [Dot11ExtRequestVirtualStation](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_request_virtual_station) |   | X |   |   |
| [Dot11ExtSendNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_notification) |   | X |   |   |
| [Dot11ExtSendUIRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request) |   | X |   |   |
| [Dot11ExtSetAuthAlgorithm](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm) |   | X |   |   |
| [Dot11ExtSetCurrentProfile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_current_profile) |   |   | X |   |
| [Dot11ExtSetDefaultKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key) |   | X |   |   |
| [Dot11ExtSetDefaultKeyId](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)|   | X |   |   |
| [Dot11ExtSetEtherTypeHandling](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) |   | X |   |   |
| [Dot11ExtSetExcludeUnencrypted](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_exclude_unencrypted) |   | X |   |   |
| [Dot11ExtSetKeyMappingKey](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key) |   | X |   |   |
| [Dot11ExtSetMulticastCipherAlgorithm](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_multicast_cipher_algorithm) |   | X |   |   |
| [Dot11ExtSetProfileCustomUserData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data) |   | X |   |   |
| [Dot11ExtSetUnicastCipherAlgorithm](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_unicast_cipher_algorithm) |   | X |   |   |
| [Dot11ExtSetVirtualStationAPProperties](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties) |   |   | X |   | 

有关 IHV 处理程序函数的详细信息，请参阅[本机 802.11 IHV 处理程序函数](native-802-11-ihv-handler-functions.md)。


