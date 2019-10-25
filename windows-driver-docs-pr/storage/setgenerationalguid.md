---
title: SetGenerationalGuid
description: SetGenerationalGuid
ms.assetid: cf8e57e5-afdf-4bc2-9849-5df3fbbdd6c5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ceffd229204dfacd5d21179e3a38ad6b3cb30bd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838027"
---
# <a name="setgenerationalguid"></a>SetGenerationalGuid


**SetGenerationalGuid**方法为发起程序 HBA 的缓存中的信息分配新的 GUID 值。

发起方 Hba 通常会缓存身份验证信息，例如与特定发起程序标识符相关联的预共享密钥、默认情况下与没有密钥的发起程序标识符关联的组键，以及 CHAP 机密。 发起方维护标识当前缓存中的信息版本的 GUID。

服务（如 iSCSI 发现服务）和更新发起程序的缓存信息的管理应用程序应更改此 GUID，以指示缓存已修改。 当 iSCSI 服务或管理应用程序重新启动时，它可以检查发起程序 HBA 的 GUID，以验证其缓存信息是否与发起方上的缓存信息同步。

应用程序和服务可以使用以下 iSCSI WMI 方法来管理发起方缓存的配置数据：

[ClearCache](clearcache.md)

[GetPresharedKeyForId](getpresharedkeyforid.md)

[SetGroupPresharedKey](setgrouppresharedkey.md)

[SetPresharedKeyForId](setpresharedkeyforid.md)

[SetTunnelModeOuterAddress](settunnelmodeouteraddress.md)

**SetGenerationalGuid**方法属于未发布的[MSISCSI\_SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关**SetGenerationalGuid**方法的参数的说明，请参阅[**SetGenerationalGuid\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setgenerationalguid_in)和[**SetGenerationalGuid\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setgenerationalguid_out)结构的成员说明。 如果 HBA 缓存信息，则实现 MSiSCSI\_SecurityConfigOperations WMI 类的微型端口驱动程序必须支持此方法。

 

 





