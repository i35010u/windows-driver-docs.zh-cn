---
title: SetGroupPresharedKey
description: SetGroupPresharedKey
ms.assetid: 7dedcc62-4ad6-42d5-a461-b0a69c9c97cd
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e4db0cf0ec72eed7a253c9945f622b35ceaaf009
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193163"
---
# <a name="setgrouppresharedkey"></a>SetGroupPresharedKey


**SetGroupPresharedKey**方法允许管理应用程序将发起方 HBA 配置为在需要密钥时使用指定的预共享密钥，但当前没有密钥与会话的标识符 (ID) 相关联

当发起方在密钥交换中使用预共享密钥时，它会将该密钥与发起程序的标识符相关联，并将该标识符及其关联密钥传递到标识包的数据部分中的目标 (也称为 *标识有效负载*) 。 发起方在主动或主模式的 Internet 密钥交换 (IKE) 期间传递标识符及其关联的密钥，如 [RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)中所述。 标识负载允许目标以一种安全的方式标识发起方，并选择适合与特定发起程序的连接的安全策略。

**SetGroupPresharedKey**方法将发起程序配置为使用尚未与某个键关联的标识符的默认预共享密钥。 若要在密钥与特定发起程序标识符之间建立显式关联，管理应用程序必须调用 [SetPresharedKeyForId](setpresharedkeyforid.md) 方法。 如果标识符和密钥之间存在显式关联，则关联的键将优先于默认键。

**SetGroupPresharedKey**方法指定默认密钥后，如果稳定存储可用，则发起方应将此密钥存储在非易失性存储器中。 但发起方还应将密钥保留在工作内存中，以便在 IKE 阶段1协商期间快速提供该密钥。 这可以提高密钥交换的效率。

**SetGroupPresharedKey** 属于未发布的 [MSiSCSI \_ SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关 **SetGroupPresharedKey** 方法的参数的说明，请参阅 [**SetGroupPresharedKey \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setgrouppresharedkey_in) 和 [**SetGroupPresharedKey \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setgrouppresharedkey_out) 结构的成员说明。

实现 MSiSCSI SecurityConfigOperations WMI 类的微型端口驱动程序 \_ 必须支持 **SetGroupPresharedKey**。

 

