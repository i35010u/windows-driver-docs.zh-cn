---
title: 与本机 802.11 802.1X 模块对接
description: 与本机 802.11 802.1X 模块对接
ms.assetid: 8af78e5b-c9d9-4f07-8f07-f4a156ffdb9e
keywords:
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
- 802.1 x 模块 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1a7e66214cbb91b2adb545285e2ad0fcfa5e449
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380726"
---
# <a name="interface-to-the-native-80211-8021x-module"></a>与本机 802.11 802.1X 模块对接




 

操作系统则接收 NDIS 后\_状态\_DOT11\_关联\_完成指示从本机 802.11 微型端口驱动程序，它会调用[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)函数以启动后关联操作由 IHV 扩展 DLL。

虽然它执行后关联的操作或 IHV 扩展 DLL 在操作完成后，可以使用支持的操作系统的访问点与用户进行身份验证的可扩展的身份验证协议 (EAP) 算法(AP)。 在此情况下，IHV 扩展 DLL 与本机 802.11 框架，用于通过在 EAP AP 通过 LAN (EAPOL) 格式发送的 EAP 数据包处理的 802.1 X 模块的接口。

有关 EAPOL 格式的详细信息，请参阅子句 7 的 IEEE 802.1x X-2001 标准。

有关 802.1x 模块和本机 802.11 框架的详细信息，请参阅[本机 802.11 软件体系结构](native-802-11-software-architecture.md)。

当与之交互用户身份验证的 802.1 X 模块，IHV 扩展 DLL 必须遵循以下准则：

-   对于 Windows Vista，IHV 扩展 DLL 可以启动 802.1x 身份验证操作通过 802.1 X 模块仅对基础结构基本的服务集 (BSS) 网络连接。

