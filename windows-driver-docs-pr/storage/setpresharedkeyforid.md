---
title: SetPresharedKeyForId
description: SetPresharedKeyForId
ms.assetid: d966fd05-31ac-4774-b970-e4ce3d02a5ba
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 82dbca93b9b8c4e29ebddf0aab6587825a8c429c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341263"
---
# <a name="setpresharedkeyforid"></a>SetPresharedKeyForId


**SetPresharedKeyForId**方法，以将特定的预共享的密钥与发起程序使用在阶段 1 积极或主模式 Internet 密钥的标识自身的标识符 (ID) 相关联的管理应用程序交换 (IKE)。

当发起程序使用预共享的密钥在密钥交换时，它将密钥关联与发起方的标识符 （和 IP 地址），并将标识符和与其关联的键传递给标识数据包的数据部分中的目标 (也称为 < c0 1>  *标识有效负载*)。 发起方的标识符和与其关联的键在过程中传递的积极或主模式 IKE，第 1 阶段中所述[RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)。 标识有效负载允许标识是安全的方式发起程序，并选择适合于与该特定的发起程序的连接的安全策略的目标。

之后**SetPresharedKeyForId**方法指定预共享的密钥、 发起方应该将其存储在非易失性存储非易失性存储是否可用。 但是，发起方还应保留预共享的密钥在工作内存中，以便它将可快速在 IKE 阶段 1 协商过程。 这将提高效率的密钥交换。 未向发起方提供非易失性内存时，发起方服务将存储代表发起方密钥。

管理应用程序可以使用**SetPresharedKeyForId**方法以将预共享的密钥与特定的发起程序标识符相关联。 若要将与所有发起程序的标识符关联的默认密钥，该应用程序可以调用[SetGroupPresharedKey](setgrouppresharedkey.md)方法。 如果标识符和密钥之间存在显式关联，显式关联指定的项优先于默认密钥。

**SetPresharedKeyForId**属于未发布[MSiSCSI\_SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关参数的说明**SetPresharedKeyForId**方法，请参阅成员的说明[ **SetPresharedKeyForId\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565806)和[ **SetPresharedKeyForId\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565810)结构。

微型端口驱动程序实现 MSiSCSI\_SecurityConfigOperations WMI 类必须支持**SetPresharedKeyForId**。

 

 





