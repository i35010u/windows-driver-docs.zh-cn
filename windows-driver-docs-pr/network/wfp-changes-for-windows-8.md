---
title: Windows 8 的 WFP 更改
description: Windows 8 的 WFP 更改
ms.assetid: B83EC5A5-6169-49AB-A7EC-F2078AA0735E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a97281105a6f232a9c12fef45b4247586b07932e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841702"
---
# <a name="wfp-changes-for-windows-8"></a>Windows 8 的 WFP 更改


Windows 筛选平台（以 Windows 8 开头）的可用功能和行为中已进行了一些更改。 通常，若要充分利用新功能，必须编译或重新编译将 NTDDI\_VERSION 宏设置为 NTDDI\_WIN8 的标注驱动程序。

-   新增功能：
    - [使用第2层筛选](using-layer-2-filtering.md)
    - [使用代理连接跟踪](using-proxied-connections-tracking.md)
    - [使用虚拟交换机筛选](using-virtual-switch-filtering.md)
-   新函数：
    - [**FwpsCalloutRegister2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister2)
    - [**FwpsFlowAbort0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowabort0)
    - [**FwpsInjectMacReceiveAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacreceiveasync0)
    - [**FwpsInjectMacSendAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacsendasync0)
    - [**FwpsNetBufferListAssociateContext1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext1)
    - [**FwpsQueryConnectionRedirectState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0)
    - [**FwpsRedirectHandleCreate0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)
    - [**FwpsRedirectHandleDestroy0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandledestroy0)
    - [**FwpsvSwitchEventsSubscribe0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventssubscribe0)
    - [**FwpsvSwitchEventsUnsubscribe0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventsunsubscribe0)
    - [**FwpsvSwitchNotifyComplete0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitchnotifycomplete0)
-   新的回调函数：
    - [*FWPS\_标注\_分类\_FN2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn2)
    - [*FWPS\_标注\_通知\_FN2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn2)
    - [*FWPS\_NET\_缓冲器\_列表\_通知\_FN1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)
    - [*FWPS\_VSWITCH\_FILTER\_引擎\_重新排序\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_filter_engine_reorder_callback0)
    - [*FWPS\_VSWITCH\_INTERFACE\_EVENT\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_interface_event_callback0)
    - [*FWPS\_VSWITCH\_生存期\_事件\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_lifetime_event_callback0)
    - [*FWPS\_VSWITCH\_策略\_事件\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_policy_event_callback0)
    - [*FWPS\_VSWITCH\_端口\_事件\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_port_event_callback0)
    - [*FWPS\_VSWITCH\_运行时\_状态\_RESTORE\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_restore_callback0)
    - [*FWPS\_VSWITCH\_运行时\_状态\_保存\_CALLBACK0*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_save_callback0)
-   新结构：
    - [**FWPS\_FILTER2**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_filter2_)
    - [**FWPS\_VSWITCH\_事件\_调度\_TABLE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_vswitch_event_dispatch_table0_)
-   新枚举：
    - [**FWPS\_连接\_重定向\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_connection_redirect_state_)
    - [**FWPS\_字段\_出口\_VSWITCH\_以太网**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_ethernet_)
    - [**FWPS\_字段\_出口\_VSWITCH\_传输\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v4_)
    - [**FWPS\_字段\_出口\_VSWITCH\_传输\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v6_)
    - [**FWPS\_字段\_入站\_MAC\_帧\_本机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_native_)
    - [**FWPS\_字段\_入口\_VSWITCH\_以太网**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_ethernet_)
    - [**FWPS\_字段\_入口\_VSWITCH\_传输\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v4_)
    - [**FWPS\_字段\_入口\_VSWITCH\_传输\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v6_)
    - [**FWPS\_字段\_出站\_MAC\_帧\_本机**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_native_)
    - [**FWPS\_VSWITCH\_事件\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_vswitch_event_type_)
-   重命名枚举：
    - [**FWPS\_字段\_入站\_MAC\_帧\_以太网**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_)（was **FWPS\_字段\_入站\_MAC\_帧\_802\_3**）
    - [**FWPS\_字段\_出站\_MAC\_帧\_以太网**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_)（was **FWPS\_字段\_出站\_MAC\_帧\_802\_3**）

 

 





