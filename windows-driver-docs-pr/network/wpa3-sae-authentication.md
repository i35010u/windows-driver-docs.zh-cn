---
title: WPA3-SAE 身份验证
description: 本主题介绍 WDI 版本1.1.8 和更高版本的 WPA3-SAE authentication。
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 48024f290351a56c9a81143210566aa24632e5c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836191"
---
# <a name="wpa3-sae-authentication"></a>WPA3-SAE 身份验证

WPA3 SAE （也称为 WPA3）在具有 WDI 版本1.1.8 和更高版本的 Windows 中受支持。 SAE 的帧内容生成和分析 (在 Windows 中执行等于) 身份验证的安全身份验证，但操作系统需要驱动程序支持来发送和接收 WPA3 身份验证帧。

## <a name="wpa3-sae-capabilities"></a>WPA3-SAE 功能

微型端口驱动程序通过执行以下操作来指示 SAE 支持：

1. 设置 SAE 支持的功能。  
    驱动程序在调用 [OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)的过程中将 **SAEAuthenticationSupported** 功能设置为 [WDI_TLV_INTERFACE_ATTRIBUTES](wdi-tlv-interface-attributes.md) 。
2. 设置 MFP 功能。  
    驱动程序在调用 [OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)的过程中将 **MFPCapable** 功能设置为 [WDI_TLV_STATION_ATTRIBUTES](wdi-tlv-station-attributes.md) 。
3. 添加 **WDI_AUTH_ALGO_WPA3_SAE** 身份验证方法。  
    该驱动程序在对 [OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)的调用中返回的身份验证密码组合列表中包含 **WDI_AUTH_ALGO_WPA3_SAE** 。 这应在以下部分中添加：
    - [WDI_TLV_STATION_ATTRIBUTES](wdi-tlv-station-attributes.md) ：： [WDI_TLV_UNICAST_ALGORITHM_LIST](wdi-tlv-unicast-algorithm-list.md)
    - [WDI_TLV_STATION_ATTRIBUTES](wdi-tlv-station-attributes.md) ：： [WDI_TLV_MULTICAST_DATA_ALGORITHM_LIST](wdi-tlv-multicast-data-algorithm-list.md)

## <a name="wpa3-sae-authentication-flow"></a>WPA3-SAE authentication flow

### <a name="connection-initiation"></a>连接启动

SAE 连接是用 [OID_WDI_TASK_CONNECT](oid-wdi-task-connect.md) 或 [OID_WDI_TASK_ROAM](oid-wdi-task-roam.md)启动的。 当驱动程序需要执行 SAE authentication 时，WDI 将 **WDI_AUTH_ALGO_WPA3_SAE** 指定为身份验证方法。 如果 WDI 在 "连接/漫游" 任务的 BSS 列表中提供 PMKID，则驱动程序将跳过 SAE 身份验证，并执行打开身份验证，然后执行 "打开身份验证" 和 "PMKID" 重新关联请求。

### <a name="authentication-flow"></a>身份验证流

![WPA3-SAE authentication flow](images/wpa3-sae-authentication-flow.png "WPA3-SAE authentication flow")

#### <a name="initial-request-for-sae-parameters"></a>SAE 参数的初始请求

驱动程序首先选择要连接或漫游的 BSS，如果 WDI 未提供该 BSS 的 PMKID，则驱动程序将从 WDI 请求提交参数，并 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)。 在此初始指示中，驱动程序将指示类型设置为 **WDI_SAE_INDICATION_TYPE_COMMIT_REQUEST_PARAMS_NEEDED**。 作为响应，WDI 会将 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) 发送到带有以下选项之一的驱动程序。

-  (**WDI_SAE_REQUEST_TYPE_COMMIT_REQUEST** 发送提交请求) 
- SAE authentication (**WDI_SAE_REQUEST_TYPE_FAILURE** 失败) 

#### <a name="upon-receiving-a-commit-response"></a>收到提交响应时

收到提交响应时，驱动程序将发送类型设置为 **WDI_SAE_INDICATION_TYPE_COMMIT_RESPONSE** [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md) 。 在响应中，WDI 将 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) 发送以下请求之一：

-  (**WDI_SAE_REQUEST_TYPE_COMMIT_REQUEST** 发送提交请求) 
-  (**WDI_SAE_REQUEST_TYPE_CONFIRM_REQUEST** 发送确认请求) 
- SAE authentication (**WDI_SAE_REQUEST_TYPE_FAILURE** 失败) 

#### <a name="upon-receiving-a-confirm-response"></a>收到确认响应后

收到确认响应时，驱动程序将发送类型设置为 **WDI_SAE_INDICATION_TYPE_CONFIRM_RESPONSE** [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md) 。 然后，WDI 将发送 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) ，并将 SAE 状态字段设置为成功或失败。 如果由于超时或其他原因导致驱动程序中的 SAE authentication 失败，则驱动程序将向类型为 se 的 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md) 指示发送 **WDI_SAE_INDICATION_TYPE_ERROR** 和 [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md)中指定的失败原因。

### <a name="timeouts-and-retransmissions"></a>超时和重传

这些是由驱动程序处理的。

## <a name="wpa3-sae-association"></a>WPA3-SAE 关联

设备使用以下选项之一连接到 SAE 网络。

### <a name="reassociation-following-sae-exchange"></a> (在 SAE exchange 后重新) 关联

这通常是第一次与 SAE 网络的关联尝试。 驱动程序在关联请求框架的 RSN IE 中设置 SAE AKM。

### <a name="reassociation-using-pmkid"></a>使用 PMKID 重新) 关联 (

如果 WDI 为 "连接/漫游" 任务中的 BSS 条目提供 PMKID，则驱动程序将执行以下操作：

1. 该驱动程序将执行开放式身份验证，然后在 (重新) 关联请求中包含 PMKID。
2. 如果设备在短时间内未收到来自 AP 的响应，或者当 AP 在响应中返回关联错误，则驱动程序将跳过使用此 AP 的 SE 身份验证，或者移到另一个 AP，或回退以便使用此 AP 进行完全 SAE 的身份验证。

SAE authentication/association 完成后，SAE 连接完成。 与之前一样，驱动程序会在 "连接" 或 "漫游" 任务结束时发送以下指示：

- [NDIS_STATUS_WDI_INDICATION_ASSOCIATION_RESULT](ndis-status-wdi-indication-association-result.md)
- [NDIS_STATUS_WDI_INDICATION_CONNECT_COMPLETE](ndis-status-wdi-indication-connect-complete.md)

## <a name="error-handling"></a>错误处理

### <a name="resending-the-sae-commit-request-frame"></a>重新发送 SAE 提交请求帧

如果驱动程序由于超时而需要重新发送提交帧，则它可以重新发送由 WDI 提供的原始标量/元素值，或者从 WDI 请求一组新的标量/元素值并 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md) 指示。

### <a name="resending-the-sae-confirm-response-frame"></a>重新发送 SAE 确认响应帧

如果驱动程序由于超时而需要重新发送确认帧，则它应请求一组新的 **SendConfirm** ，并使用 [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)指示来 **确认** WDI 中的值，并将类型设置为 **WDI_SAE_INDICATION_TYPE_CONFIRM_REQUEST_RESEND_REQUEST**。