-   IHV 扩展 DLL 必须注册以接收 EAPOL 数据包的操作系统。 在这种情况下，必须调用 DLL [ **Dot11ExtSetEtherTypeHandling** ](https://msdn.microsoft.com/library/windows/hardware/ff547587)函数，并添加到列表中传递的已注册EtherTypesIEEEEAPOLEtherType(0x888E)*pusRegistration*参数。 操作系统 EtherType 注册后，将收到的 EAPOL 数据包转发到通过调用 IHV 扩展 DLL [ *Dot11ExtIhvReceivePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff547513) IHV 处理程序函数。

    有关注册 EtherTypes 的详细信息，请参阅[IEEE EtherType 处理](ieee-ethertype-handling.md)。

-   IHV 扩展 DLL 时它正在执行后关联操作，通过调用启动身份验证操作 802.1x [ **Dot11ExtStartOneX** ](https://msdn.microsoft.com/library/windows/hardware/ff547610)函数。 当调用此函数时，操作系统执行以下任务：

    -   显示的 802.1 X 身份验证配置的属性页。 此信息包括用于身份验证的 EAP 算法。
    -   提示用户输入凭据。
    -   EAPOL 启动数据包发送到亚太启动 802.1 X 身份验证。

    IHV 扩展 DLL 可以调用**Dot11ExtStartOneX**调用内[ *Dot11ExtIhvPerformPostAssociate* ](https://msdn.microsoft.com/library/windows/hardware/ff547492)或后该函数调用返回。

-   可以调用 IHV 扩展 DLL [ **Dot11ExtStartOneX** ](https://msdn.microsoft.com/library/windows/hardware/ff547610)函数仅在本机 802.11 微型端口驱动程序与 AP 的关联操作完成后。 在此情况下，不能调用 IHV 扩展 DLL **Dot11ExtStartOneX**函数在任一以下条件：
    -   操作系统调用之前[ *Dot11ExtIhvPerformPostAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547492)。 微型端口驱动程序已成功完成关联操作后，操作系统将调用此函数。 有关此操作的详细信息，请参阅[关联操作](association-operations.md)。
    -   操作系统调用后[ *Dot11ExtIhvStopPostAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547521)。 微型端口驱动程序与 AP 解除关联操作完成后，操作系统将调用此函数。 有关此操作的详细信息，请参阅[解除关联操作](disassociation-operations.md)。
    -   操作系统调用后[ *Dot11ExtIhvAdapterReset*](https://msdn.microsoft.com/library/windows/hardware/ff547434)。 微型端口驱动程序带有基本的服务集 (BSS) 网络的断开连接操作完成后，操作系统将调用此函数。 有关此操作的详细信息，请参阅[断开连接操作](disconnection-operations.md)。
-   IHV 扩展 DLL 802.1 X 身份验证操作时，可以通过调用取消该操作[ **Dot11ExtStopOneX**](https://msdn.microsoft.com/library/windows/hardware/ff547614)。

-   802.1 X 身份验证操作时，必须调用 IHV 扩展 DLL [ **Dot11ExtProcessOneXPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547541) EAPOL 数据包转发到操作系统进行处理。
    **请注意**  IHV 扩展 DLL 负责处理从 AP 接收 Eapol-key 数据包。 DLL 必须将这些数据包传递到通过调用操作系统[ **Dot11ExtProcessOneXPacket**](https://msdn.microsoft.com/library/windows/hardware/ff547541)。

     

-   802.1 X 身份验证操作完成后，操作系统将调用[ *Dot11ExtIhvOneXIndicateResult* ](https://msdn.microsoft.com/library/windows/hardware/ff547482) IHV 处理程序函数。 调用此函数后，IHV 扩展 DLL 负责处理从 AP，如用于密码密钥派生的 Eapol-key 数据包接收到的所有 EAPOL 数据包。

-   如果 802.1 X 身份验证操作已成功完成，操作系统 MPPE 发送键将值传递给[ **DOT11\_MSONEX\_结果\_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff548698)指向结构*pDot11MsOneXResultParams*参数[ *Dot11ExtIhvOneXIndicateResult*](https://msdn.microsoft.com/library/windows/hardware/ff547482)。 指向 MPPE 发送密钥值**pbMPPESendKey** DOT11 成员\_MSONEX\_结果\_PARAMS 通过身份验证过程派生并且由 IHV 扩展 DLL 时将 Eapol-key 数据包发送到 AP 中。 此密钥进行加密，应通过调用解密**CryptUnprotectData** Windows SDK 中所述的函数。

-   用于派生的加密密钥的算法是依赖的独立硬件供应商 (IHV) 实现为基础。 IHV 扩展 DLL 可支持标准的密钥派生算法，例如在 ieee 802.11i 子句 8.5 中定义的算法-2004年标准，以及它可以支持专有密钥派生算法。

-   派生密钥后，IHV 扩展 DLL 可以调用以下函数将下载到本机 802.11 微型端口驱动程序，管理无线 LAN (WLAN) 适配器的密码密钥。

    -   [**Dot11ExtSetDefaultKey**](https://msdn.microsoft.com/library/windows/hardware/ff547578)

    -   [**Dot11ExtSetDefaultKeyId**](https://msdn.microsoft.com/library/windows/hardware/ff547584)

    -   [**Dot11ExtSetKeyMappingKey**](https://msdn.microsoft.com/library/windows/hardware/ff547597)

-   IHV 扩展 DLL 将通过调用完成后关联操作[ **Dot11ExtPostAssociateCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff547530)函数。 后关联操作完成后，IHV 扩展 DLL 可以启动另一个 802.1x 身份验证操作，如果 DLL 确定，用户必须重新进行身份验证。

下图显示了 IHV 扩展 DLL 启动后关联操作期间 802.1 X 身份验证操作时的事件序列。

![说明的一系列事件时 ihv 扩展 dll 启动后关联操作过程中的经过 802.1x 身份验证操作的关系图](images/ihv-ext-802.1x.png)

 

 





