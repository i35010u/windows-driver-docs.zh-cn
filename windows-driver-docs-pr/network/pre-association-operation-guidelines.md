---
title: 关联前的操作指导原则
description: 关联前的操作指导原则
keywords:
- 预关联操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce89c2cf33b9e3d2f1d43b2bb9c19f5f51eaf7fb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794343"
---
# <a name="pre-association-operation-guidelines"></a>关联前的操作指导原则




 

执行预关联操作时，IHV 扩展 DLL 必须遵循这些准则。

-   调用 [*Dot11ExtIhvPerformPreAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) 函数时，必须执行以下操作：
    -   验证连接和安全配置文件的 IHV 扩展。 如果配置文件参数无效， *Dot11ExtIhvPerformPreAssociate* 函数将返回 winerror.h 中定义的相应错误代码。
    -   创建并启动一个新线程，用于完成预关联操作。 由于必须通过调用 [*Dot11ExtIhvPerformPreAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)异步完成预关联操作，因此在操作完成后，IHV 扩展 DLL 必须从此线程调用 [**Dot11ExtPreAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion) 。
    -   \_从函数调用返回错误 SUCCESS。 此时，系统会通知操作系统：网络配置文件有效并且正在进行预关联操作。
-   IHV 扩展 DLL 可以调用 [**Dot11ExtNicSpecificExtension**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_nic_specific_extension) 函数来配置无线 LAN (WLAN) 适配器。 此函数可以从对 [*Dot11ExtIhvPerformPreAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate) 的调用中调用，也可以从在 *Dot11ExtIhvPerformPreAssociate* 返回后处理预关联操作的线程调用。

-   对 [**Dot11ExtSetProfileCustomUserData**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_profile_custom_user_data)、 [**Dot11ExtGetProfileCustomUserData**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_get_profile_custom_user_data)和 [**Dot11ExtSetCurrentProfile**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_current_profile) 的调用不得从对 [*Dot11ExtIhvPerformPreAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)的调用中进行。 仅当 *Dot11ExtIhvPerformPreAssociate* 返回错误 SUCCESS 后，才能调用这些函数 \_ 。

-   在 IHV 扩展 DLL 调用 [**Dot11ExtPreAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion) 来完成预关联操作后，连接会话的句柄不再有效。 操作系统通过 [*Dot11ExtIhvPerformPreAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_pre_associate)的 *hConnectSession* 参数传递此句柄。 在调用声明 *hConnectSession* 参数的任何 IHV 扩展性函数时，DLL 不得使用此句柄值。

    有关 IHV 扩展性函数的详细信息，请参阅 [本机 802.11 IHV 扩展性函数](./native-802-11-ihv-extensibility-functions.md)。

-   如果调用 [*Dot11ExtIhvAdapterReset*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) 函数，则 IHV 扩展 DLL 必须通过调用 [**Dot11ExtPreAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)来取消预关联操作。 有关重置操作的详细信息，请参阅 [802.11 WLAN 适配器重置](802-11-wlan-adapter-reset.md)。

-   如果调用 [*Dot11ExtIhvDeinitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) 函数，则 IHV 扩展 DLL 必须在内部取消预关联操作。 但是，它不能调用任何只能在适配器初始化之后调用的 IHV 扩展性函数，包括 [**Dot11ExtPreAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_pre_associate_completion)。

 

 
