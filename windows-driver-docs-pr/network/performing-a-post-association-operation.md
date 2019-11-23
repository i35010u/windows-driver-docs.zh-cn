---
title: 执行关联后的操作
description: 执行关联后的操作
ms.assetid: b029d499-a23d-4f2f-aa28-2e8bfb2a00e5
keywords:
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5df8cb077fb86e4a1b9e034c07e3860ab4e16002
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843692"
---
# <a name="performing-a-post-association-operation"></a>执行关联后的操作




 

当无线 LAN （WLAN）适配器使用访问点（AP）成功完成802.11 关联操作时，本机802.11 微型端口驱动程序通过使[NDIS\_状态\_DOT11\_关联\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-association-completion)指示来通知操作系统。 有关关联操作的详细信息，请参阅[关联运算](association-operations.md)。

**注意**  对于 Windows VISTA，IHV 扩展 DLL 仅支持基础结构基本服务集（BSS）网络。

 

操作系统接收到 NDIS\_状态\_DOT11\_关联\_完成指示后，它将调用[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数来通知 IHV 扩展 DLL 以下内容：

-   为与 AP 关联而创建新的数据端口。 通过[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数的*PPORTSTATE*参数向 IHV 扩展 DLL 传递数据端口的当前状态。 有关端口状态参数的详细信息，请参阅[**DOT11\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlclient/ns-wlclient-_dot11_port_state)。

-   无线 LAN （WLAN）适配器与 AP 之间关联的参数。 通过[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数的*PDOT11ASSOCPARAMS*参数向 IHV 扩展 DLL 传递关联参数。 有关关联参数的详细信息，请参阅[**DOT11\_association\_完成\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/windot11/ns-windot11-dot11_association_completion_parameters)。

调用[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)时，IHV 扩展 DLL 使用 AP 启动关联后操作以对数据端口进行身份验证。 完成此操作后，IHV 扩展 DLL 可以执行以下操作：

-   为新的数据端口分配所需的任何资源。

-   针对关联的数据端口执行专有安全处理。 IHV 扩展 DLL 可从[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数的*pPortState*参数确定数据端口的当前状态。

-   调用[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)函数以请求 IHV UI 扩展 DLL 提示用户输入安全参数，如用户的凭据。

-   使用通过[**Dot11ExtSetAuthAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)启用的身份验证算法向 AP 进行身份验证。 IHV 扩展 DLL 在预关联操作过程中调用**Dot11ExtSetAuthAlgorithm** 。 有关此操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   通过调用[**Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)函数将安全数据包发送到 AP。

    发送安全数据包后，操作将通过调用[*Dot11ExtIhvSendPacketCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)函数通知 IHV 扩展 DLL。

    有关发送安全数据包的详细信息，请参阅[发送操作](send-operations.md)。

-   从 AP 接收安全数据包。 操作系统为 WLAN 适配器接收的每个安全数据包调用[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)函数。

    每个接收到的安全数据包都按从 WLAN 适配器接收到的顺序进行序列化和指示。 操作系统只调用[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)函数来指示接收到的安全数据包，这些数据包与 IEEE EtherTypes 列表中的条目相匹配，后者由 IHV 扩展 DLL 通过调用[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)函数指定。

    有关接收安全数据包的详细信息，请参阅[接收操作](receive-operations.md)。

-   使用通过身份验证算法派生的密码密钥配置 WLAN 适配器。 可以调用以下 IHV 扩展性函数，将密码密钥下载到 WLAN 适配器。
    -   [**Dot11ExtSetDefaultKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key)
    -   [**Dot11ExtSetDefaultKeyId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)
    -   [**Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)
-   配置 WLAN 适配器，以通过调用[**Dot11ExtSetExcludeUnencrypted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_exclude_unencrypted) IHV 扩展性函数排除未加密的数据包。

对数据端口进行身份验证后，必须调用[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)来完成关联后操作。

下图显示了在之后的关联操作过程中所涉及的步骤。

![说明在后期关联操作过程中涉及的步骤的关系图](images/ihv-ext-postassoc.png)

执行后关联操作时，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须从对[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)的调用异步调用[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) 。

-   完成后关联操作后，每当数据端口的身份验证状态发生更改时，IHV 扩展 DLL 都可以调用[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) 。

-   如果调用[*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)函数，则 IHV 扩展 DLL 必须通过调用[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)取消所有挂起的后关联操作。 有关重置操作的详细信息，请参阅[802.11 WLAN 适配器重置](802-11-wlan-adapter-reset.md)。

-   如果调用[*Dot11ExtIhvDeinitAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)函数，则 IHV 扩展 DLL 必须在内部取消所有挂起的关联后操作。 但是，它不能调用任何只能在适配器初始化之后调用的 IHV 扩展性函数，包括[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)。 有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)。

 

 





