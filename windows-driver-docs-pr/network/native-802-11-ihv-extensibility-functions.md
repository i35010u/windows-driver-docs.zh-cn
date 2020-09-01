---
title: 本机 802.11 IHV 扩展性函数
description: 本部分介绍本机 802.11 ihv 扩展 DLL 802.11 的本机 IHV 扩展性函数
keywords:
- 本机 802.11 IVH 扩展性函数
- 本机 802.11 IHV 扩展 DLL 扩展性函数
- WDK 本机 802.11 IVH 扩展性函数
ms.assetid: 0E7CC153-5434-459D-9773-8CCAFBACD016
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: efb49fc5236b8ea395148b8bcd465b5e20c96918
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217030"
---
# <a name="native-80211-ihv-extensibility-functions"></a>本机 802.11 IHV 扩展性函数

> [!IMPORTANT]
> Windows 10 和更高版本中不推荐使用 [本机802.11 无线 LAN](/previous-versions/windows/hardware/wireless/native-802-11-wireless-lan4) 接口。 请改用 WLAN 设备驱动程序接口 (WDI) 。 有关 WDI 的详细信息，请参阅 [WLAN 通用 Windows 驱动程序模型](./wdi-miniport-driver-design-guide.md)。

本机 802.11 IHV 扩展性函数由操作系统提供，由 IHV 扩展 DLL 调用以执行以下操作：

