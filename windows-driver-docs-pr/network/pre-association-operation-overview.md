---
title: 关联前的操作概述
description: 关联前的操作概述
ms.assetid: c33cf228-720f-4204-820c-0fb9a288bc6e
keywords:
- 预关联操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e5b5e16c906ef21e769e2cc2db6cadf96b98b4b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843495"
---
# <a name="pre-association-operation-overview"></a>关联前的操作概述




 

用户选择了基本服务集（BSS）网络连接的配置文件后，操作系统将调用[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)函数来启动预关联操作。 调用此函数时，将执行以下操作：

-   验证连接和安全配置文件的 IHV 定义的扩展。

    如果 IHV 扩展 DLL 确定配置文件不正确，它将返回 Winerror.h 中定义的相应错误代码。 在这种情况下，操作系统会通知用户无法使用网络配置文件。

-   基于由 IHV 定义的连接和安全配置文件的扩展启动预关联操作。

    启动预关联操作后，必须通过调用[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)异步完成此操作。

IHV 扩展 DLL 通过调用[**Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)完成预关联操作。 执行此调用后，操作系统将通过发出 OID\_的 set 请求来启动连接操作， [\_将\_请求连接](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-connect-request)到用于管理 WLAN 适配器的本机802.11 微型端口驱动程序。

下图显示了在预关联操作过程中涉及的步骤。

![说明在预关联操作过程中涉及的步骤的关系图](images/ihv-ext-preassoc.png)

调用[*Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)时，操作系统通过以下参数将 IHV 定义的扩展传递到连接和安全配置文件。

<a href="" id="pihvprofileparams"></a>*pIhvProfileParams*  
此参数被传递到[**DOT11EXT\_IHV\_PROFILE\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihvtypes/ns-wlanihvtypes-_dot11ext_ihv_profile_params)结构，后者指定将应用网络配置文件的基本服务集（BSS）网络的属性。 例如， **DOT11EXT\_IHV\_PROFILE\_PARAMS**结构指定了服务集标识符（SSID）和 BSS 网络的类型。

<a href="" id="pihvconnprofile"></a>*pIhvConnProfile*  
此参数被传递到[**DOT11EXT\_IHV 的指针\_连接性\_配置文件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_connectivity_profile)结构，该结构包含连接配置文件的设置。 操作系统仅将扩展传递到由 IHV 定义并由用户选择的连接配置文件。

<a href="" id="pihvsecprofile"></a>*pIhvSecProfile*  
此参数被传递到包含安全配置文件设置的[**DOT11EXT\_IHV\_安全\_配置文件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_security_profile)结构的指针。 操作系统仅将扩展传递到由 IHV 定义并由用户选择的安全配置文件。

<a href="" id="pconnectablebssid"></a>*pConnectableBssid*  
此参数被传递到[**DOT11\_BSS\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlclient/ns-wlclient-_dot11_bss_list)结构，该结构包含一个或多个802.11 信标，或者 DLL 将在其中执行该网络的侦听响应帧预关联操作。

执行预关联操作时，IHV 扩展 DLL 可以执行以下操作：

-   调用[**Dot11ExtNicSpecificExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)函数，以便为连接到本机802.11 微型端口驱动程序的网络连接发出专用配置请求。

    通过*pIhvConnProfile*和*PIHVPROFILEPARAMS*参数，IHV 扩展 DLL 可以确定用户选择了哪些专用连接设置。

    通过*pConnectableBssid*参数，IHV 扩展 DLL 可以确定 BSS 网络的属性，并且可以相应地配置专有网络设置。

-   使用要在 BSS 网络连接上使用的专有身份验证和密码算法配置 WLAN 适配器。

    通过*pszXmlFragmentIhvSecurity*参数，IHV 扩展 DLL 可以确定用户选择了哪些专用安全算法。

    可以调用以下 IHV 扩展性函数来设置安全算法。

    -   [**Dot11ExtSetAuthAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)
    -   [**Dot11ExtSetUnicastCipherAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_unicast_cipher_algorithm)
    -   [**Dot11ExtSetMulticastCipherAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_multicast_cipher_algorithm)
-   调用[**Dot11ExtSendUIRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)函数以请求 IHV UI 扩展 DLL 提示用户输入安全参数，如用户的凭据。

-   调用[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)函数，以便为 DLL 将接收的安全数据包注册 IEEE EtherTypes 列表。 注册列表后，操作系统将为其 EtherType 与列表中的条目相匹配的每个数据包调用[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet) IHV 处理程序函数。

    IHV 扩展 DLL 还可以指定将从负载解密中排除的 EtherTypes 的列表。 有关注册 EtherTypes 的详细信息，请参阅[IEEE EtherType 处理](ieee-ethertype-handling.md)。

-   调用[**Dot11ExtSetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data)函数以保存特定于用户和当前 BSS 网络配置文件的注册表中的数据。

-   调用[**Dot11ExtGetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data)函数以从注册表中检索特定于用户和当前 BSS 网络配置文件的数据。

有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)。

有关 BSS 网络的连接操作的详细信息，请参阅[连接操作](connection-operations.md)。

 

 





