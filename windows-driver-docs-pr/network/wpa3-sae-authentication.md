---
title: WPA3 SAE 身份验证
description: 本主题介绍 WDI 版本 1.1.8 WPA3 SAE 身份验证和更高版本。
ms.assetid: BE6EF8E4-F4EB-4D39-AC33-B67F8935DCBC
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 90ead0fe0ef244a3ee0f5a5e3439ba0f6ae530e0
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905318"
---
# <a name="wpa3-sae-authentication"></a>WPA3 SAE 身份验证

WPA3 SAE，也称为 WPA3 个人、 是支持在 Windows 中使用 WDI 版本 1.1.8 及更高版本。 生成和分析 SAE （安全身份验证的等于） 身份验证在 Windows 中，完成，但操作系统需要驱动程序支持用于发送和接收 WPA3 SAE 身份验证框架内容的帧。

## <a name="wpa3-sae-capabilities"></a>WPA3 SAE 功能

微型端口驱动程序通过执行以下操作来表示 SAE 支持：

1. 设置 SAE 支持功能。  
    驱动程序集**SAEAuthenticationSupported**中的功能[WDI_TLV_INTERFACE_ATTRIBUTES](wdi-tlv-interface-attributes.md)在调用[OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)。
2. 设置 MFP 功能。  
    驱动程序集**MFPCapable**中的功能[WDI_TLV_STATION_ATTRIBUTES](wdi-tlv-station-attributes.md)在调用[OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)。
3. 添加**WDI_AUTH_ALGO_WPA3_SAE**身份验证方法。  
    驱动程序都包括**WDI_AUTH_ALGO_WPA3_SAE**调用中返回的身份验证和密码组合的列表中[OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)。 这应在以下各节中添加：
    - [WDI_TLV_STATION_ATTRIBUTES](wdi-tlv-station-attributes.md) ::[WDI_TLV_UNICAST_ALGORITHM_LIST](wdi-tlv-unicast-algorithm-list.md)
    - [WDI_TLV_STATION_ATTRIBUTES](wdi-tlv-station-attributes.md) ::[WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST](wdi-tlv-multicast-data-algorithm-list.md)

## <a name="wpa3-sae-authentication-flow"></a>WPA3 SAE 身份验证流

### <a name="connection-initiation"></a>连接初始化

SAE 连接均使用发起[OID_WDI_TASK_CONNECT](oid-wdi-task-connect.md)或[OID_WDI_TASK_ROAM](oid-wdi-task-roam.md)。 指定 WDI **WDI_AUTH_ALGO_WPA3_SAE**作为身份验证方法时进行 SAE 身份验证所需的驱动程序。 如果 WDI 提供的 BSS 列表中的连接/漫游任务 PMKID，驱动程序将跳过 SAE 身份验证，并执行开放式身份验证而是跟 PMKID 的重新关联请求。

### <a name="authentication-flow"></a>身份验证流

![WPA3 SAE 身份验证流](images/wpa3-sae-authentication-flow.png "WPA3 SAE 身份验证流")

#### <a name="initial-request-for-sae-parameters"></a>初始请求 SAE 参数

该驱动程序首先选择要连接或漫游到 BSS 和 WDI 未提供该 BSS PMKID，如果驱动程序将请求提交参数从与 WDI [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)。 在此初始指示驱动程序将指示类型设置为**WDI_SAE_INDICATION_TYPE_COMMIT_REQUEST_PARAMS_NEEDED**。 在响应中，发送 WDI [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)与驱动程序带有以下选项之一。

- 提交请求发送 (**WDI_SAE_REQUEST_TYPE_COMMIT_REQUEST**)
- SAE 身份验证失败 (**WDI_SAE_REQUEST_TYPE_FAILURE**)

#### <a name="upon-receiving-a-commit-response"></a>一旦收到提交响应

收到提交响应，该驱动程序将发送[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)类型设置为**WDI_SAE_INDICATION_TYPE_COMMIT_RESPONSE**。 在响应中，发送 WDI [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)以下请求之一：

- 提交请求发送 (**WDI_SAE_REQUEST_TYPE_COMMIT_REQUEST**)
- 发送确认请求 (**WDI_SAE_REQUEST_TYPE_CONFIRM_REQUEST**)
- SAE 身份验证失败 (**WDI_SAE_REQUEST_TYPE_FAILURE**)

#### <a name="upon-receiving-a-confirm-response"></a>在收到确认响应时

收到确认响应，该驱动程序将发送[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)类型设置为**WDI_SAE_INDICATION_TYPE_CONFIRM_RESPONSE**。 然后将发送 WDI [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) SAE 状态字段设置为成功或失败。 如果由于超时或其他原因驱动程序在 SAE 身份验证失败，驱动程序将发送[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)与类型的系统工程师到指示**WDI_SAE_INDICATION_TYPE_ERROR**中指定的失败原因[WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md)。

### <a name="timeouts-and-retransmissions"></a>超时和重传

这些驱动程序进行处理。

## <a name="wpa3-sae-association"></a>WPA3 SAE 关联

设备连接到使用以下选项之一的 SAE 网络。

### <a name="reassociation-following-sae-exchange"></a>(Re)以下 SAE exchange 的关联

这通常是首次尝试关联 SAE 网络。 该驱动程序设置中关联请求帧中 RSN IE SAE AKM。

### <a name="reassociation-using-pmkid"></a>(Re)使用 PMKID 关联

如果 WDI 提供 PMKID connect/漫游任务中的 BSS 条目，该驱动程序执行以下操作：

1. 该驱动程序执行跟 PMKID (Re) 关联请求中包含的打开身份验证。
2. 如果设备未收到响应亚太短的时间，或者如果 AP 在响应中返回关联错误，该驱动程序将跳过此应用程序使用 SE 身份验证并将移动到另一个 AP，或将回退到使用此应用程序的完整 SAE 身份验证执行的操作。

SAE 连接完成后 SAE 身份验证/关联已完成。 为之前，驱动程序将发送以下迹象上结束连接或漫游任务：

- [NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT](ndis-status-wdi-indication-association-result.md)
- [NDIS_STATUS_WDI_INDICATION_CONNECT_COMPLETE](ndis-status-wdi-indication-connect-complete.md)

## <a name="error-handling"></a>错误处理

### <a name="resending-the-sae-commit-request-frame"></a>重新发送 SAE 提交请求帧

如果驱动程序需要重新发送提交帧由于超时，它可以重新发送已由 WDI，提供的原始标量/元素值，或请求 WDI 使用一组新的标量/元素值[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)指示。

### <a name="resending-the-sae-confirm-response-frame"></a>重新发送 SAE 确认响应帧

如果该驱动程序必须重新发送确认框时，由于超时，则应请求一组新的**SendConfirm**并**确认**值从与 WDI [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)指示，将类型设置为**WDI_SAE_INDICATION_TYPE_CONFIRM_REQUEST_RESEND_REQUEST**。
