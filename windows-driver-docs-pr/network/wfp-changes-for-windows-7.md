---
title: Windows 7 的 WFP 更改
description: Windows 7 的 WFP 更改
ms.assetid: c7b15182-592a-4cdb-98aa-5283ed2f51a0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbb6c495e6f6683261e12e62f123a09dee88206f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841705"
---
# <a name="wfp-changes-for-windows-7"></a>Windows 7 的 WFP 更改


Windows 筛选平台的可用功能和行为中已进行了一些更改，以 Windows 7 开始。 通常，若要充分利用新功能，必须编译或重新编译将 NTDDI\_VERSION 宏设置为 NTDDI\_WIN7 的标注驱动程序。

-   新函数：
    - [**FwpsAcquireClassifyHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquireclassifyhandle0)
    - [**FwpsAcquireWritableLayerDataPointer0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsacquirewritablelayerdatapointer0)
    - [**FwpsApplyModifiedLayerData0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsapplymodifiedlayerdata0)
    - [**FwpsCalloutRegister1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscalloutregister1)
    - [**FwpsCompleteClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteclassify0)
    - [**FwpsPendClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0)
    - [**FwpsReleaseClassifyHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreleaseclassifyhandle0)
    - [*classifyFn1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn1)
    - [*notifyFn1*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn1)
    - [**FWPS\_NET\_缓冲器\_列表\_通知\_FN0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_net_buffer_list_notify_fn0)
    - [**FwpsInjectTransportSendAsync1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjecttransportsendasync1)
    - [**FwpsNetBufferListAssociateContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistassociatecontext0)
    - [**FwpsNetBufferListGetTagForContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistgettagforcontext0)
    - [**FwpsNetBufferListRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistremovecontext0)
    - [**FwpsNetBufferListRetrieveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsnetbufferlistretrievecontext0)
    - [**FwpsAleEndpointCreateEnumHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointcreateenumhandle0)
    - [**FwpsAleEndpointDestroyEnumHandle0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointdestroyenumhandle0)
    - [**FwpsAleEndpointEnum0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointenum0)
    - [**FwpsAleEndpointGetById0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointgetbyid0)
    - [**FwpsAleEndpointGetSecurityInfo0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointgetsecurityinfo0)
    - [**FwpsAleEndpointSetSecurityInfo0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsaleendpointsetsecurityinfo0)
-   新的结构和枚举：
    - [**FWPS\_ALE\_终结点\_枚举\_TEMPLATE0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_ale_endpoint_enum_template0_)
    - [**FWPS\_ALE\_终结点\_PROPERTIES0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_ale_endpoint_properties0_)
    - [**FWPS\_绑定\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_bind_request0)
    - [**FWPS\_CALLOUT1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout1_)
    - [**FWPS\_连接\_REQUEST0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-_fwps_connect_request0)
    - [**FWPS\_字段\_ALE\_绑定\_重定向\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_bind_redirect_v4_)
    - [**FWPS\_字段\_ALE\_绑定\_重定向\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_bind_redirect_v6_)
    - [**FWPS\_字段\_ALE\_连接\_重定向\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_connect_redirect_v4_)
    - [**FWPS\_字段\_ALE\_连接\_重定向\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_connect_redirect_v6_)
    - [**FWPS\_字段\_ALE\_终结点\_关闭\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_endpoint_closure_v4_)
    - [**FWPS\_字段\_ALE\_终结点\_关闭\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_endpoint_closure_v6_)
    - [**FWPS\_字段\_ALE\_资源\_版本\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_resource_release_v4_)
    - [**FWPS\_字段\_ALE\_资源\_RELEASE\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_ale_resource_release_v6_)
    - [**FWPS\_字段\_入站\_MAC\_帧\_802\_3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_)
    - [**FWPS\_字段\_KM\_授权**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_km_authorization_)
    - [**FWPS\_字段\_名称\_分辨率\_缓存\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_name_resolution_cache_v4_)
    - [**FWPS\_字段\_名称\_分辨率\_缓存\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_name_resolution_cache_v6_)
    - [**FWPS\_字段\_出站\_MAC\_帧\_802\_3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_)
    - [**FWPS\_字段\_STREAM\_数据包\_V4**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_stream_packet_v4_)
    - [**FWPS\_字段\_STREAM\_包\_V6**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_stream_packet_v6_)
    - [**FWPS\_FILTER1**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_filter1_)
    - [**FWPS\_NET\_BUFFER\_列表\_事件\_TYPE0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_net_buffer_list_event_type0_)
    - [**FWPS\_传输\_发送\_PARAMS1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_transport_send_params1_)
-   新文档主题：
    - [使用 Bind 或 Connect 重定向](using-bind-or-connect-redirection.md)
    - [使用数据包标记](using-packet-tagging.md)
    - [ALE 终结点生存期管理](ale-endpoint-lifetime-management.md)

 

 





