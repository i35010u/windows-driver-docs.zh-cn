---
title: 执行关联后的操作
description: 执行关联后的操作
ms.assetid: b029d499-a23d-4f2f-aa28-2e8bfb2a00e5
keywords:
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9dadc0f245427398f7c93b831220a08c8ee8451
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384542"
---
# <a name="performing-a-post-association-operation"></a>执行关联后的操作




 

当无线 LAN (WLAN) 适配器已成功完成的访问点 (AP) 802.11 的关联操作时，本机 802.11 微型端口驱动程序通知操作系统，从而[NDIS\_状态\_DOT11\_关联\_完成](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-association-completion)指示。 有关关联操作的详细信息，请参阅[关联操作](association-operations.md)。

**请注意**  For Windows Vista 中，只有在基础结构的基本服务设置 (BSS) 网络 IHV 扩展 DLL 支持。

 

操作系统则接收 NDIS 后\_状态\_DOT11\_关联\_调用完成指示[ *Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数，以通知以下 IHV 扩展 DLL:

-   创建的新的数据端口与亚太的关联。 IHV 扩展 DLL 传递的当前状态的数据端口穿过*pPortState*的参数[ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数。 有关端口状态参数的详细信息，请参阅[ **DOT11\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlclient/ns-wlclient-_dot11_port_state)。

-   无线 LAN (WLAN) 适配器和亚太之间的关联的参数。 IHV 扩展 DLL 传递通过关联参数*pDot11AssocParams*的参数[ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数。 有关关联参数的详细信息，请参阅[ **DOT11\_关联\_完成\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/windot11/ns-windot11-dot11_association_completion_parameters)。

当[ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)是调用，IHV 扩展 DLL 启动后关联操作与 AP 进行身份验证的数据端口。 通过此操作，IHV 扩展 DLL 可以执行以下操作：

-   分配新的数据端口所需的任何资源。

-   执行专用安全关联的数据端口上处理。 IHV 扩展 DLL 可以确定从数据端口的当前状态*pPortState*的参数[ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数。

-   调用[ **Dot11ExtSendUIRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_ui_request)函数请求 IHV UI 扩展 DLL 来提示用户输入安全参数，例如用户的凭据。

-   AP 使用启用通过身份验证算法使用进行身份验证[ **Dot11ExtSetAuthAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)。 IHV 扩展 DLL 调用**Dot11ExtSetAuthAlgorithm**预关联操作过程中。 有关此操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   将安全数据包发送到通过调用 AP [ **Dot11ExtSendPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_send_packet)函数。

    当安全数据包已发送时，操作系统会通知 IHV 扩展 DLL 通过调用[ *Dot11ExtIhvSendPacketCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)函数。

    有关发送安全数据包的详细信息，请参阅[发送操作](send-operations.md)。

-   从 AP 接收安全数据包。 操作系统调用[ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet) WLAN 适配器接收到的每个安全数据包的函数。

    每个接收的安全数据包被序列化，并指示它们将 WLAN 适配器从接收到的顺序。 操作系统将仅调用[ *Dot11ExtIhvReceivePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_packet)函数来指示与 IEEE EtherTypes 列表中的条目匹配的 IHV 由指定的接收到的安全数据包扩展 DLL 通过调用到[ **Dot11ExtSetEtherTypeHandling** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)函数。

    有关接收安全数据包的详细信息，请参阅[接收操作](receive-operations.md)。

-   使用通过身份验证算法派生的加密密钥配置将 WLAN 适配器。 可以调用以下 IHV 扩展性函数以进行下载到 WLAN 适配器的密码密钥。
    -   [**Dot11ExtSetDefaultKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key)
    -   [**Dot11ExtSetDefaultKeyId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)
    -   [**Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)
-   将 WLAN 适配器配置为排除通过调用未加密的数据包[ **Dot11ExtSetExcludeUnencrypted** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_exclude_unencrypted) IHV 扩展性函数。

数据端口已通过身份验证后，必须调用 IHV 扩展 DLL [ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)完成后关联操作。

下图显示涉及后关联操作过程的步骤。

![说明后关联操作过程中所涉及的步骤的关系图](images/ihv-ext-postassoc.png)

执行后关联操作时，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须调用[ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)以异步方式从调用[ *Dot11ExtIhvPerformPostAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate).

-   完成后关联操作后, 可以调用 IHV 扩展 DLL [ **Dot11ExtPostAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)每当数据的身份验证状态的端口的更改。

-   如果[ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)调用函数，IHV 扩展 DLL 必须通过调用取消后关联的所有挂起操作[ **Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)。 有关重置操作的详细信息，请参阅[802.11 WLAN 适配器重置](802-11-wlan-adapter-reset.md)。

-   如果[ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)调用函数，IHV 扩展 DLL 必须在内部取消后关联的所有挂起操作。 但是，它必须调用任一 IHV 扩展性函数可以仅在适配器初始化后调用包括[ **Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)。 有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)。

 

 





