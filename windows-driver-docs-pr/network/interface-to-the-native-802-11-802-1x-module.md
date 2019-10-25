---
title: 与本机 802.11 802.1X 模块对接
description: 与本机 802.11 802.1X 模块对接
ms.assetid: 8af78e5b-c9d9-4f07-8f07-f4a156ffdb9e
keywords:
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
- 802.1 x 模块 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea63a0ffc55be888a18963337cfc140ec851c20b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844190"
---
# <a name="interface-to-the-native-80211-8021x-module"></a>与本机 802.11 802.1X 模块对接




 

在操作系统接收到 NDIS\_状态\_DOT11\_关联\_本机802.11 微型端口驱动程序中的完成指示后，它将调用[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数来启动由 IHV 扩展 DLL 进行的关联后操作。

当执行后关联操作或操作完成后，IHV 扩展 DLL 可以使用操作系统支持的可扩展身份验证协议（EAP）算法对用户使用访问点进行身份验证（AP）。 在这种情况下，IHV 扩展 DLL 使用本机 802.11 framework 的 802.1 X 模块进行处理，以处理由 EAP over LAN （EAPOL）格式的 AP 发送的 EAP 数据包。

有关 EAPOL 格式的详细信息，请参阅 IEEE 802.1 X-2001 标准的子句7。

有关 802.1 X 模块和 Native 802.11 framework 的详细信息，请参阅[本机802.11 软件体系结构](native-802-11-software-architecture.md)。

在将 802.1 X 模块与用户身份验证建立交互时，IHV 扩展 DLL 必须遵循以下准则：

-   对于 Windows Vista，IHV 扩展 DLL 只能通过 802.1 X 模块启动 802.1 X authentication 操作，以仅针对基础结构基本服务集（BSS）网络连接。

-   IHV 扩展 DLL 必须注册到操作系统才能接收 EAPOL 数据包。 在这种情况下，DLL 必须调用[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)函数，并将 IEEE EAPOL EtherType （0x888E）添加到通过*pusRegistration*参数传入的已注册 EtherTypes 的列表。 注册 EtherType 后，操作系统会通过调用[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet) IHV 处理程序函数将接收的 EAPOL 数据包转发到 IHV 扩展 DLL。

    有关注册 EtherTypes 的详细信息，请参阅[IEEE EtherType 处理](ieee-ethertype-handling.md)。

-   当执行后关联操作时，IHV 扩展 DLL 会通过调用[**Dot11ExtStartOneX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_start)函数启动 802.1 x authentication 操作。 调用此函数时，操作系统将执行以下操作：

    -   显示 802.1 X 身份验证配置的 "属性" 页。 此信息包括用于身份验证的 EAP 算法。
    -   提示用户输入凭据。
    -   将 EAPOL 启动数据包发送到 AP，以启动 802.1 X 身份验证。

    在对[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)的调用或函数调用返回后，IHV 扩展 DLL 可以调用**Dot11ExtStartOneX** 。

-   仅在本机802.11 微型端口驱动程序完成与 AP 的关联操作之后，才能调用[**Dot11ExtStartOneX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_start)函数。 在这种情况下，如果存在以下任何情况，则 IHV 扩展 DLL 不得调用**Dot11ExtStartOneX**函数：
    -   在操作系统调用[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)之前。 当微型端口驱动程序成功完成关联操作后，操作系统将调用此函数。 有关此操作的详细信息，请参阅[关联运算](association-operations.md)。
    -   操作系统调用[*Dot11ExtIhvStopPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_stop_post_associate)后。 在微型端口驱动程序完成与 AP 的解除解除操作后，操作系统将调用此函数。 有关此操作的详细信息，请参阅解除相关[操作](disassociation-operations.md)。
    -   操作系统调用[*Dot11ExtIhvAdapterReset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)后。 在微型端口驱动程序完成与基本服务集（BSS）网络的断开操作后，操作系统将调用此函数。 有关此操作的详细信息，请参阅[断开连接操作](disconnection-operations.md)。
-   当 802.1 X authentication 操作正在进行时，IHV 扩展 DLL 可以通过调用[**Dot11ExtStopOneX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_onex_stop)来取消操作。

-   当 802.1 X authentication 操作正在进行时，IHV 扩展 DLL 必须调用[**Dot11ExtProcessOneXPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_process_onex_packet)将 EAPOL 数据包转发给操作系统进行处理。
    **请注意**  IHV 扩展 DLL 负责处理从 AP 收到的 EAPOL 密钥包。 DLL 不能通过调用[**Dot11ExtProcessOneXPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_process_onex_packet)将这些数据包传递到操作系统。

     

-   802.1 X authentication 操作完成后，操作系统将调用[*Dot11ExtIhvOneXIndicateResult*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_onex_indicate_result) IHV 处理程序函数。 调用此函数后，IHV 扩展 DLL 负责处理从该 AP 接收的所有 EAPOL 数据包，如用于派生密码密钥的 EAPOL 密钥包。

-   如果 802.1 X authentication 操作已成功完成，则操作系统会将 MPPE 发送键值传递到[**DOT11\_MSONEX\_结果\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11_msonex_result_params)由*PDOT11MSONEXRESULTPARAMS*指向的参数结构。[*Dot11ExtIhvOneXIndicateResult*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_onex_indicate_result)的参数。 DOT11\_MSONEX\_RESULT\_参数的**pbMPPESendKey**成员指向的 MPPE 发送密钥值是通过身份验证过程派生的，并且在将 EAPOL 密钥发送到 AP 时，由 IHV 扩展 DLL 使用。 此密钥已加密，应通过调用 Windows SDK 中所述的**CryptUnprotectData**函数进行解密。

-   用于派生密码密钥的算法依赖于独立硬件供应商（IHV）的实现。 IHV 扩展 DLL 可支持标准密钥派生算法，如 IEEE 802.11 i-2004 标准的子句8.5 中定义的算法，还可以支持专用密钥派生算法。

-   派生密钥后，IHV 扩展 DLL 可以调用以下函数，将密码密钥下载到用于管理无线 LAN （WLAN）适配器的本机802.11 微型端口驱动程序。

    -   [**Dot11ExtSetDefaultKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key)

    -   [**Dot11ExtSetDefaultKeyId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)

    -   [**Dot11ExtSetKeyMappingKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)

-   IHV 扩展 DLL 通过调用[**Dot11ExtPostAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)函数完成关联后操作。 后关联操作完成后，如果 DLL 确定用户必须重新进行身份验证，则 IHV 扩展 DLL 可以启动另一 802.1 X 身份验证操作。

下图显示了在后处理操作期间 IHV 扩展 DLL 启动 802.1 X 身份验证操作时的事件顺序。

![说明在后期关联操作过程中 ihv 扩展 dll 启动 802.1 x authentication 操作时的事件序列的关系图](images/ihv-ext-802.1x.png)

 

 





