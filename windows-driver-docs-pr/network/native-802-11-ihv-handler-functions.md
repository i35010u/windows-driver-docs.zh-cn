---
title: 本机 802.11 IHV 处理程序函数
description: 本部分介绍802.11 本机 802.11 ihv 扩展 DLL 的本机 IHV 处理程序函数
keywords:
- Native 802.11 IVH 处理程序函数
- 本机 802.11 IHV 扩展 DLL 处理程序函数
- WDK Native 802.11 IVH 处理程序函数
ms.date: 04/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33d631e49cc374a093d968ac73d69ba7cd267c2d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839481"
---
# <a name="native-80211-ihv-handler-functions"></a>本机 802.11 IHV 处理程序函数

>[!IMPORTANT]
> Windows 10 和更高版本中不推荐使用 [本机802.11 无线 LAN](/previous-versions/windows/hardware/wireless/native-802-11-wireless-lan4) 接口。 请改用 WLAN 设备驱动程序接口 (WDI) 。 有关 WDI 的详细信息，请参阅 [WLAN 通用 Windows 驱动程序模型](./wdi-miniport-driver-design-guide.md)。

本机 802.11 IHV 处理程序函数由 IHV 扩展 DLL 提供，由操作系统调用以执行以下操作：

- 分配和释放在本机802.11 框架中使用的缓冲区。
- 通过 IHV 的无线 LAN (WLAN) 适配器发送数据包，如通过身份验证算法定义的数据包。
- 基于指定的 IEEE EtherType 值和隐私例外规则列表接收数据包。
- 针对任何专有身份验证和密码算法，为 IHV 的 WLAN 适配器配置各种安全设置。
- 如果安装了) 来处理事件通知，则 (具有 IHV UI 扩展 DLL 的接口。 例如，IHV 扩展 DLL 可能会通知 UI 扩展 DLL，其中包含基本服务集中涉及的各个阶段， (BSS) 网络连接。 

有关 IHV UI 扩展 DLL 的详细信息，请参阅 [本机 802.11 IHV Ui 扩展 dll](native-802-11-ihv-ui-extensions-dll2.md)。

> [!NOTE]
> 除了 [Dot11ExtIhvGetVersionInfo](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info) 和 [Dot11ExtIhvInitService](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)，操作系统通过与 [DOT11EXT_IHV_HANDLERS](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_handlers) 结构的成员相关联的函数指针调用 IHV 处理程序函数。 当操作系统调用 *Dot11ExtIhvInitService* IHV 处理程序函数时，IHV 扩展 DLL 通过 *pDot11IHVHandlers* 参数返回到 IHV 处理程序函数的指针列表。

本部分介绍以下本机 802.11 IHV 处理程序函数。

- [Dot11ExtIhvAdapterReset](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)
- [Dot11ExtIhvControl](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_control)
- [Dot11ExtIhvCreateDiscoveryProfiles](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_create_discovery_profiles)
- [Dot11ExtIhvDeinitAdapter](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)
- [Dot11ExtIhvDeinitService](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_service)
- [Dot11ExtIhvGetVersionInfo](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_get_version_info)
- [Dot11ExtIhvInitAdapter](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_adapter)
- [Dot11ExtIhvInitService](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_service)
- [Dot11ExtIhvInitVirtualStation](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_virtual_station)
- [Dot11ExtIhvIsUIRequestPending](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending)
- [Dot11ExtIhvOneXIndicateResult](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_onex_indicate_result)
- [Dot11ExtIhvPerformCapabilityMatch](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_capability_match)
- [Dot11ExtIhvPerformPostAssociate](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)
- [Dot11ExtIhvPerformPreAssociate](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)
- [Dot11ExtIhvProcessSessionChange](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_session_change)
- [Dot11ExtIhvProcessUIResponse](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response)
- [Dot11ExtIhvQueryUIRequest](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request)
- [Dot11ExtIhvReceiveIndication](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication)
- [Dot11ExtIhvReceivePacket](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)
- [Dot11ExtIhvSendPacketCompletion](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)
- [Dot11ExtIhvStopPostAssociate](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)
- [Dot11ExtIhvValidateProfile](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_validate_profile)
