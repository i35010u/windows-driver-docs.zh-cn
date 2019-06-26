---
title: 关联前的操作指导原则
description: 关联前的操作指导原则
ms.assetid: 35e9b701-6d5d-4c76-80fc-bb146be1ddb1
keywords:
- 预关联操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c8fdc546233bcea904f8f7547fb7a6d051202af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356070"
---
# <a name="pre-association-operation-guidelines"></a>关联前的操作指导原则




 

执行预关联操作时，IHV 扩展 DLL 必须遵循这些准则。

-   当[ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)调用函数，IHV 扩展 DLL 必须执行以下操作：
    -   验证连接和安全配置文件的 IHV 扩展。 如果配置文件参数无效，则*Dot11ExtIhvPerformPreAssociate*函数将返回相应的错误代码在 Winerror.h 中定义。
    -   创建并开始预关联操作完成一个新线程。 因为预关联操作必须通过调用以异步方式完成[ *Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)，IHV 扩展 DLL 必须调用[ **Dot11ExtPreAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)从此线程在操作完成后。
    -   返回错误\_函数调用的成功。 在此情况下，验证网络配置文件有效且预关联操作正在进行中，会通知操作系统。
-   可以调用 IHV 扩展 DLL [ **Dot11ExtNicSpecificExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension)函数配置无线 LAN (WLAN) 适配器。 调用此函数可以从两个对的调用中[ *Dot11ExtIhvPerformPreAssociate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)或处理之后预关联操作的线程从*Dot11ExtIhvPerformPreAssociate*返回。

-   调用[ **Dot11ExtSetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data)， [ **Dot11ExtGetProfileCustomUserData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data)，和[ **Dot11ExtSetCurrentProfile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_current_profile)必须对的调用中建立从[ *Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)。 这些函数只能在调用后*Dot11ExtIhvPerformPreAssociate*将返回错误\_成功。

-   IHV 扩展 DLL 后，将调用[ **Dot11ExtPreAssociateCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)要完成预关联操作，此连接会话的句柄不再有效。 操作系统将通过此句柄传递*hConnectSession*的参数[ *Dot11ExtIhvPerformPreAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)。 调用声明任何 IHV 扩展性函数时，DLL 必须使用此句柄值*hConnectSession*参数。

    有关 IHV 扩展性函数的详细信息，请参阅[本机 802.11 IHV 扩展性函数](https://docs.microsoft.com/windows-hardware/drivers/network/native-802-11-ihv-extensibility-functions)。

-   如果[ *Dot11ExtIhvAdapterReset* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_adapter_reset)调用函数，IHV 扩展 DLL 必须通过调用取消预关联操作[ **Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)。 有关重置操作的详细信息，请参阅[802.11 WLAN 适配器重置](802-11-wlan-adapter-reset.md)。

-   如果[ *Dot11ExtIhvDeinitAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter)调用函数，IHV 扩展 DLL 必须在内部取消预关联操作。 但是，它必须调用任一 IHV 扩展性函数可以仅在适配器初始化后调用包括[ **Dot11ExtPreAssociateCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)。

 

 





