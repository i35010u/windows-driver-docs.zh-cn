---
title: 执行关联后的操作
description: 执行关联后的操作
ms.assetid: b029d499-a23d-4f2f-aa28-2e8bfb2a00e5
keywords:
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fceb3213d631ca3aa10163af8f7efefb18556bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562557"
---
# <a name="performing-a-post-association-operation"></a>执行关联后的操作




 

当无线 LAN (WLAN) 适配器已成功完成的访问点 (AP) 802.11 的关联操作时，本机 802.11 微型端口驱动程序通知操作系统，从而[NDIS\_状态\_DOT11\_关联\_完成](https://msdn.microsoft.com/library/windows/hardware/ff567319)指示。 有关关联操作的详细信息，请参阅[关联操作](association-operations.md)。

**请注意**  For Windows Vista 中，只有在基础结构的基本服务设置 (BSS) 网络 IHV 扩展 DLL 支持。

 

操作系统则接收 NDIS 后\_状态\_DOT11\_关联\_调用完成指示[ *Dot11ExtIhvPerformPostAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547492)函数，以通知以下 IHV 扩展 DLL:

-   创建的新的数据端口与亚太的关联。 IHV 扩展 DLL 传递的当前状态的数据端口穿过*pPortState*的参数[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)函数。 有关端口状态参数的详细信息，请参阅[ **DOT11\_端口\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff548753)。

-   无线 LAN (WLAN) 适配器和亚太之间的关联的参数。 IHV 扩展 DLL 传递通过关联参数*pDot11AssocParams*的参数[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)函数。 有关关联参数的详细信息，请参阅[ **DOT11\_关联\_完成\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff547647)。

当[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)是调用，IHV 扩展 DLL 启动后关联操作与 AP 进行身份验证的数据端口。 通过此操作，IHV 扩展 DLL 可以执行以下操作：

-   分配新的数据端口所需的任何资源。

-   执行专用安全关联的数据端口上处理。 IHV 扩展 DLL 可以确定从数据端口的当前状态*pPortState*的参数[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)函数。

-   调用[ **Dot11ExtSendUIRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547567)函数请求 IHV UI 扩展 DLL 来提示用户输入安全参数，例如用户的凭据。

-   AP 使用启用通过身份验证算法使用进行身份验证[ **Dot11ExtSetAuthAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547571)。 IHV 扩展 DLL 调用**Dot11ExtSetAuthAlgorithm**预关联操作过程中。 有关此操作的详细信息，请参阅[预关联操作](pre-association-operations.md)。

-   将安全数据包发送到通过调用 AP [ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)函数。

    当安全数据包已发送时，操作系统会通知 IHV 扩展 DLL 通过调用[ *Dot11ExtIhvSendPacketCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff547516)函数。

    有关发送安全数据包的详细信息，请参阅[发送操作](send-operations.md)。

-   从 AP 接收安全数据包。 操作系统调用[ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513) WLAN 适配器接收到的每个安全数据包的函数。

    每个接收的安全数据包被序列化，并指示它们将 WLAN 适配器从接收到的顺序。 操作系统将仅调用[ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513)函数来指示与 IEEE EtherTypes 列表中的条目匹配的 IHV 由指定的接收到的安全数据包扩展 DLL 通过调用到[ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587)函数。

    有关接收安全数据包的详细信息，请参阅[接收操作](receive-operations.md)。

-   使用通过身份验证算法派生的加密密钥配置将 WLAN 适配器。 可以调用以下 IHV 扩展性函数以进行下载到 WLAN 适配器的密码密钥。
    -   [**Dot11ExtSetDefaultKey**](https://msdn.microsoft.com/library/windows/hardware/ff547578)
    -   [**Dot11ExtSetDefaultKeyId**](https://msdn.microsoft.com/library/windows/hardware/ff547584)
    -   [**Dot11ExtSetKeyMappingKey**](https://msdn.microsoft.com/library/windows/hardware/ff547597)
-   将 WLAN 适配器配置为排除通过调用未加密的数据包[ **Dot11ExtSetExcludeUnencrypted** ](https://msdn.microsoft.com/library/windows/hardware/ff547589) IHV 扩展性函数。

数据端口已通过身份验证后，必须调用 IHV 扩展 DLL [ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)完成后关联操作。

下图显示涉及后关联操作过程的步骤。

![说明后关联操作过程中所涉及的步骤的关系图](images/ihv-ext-postassoc.png)

执行后关联操作时，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须调用[ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)以异步方式从调用[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492).

-   完成后关联操作后, 可以调用 IHV 扩展 DLL [ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)每当数据的身份验证状态的端口的更改。

-   如果[ *Dot11ExtIhvAdapterReset* ](https://msdn.microsoft.com/library/windows/hardware/ff547434)调用函数，IHV 扩展 DLL 必须通过调用取消后关联的所有挂起操作[ **Dot11ExtPostAssociateCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff547530)。 有关重置操作的详细信息，请参阅[802.11 WLAN 适配器重置](802-11-wlan-adapter-reset.md)。

-   如果[ *Dot11ExtIhvDeinitAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff547452)调用函数，IHV 扩展 DLL 必须在内部取消后关联的所有挂起操作。 但是，它必须调用任一 IHV 扩展性函数可以仅在适配器初始化后调用包括[ **Dot11ExtPostAssociateCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff547530)。 有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://msdn.microsoft.com/library/windows/hardware/ff560609)。

 

 





