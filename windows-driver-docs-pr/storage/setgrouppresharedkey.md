---
title: SetGroupPresharedKey
description: SetGroupPresharedKey
ms.assetid: 7dedcc62-4ad6-42d5-a461-b0a69c9c97cd
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1e357d03f819bdc5d10c6ac35c6e645749d272cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541500"
---
# <a name="setgrouppresharedkey"></a>SetGroupPresharedKey


**SetGroupPresharedKey**方法允许管理的应用程序配置为使用指定的预共享的密钥，只要密钥是必需的但没有键是会话标识符 (ID) 与当前相关联的 HBA 发起程序

当发起程序使用预共享的密钥在密钥交换时，它将密钥与发起程序标识符相关联，并将标识符和与其关联的键传递给标识数据包的数据部分中的目标 (也称为*标识有效负载*)。 发起方的标识符和与其关联的键在过程中传递的积极或主模式 Internet 密钥交换 (IKE) 第一阶段中所述[RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)。 标识有效负载允许标识是安全的方式发起程序，并选择适合于与该特定的发起程序的连接的安全策略的目标。

**SetGroupPresharedKey**方法配置发起程序要将默认预共享的密钥用于尚不与键关联的标识符。 若要显式之间建立关联的键和一个特定的发起程序标识符，管理应用程序必须调用[SetPresharedKeyForId](setpresharedkeyforid.md)方法。 如果标识符和密钥，该关联，优先于默认密钥的密钥之间存在显式关联。

之后**SetGroupPresharedKey**方法指定的默认密钥、 非易失性存储是否可用发起方应将此密钥存储在非易失性存储中。 但是，发起方应该还将密钥保存在工作内存中，以便它将可快速在 IKE 阶段 1 协商过程。 这将提高效率的密钥交换。

**SetGroupPresharedKey**属于未发布[MSiSCSI\_SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关参数的说明**SetGroupPresharedKey**方法，请参阅成员的说明[ **SetGroupPresharedKey\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565695)和[ **SetGroupPresharedKey\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565697)结构。

微型端口驱动程序实现 MSiSCSI\_SecurityConfigOperations WMI 类必须支持**SetGroupPresharedKey**。

 

 