- 分配和释放在本机802.11 框架中使用的缓冲区。
- 通过 IHV 的无线 LAN (WLAN) 适配器发送数据包，如通过身份验证算法定义的数据包。
- 针对 IHV 扩展 DLL 支持的任何身份验证和密码算法，为 IHV 的 WLAN 适配器配置各种安全设置。
- 如果安装了) 来处理事件通知，则 (具有 IHV UI 扩展 DLL 的接口。 例如，IHV 扩展 DLL 可能会通知 IHV UI 扩展 DLL，其中包含有关基本服务集中涉及的各个阶段 (BSS) 网络连接。 

有关 IHV UI 扩展 DLL 的详细信息，请参阅 [本机 802.11 IHV Ui 扩展 dll](native-802-11-ihv-ui-extensions-dll2.md)。

> [!NOTE]
> IHV 扩展 DLL 通过与 [DOT11EXT_APIS](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_apis) 结构的成员相关联的函数指针调用每个本机 802.11 IHV 扩展性函数。 当操作系统调用 [Dot11ExtIhvInitService](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service) IHV 处理程序函数时，它通过 *PDOT11EXTAPI* 参数向 IHV 扩展性函数传递指针列表。
 
下表列出了可由 IHV 扩展 DLL 调用的本机 802.11 IHV 扩展函数。 每个 IHV 扩展性函数只能在这些条件下调用。


- **在服务初始化后调用**  
仅当调用 [Dot11ExtIhvInitService](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service) Ihv 处理程序函数以初始化 IHV 扩展 DLL 之后，才能调用 ihv 扩展性函数。 此外，在调用 [Dot11ExtIhvDeinitService](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_service) IHV 处理程序函数后，扩展 DLL 无法调用 IHV 扩展性函数。
- **在适配器初始化后调用**  
仅当调用 [Dot11ExtIhvInitAdapter](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter) Ihv 处理程序函数以初始化 ihv WLAN 适配器的接口后，才能调用 ihv 扩展性函数。  
IHV 扩展性函数需要一个用于标识 WLAN 适配器的句柄。 调用 *Dot11ExtIhvInitAdapter* 时，会通过 *HDOT11SVCHANDLE* 参数向 IHV 扩展 DLL 传递此句柄。  
调用 [Dot11ExtIhvDeinitAdapter](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) IHV 处理程序函数后，扩展 DLL 无法调用 IHV 扩展性函数。
- **在预关联后调用**  
仅当调用 [Dot11ExtIhvPerformPreAssociate](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) IHV 处理程序函数以启动具有基本服务集的预关联操作 (BSS) 网络后，才能调用 ihv 扩展性函数。  
IHV 扩展性函数需要一个句柄，用于标识 BSS 网络连接。 调用 *Dot11ExtIhvPerformPreAssociate* 时，会通过 *HCONNECTION* 参数向 IHV 扩展 DLL 传递此句柄。  
调用 [Dot11ExtIhvDeinitAdapter](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) 或 [Dot11ExtIhvAdapterReset](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) IHV 处理程序函数后，扩展 DLL 无法调用 IHV 扩展性函数。
- **在后关联后调用**  
仅当调用 [Dot11ExtIhvPerformPostAssociate](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) IHV 处理程序函数以) 网络 (BSS 启动关联后操作时，才能调用 ihv 扩展性函数。  
IHV 扩展性函数需要一个句柄，该句柄标识与 BSS 网络连接的安全会话。 调用 *Dot11ExtIhvPerformPostAssociate* 时，会通过 *HSECURITYSESSIONID* 参数向 IHV 扩展 DLL 传递此句柄。  
调用 [Dot11ExtIhvDeinitAdapter](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) 或 [Dot11ExtIhvAdapterReset](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) IHV 处理程序函数后，扩展 DLL 无法调用 IHV 扩展性函数。

| 函数 | 在服务初始化后调用 | 在适配器初始化后调用 | 在预关联后调用 | 在后关联后调用 |
| --- | --- | --- | --- | --- |
| [Dot11ExtAllocateBuffer](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_allocate_buffer) | X |   |   |   |
| [Dot11ExtFreeBuffer](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_free_buffer) | X |   |   |   |
| [Dot11ExtGetProfileCustomUserData](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data) |   |   | X |   | 
| [Dot11ExtNicSpecificExtension](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension) |   | X |   |   |
| [Dot11ExtStartOneX](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_start) |   |   |   | X |
| [Dot11ExtStopOneX](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_stop) |   |   |   | X |
| [Dot11ExtPostAssociateCompletion](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) |   |   |   | X |
| [Dot11ExtPreAssociateCompletion](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion) |   |   | X |   |
| [Dot11ExtProcessOneXPacket](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_process_onex_packet) |   |   |   | X |
| [Dot11ExtQueryVirtualStationProperties](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_query_virtual_station_properties) |   | X |   |   |
| [Dot11ExtReleaseVirtualStation](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_release_virtual_station) |   | X |   |   |
| [Dot11ExtRequestVirtualStation](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_request_virtual_station) |   | X |   |   |
| [Dot11ExtSendNotification](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_notification) |   | X |   |   |
| [Dot11ExtSendUIRequest](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request) |   | X |   |   |
| [Dot11ExtSetAuthAlgorithm](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm) |   | X |   |   |
| [Dot11ExtSetCurrentProfile](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_current_profile) |   |   | X |   |
| [Dot11ExtSetDefaultKey](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key) |   | X |   |   |
| [Dot11ExtSetDefaultKeyId](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)|   | X |   |   |
| [Dot11ExtSetEtherTypeHandling](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) |   | X |   |   |
| [Dot11ExtSetExcludeUnencrypted](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_exclude_unencrypted) |   | X |   |   |
| [Dot11ExtSetKeyMappingKey](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key) |   | X |   |   |
| [Dot11ExtSetMulticastCipherAlgorithm](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_multicast_cipher_algorithm) |   | X |   |   |
| [Dot11ExtSetProfileCustomUserData](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data) |   | X |   |   |
| [Dot11ExtSetUnicastCipherAlgorithm](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_unicast_cipher_algorithm) |   | X |   |   |
| [Dot11ExtSetVirtualStationAPProperties](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties) |   |   | X |   | 

有关 IHV 处理程序函数的详细信息，请参阅 [本机 802.11 IHV 处理程序函数](native-802-11-ihv-handler-functions.md)。