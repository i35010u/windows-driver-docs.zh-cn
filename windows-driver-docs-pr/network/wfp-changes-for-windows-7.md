---
title: Windows 7 的 WFP 更改
description: Windows 7 的 WFP 更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6a8002eaeda3b36a8427602a85c359ee63312a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821901"
---
# <a name="wfp-changes-for-windows-7"></a>Windows 7 的 WFP 更改


Windows 筛选平台的可用功能和行为中已进行了一些更改，以 Windows 7 开始。 通常，若要利用新功能，必须编译或重新编译 \_ 将 NTDDI VERSION 宏设置为 NTDDI WIN7 的标注驱动程序 \_ 。

-   新函数：
    - [**FwpsAcquireClassifyHandle0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquireclassifyhandle0)
    - [**FwpsAcquireWritableLayerDataPointer0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquirewritablelayerdatapointer0)
    - [**FwpsApplyModifiedLayerData0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsapplymodifiedlayerdata0)
    - [**FwpsCalloutRegister1**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister1)
    - [**FwpsCompleteClassify0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteclassify0)
    - [**FwpsPendClassify0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0)
    - [**FwpsReleaseClassifyHandle0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreleaseclassifyhandle0)
    - [*classifyFn1*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn1)
    - [*notifyFn1*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn1)
    - [**FWPS \_ 网络 \_ 缓冲区 \_ 列表 \_ 通知 \_ FN0**](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)
    - [**FwpsInjectTransportSendAsync1**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportsendasync1)
    - [**FwpsNetBufferListAssociateContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext0)
    - [**FwpsNetBufferListGetTagForContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistgettagforcontext0)
    - [**FwpsNetBufferListRemoveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)
    - [**FwpsNetBufferListRetrieveContext0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0)
    - [**FwpsAleEndpointCreateEnumHandle0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointcreateenumhandle0)
    - [**FwpsAleEndpointDestroyEnumHandle0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointdestroyenumhandle0)
    - [**FwpsAleEndpointEnum0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointenum0)
    - [**FwpsAleEndpointGetById0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointgetbyid0)
    - [**FwpsAleEndpointGetSecurityInfo0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointgetsecurityinfo0)
    - [**FwpsAleEndpointSetSecurityInfo0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointsetsecurityinfo0)
-   新的结构和枚举：
    - [**FWPS \_ ALE \_ 终结点 \_ 枚举 \_ TEMPLATE0**](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_ale_endpoint_enum_template0)
    - [**FWPS \_ ALE \_ 终结点 \_ PROPERTIES0**](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_ale_endpoint_properties0)
    - [**FWPS \_ 绑定 \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_bind_request0)
    - [**FWPS \_ CALLOUT1**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout1_)
    - [**FWPS \_ CONNECT \_ REQUEST0**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)
    - [**FWPS \_ 字段 \_ ALE \_ 绑定 \_ 重定向 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_bind_redirect_v4_)
    - [**FWPS \_ 字段 \_ ALE \_ 绑定 \_ 重定向 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_bind_redirect_v6_)
    - [**FWPS \_ 字段 \_ ALE \_ CONNECT \_ 重定向 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_connect_redirect_v4_)
    - [**FWPS \_ 字段 \_ ALE \_ CONNECT \_ 重定向 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_connect_redirect_v6_)
    - [**FWPS \_ 字段 \_ ALE \_ 终结点 \_ 关闭 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_endpoint_closure_v4_)
    - [**FWPS \_ 字段 \_ ALE \_ 终结点 \_ 关闭 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_endpoint_closure_v6_)
    - [**FWPS \_ 字段 \_ ALE \_ 资源 \_ 释放 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_resource_release_v4_)
    - [**FWPS \_ 字段 \_ ALE \_ 资源 \_ 释放 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_resource_release_v6_)
    - [**FWPS \_ 字段 \_ 入站 \_ MAC \_ 帧 \_ 802 \_ 3**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_)
    - [**FWPS \_ 字段 \_ KM \_ 授权**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_km_authorization_)
    - [**FWPS \_ 字段 \_ 名称 \_ 解析 \_ 缓存 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_name_resolution_cache_v4_)
    - [**FWPS \_ 字段 \_ 名称 \_ 解析 \_ 缓存 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_name_resolution_cache_v6_)
    - [**FWPS \_ 字段 \_ 出站 \_ MAC \_ 帧 \_ 802 \_ 3**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_)
    - [**FWPS \_ 字段 \_ 流 \_ 数据包 \_ V4**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_stream_packet_v4_)
    - [**FWPS \_ 字段 \_ 流 \_ 包 \_ V6**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_stream_packet_v6_)
    - [**FWPS \_ FILTER1**](/windows/win32/api/fwpstypes/ns-fwpstypes-fwps_filter1)
    - [**FWPS \_ NET \_ BUFFER \_ LIST \_ 事件 \_ TYPE0**](/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_net_buffer_list_event_type0_)
    - [**FWPS \_ TRANSPORT \_ SEND \_ PARAMS1**](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_transport_send_params1_)
-   新文档主题：
    - [使用绑定或连接重定向](using-bind-or-connect-redirection.md)
    - [使用数据包标记](using-packet-tagging.md)
    - [ALE 终结点生存期管理](ale-endpoint-lifetime-management.md)

 

