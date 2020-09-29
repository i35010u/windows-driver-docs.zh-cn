---
title: Windows 8 的 WFP 更改
description: Windows 8 的 WFP 更改
ms.assetid: B83EC5A5-6169-49AB-A7EC-F2078AA0735E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6871cb9806bd1f60d4658b2d12895452dc621226
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423586"
---
# <a name="wfp-changes-for-windows-8"></a>Windows 8 的 WFP 更改


Windows 筛选平台（以 Windows 8 开头）的可用功能和行为中已进行了一些更改。 通常，若要充分利用新功能，必须编译或重新编译具有 NTDDI 版本宏的标注驱动程序， \_ 将其设置为 NTDDI \_ WIN8。

-   新功能：
    - [使用第 2 层筛选](using-layer-2-filtering.md)
    - [使用代理连接跟踪](using-proxied-connections-tracking.md)
    - [使用虚拟交换机筛选](using-virtual-switch-filtering.md)
-   新函数：
    - [**FwpsCalloutRegister2**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister2)
    - [**FwpsFlowAbort0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowabort0)
    - [**FwpsInjectMacReceiveAsync0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacreceiveasync0)
    - [**FwpsInjectMacSendAsync0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacsendasync0)
    - [**FwpsNetBufferListAssociateContext1**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext1)
    - [**FwpsQueryConnectionRedirectState0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsqueryconnectionredirectstate0)
    - [**FwpsRedirectHandleCreate0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandlecreate0)
    - [**FwpsRedirectHandleDestroy0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsredirecthandledestroy0)
    - [**FwpsvSwitchEventsSubscribe0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventssubscribe0)
    - [**FwpsvSwitchEventsUnsubscribe0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitcheventsunsubscribe0)
    - [**FwpsvSwitchNotifyComplete0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsvswitchnotifycomplete0)
-   新的回调函数：
    - [*FWPS \_ 标注 \_ 分类 \_ FN2*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn2)
    - [*FWPS \_ 标注 \_ 通知 \_ FN2*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn2)
    - [*FWPS \_ 网络 \_ 缓冲区 \_ 列表 \_ 通知 \_ FN1*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn1)
    - [*FWPS \_ VSWITCH \_ 筛选器 \_ 引擎 \_ 重新排序 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_filter_engine_reorder_callback0)
    - [*FWPS \_ VSWITCH \_ INTERFACE \_ EVENT \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_interface_event_callback0)
    - [*FWPS \_ VSWITCH \_ 生存期 \_ 事件 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_lifetime_event_callback0)
    - [*FWPS \_ VSWITCH \_ 策略 \_ 事件 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_policy_event_callback0)
    - [*FWPS \_ VSWITCH \_ PORT \_ 事件 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_port_event_callback0)
    - [*FWPS \_ VSWITCH \_ 运行时 \_ 状态 \_ 还原 \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_restore_callback0)
    - [*FWPS \_ VSWITCH \_ 运行时 \_ 状态 \_ SAVE \_ CALLBACK0*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_vswitch_runtime_state_save_callback0)
-   新结构：
    - [**FWPS \_ FILTER2**](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_filter2)
    - [**FWPS \_ VSWITCH \_ 事件 \_ 调度 \_ TABLE0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_vswitch_event_dispatch_table0_)
-   新枚举：
    - [**FWPS \_ 连接 \_ 重定向 \_ 状态**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_connection_redirect_state_)
    - [**FWPS \_ 字段 \_ 出口 \_ VSWITCH \_ 以太网**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_ethernet_)
    - [**FWPS \_ 字段 \_ 出口 \_ VSWITCH \_ 传输 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v4_)
    - [**FWPS \_ 字段 \_ 出口 \_ VSWITCH \_ 传输 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_egress_vswitch_transport_v6_)
    - [**FWPS \_ 字段 \_ 入站 \_ MAC \_ 帧 \_ 本机**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_native_)
    - [**FWPS \_ 字段 \_ 入口 \_ VSWITCH \_ 以太网**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_ethernet_)
    - [**FWPS \_ 字段 \_ 入口 \_ VSWITCH \_ 传输 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v4_)
    - [**FWPS \_ 字段 \_ 入口 \_ VSWITCH \_ 传输 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ingress_vswitch_transport_v6_)
    - [**FWPS \_ 字段 \_ 出站 \_ MAC \_ 帧 \_ 本机**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_native_)
    - [**FWPS \_ VSWITCH \_ 事件 \_ 类型**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_vswitch_event_type_)
-   重命名枚举：
    - [**FWPS \_字段 \_ 入站 \_ mac \_ 帧 \_ 以太网**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_) (**FWPS \_ 字段 \_ 入站 \_ mac \_ 帧 \_ 802 \_ 3**) 
    - [**FWPS \_字段 \_ 出站 \_ mac \_ 帧 \_ 以太网**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_) (**FWPS \_ 字段 \_ 出站 \_ mac \_ 帧 \_ 802 \_ 3**) 

 

