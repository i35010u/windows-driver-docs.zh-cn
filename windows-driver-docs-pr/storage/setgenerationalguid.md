---
title: SetGenerationalGuid
description: SetGenerationalGuid
ms.assetid: cf8e57e5-afdf-4bc2-9849-5df3fbbdd6c5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0c4f6288b8742f2e19357ef830bdb412b1ecdf5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384660"
---
# <a name="setgenerationalguid"></a>SetGenerationalGuid


**SetGenerationalGuid**方法将分配新的 GUID 值给发起方中的信息 HBA 的缓存。

通常，发起方 Hba 缓存例如与特定的发起程序标识符，默认情况下使用没有密钥，并且的 CHAP 机密的发起程序标识符相关联的组键相关联的预共享密钥身份验证信息。 发起方维护标识目前在其缓存中的信息的版本的 GUID。

服务，如 iSCSI 发现服务和更新发起程序的缓存的信息的管理应用程序应更改此 GUID 来指示缓存已被修改。 ISCSI 服务或管理应用程序重新启动时，它可以检查要验证其缓存的信息同步在发起程序上的缓存信息的发起方 HBA 的 GUID。

应用程序和服务可以使用以下 iSCSI WMI 方法来管理发起程序的缓存的配置数据：

[ClearCache](clearcache.md)

[GetPresharedKeyForId](getpresharedkeyforid.md)

[SetGroupPresharedKey](setgrouppresharedkey.md)

[SetPresharedKeyForId](setpresharedkeyforid.md)

[SetTunnelModeOuterAddress](settunnelmodeouteraddress.md)

**SetGenerationalGuid**方法属于未发布[MSiSCSI\_SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关参数的说明**SetGenerationalGuid**方法，请参阅成员的说明[ **SetGenerationalGuid\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_setgenerationalguid_in)和[**SetGenerationalGuid\_出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsiop/ns-iscsiop-_setgenerationalguid_out)结构。 微型端口驱动程序实现 MSiSCSI\_SecurityConfigOperations WMI 类必须支持此方法，如果 HBA 缓存信息。

 

 





