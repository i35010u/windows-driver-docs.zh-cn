---
title: SetPresharedKeyForId
description: SetPresharedKeyForId
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d8941154b3cf9aa9c517b6d32c1817773f6a86cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817981"
---
# <a name="setpresharedkeyforid"></a>SetPresharedKeyForId


使用 **SetPresharedKeyForId** 方法，管理应用程序可以将特定的预共享密钥与 ID (ID) 相关联，发起方在主动或主模式的 Internet 密钥交换 (IKE) 期间使用该标识符来标识自身。

当发起方在密钥交换中使用预共享密钥时，它会将该密钥与发起方 (的标识符相关联，并将其与 IP 地址关联) 并将该标识符及其关联密钥传递到标识 (数据包的数据部分（也称为 *标识有效负载*) ）中的目标。 如 [RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)中所述，发起方在主动或 MAIN 模式 IKE 的第1阶段传递标识符及其关联的密钥。 标识负载允许目标以一种安全的方式标识发起方，并选择适合与特定发起程序的连接的安全策略。

**SetPresharedKeyForId** 方法指定了预共享密钥后，如果稳定存储可用，则发起方应将其存储在非易失性存储器中。 但发起方还应将预共享密钥保留在工作内存中，以便在 IKE 阶段1协商期间快速使用。 这可以提高密钥交换的效率。 如果发起程序无法使用非易失性内存，则发起方服务将代表发起方存储密钥。

管理应用程序可以使用 **SetPresharedKeyForId** 方法将预共享密钥与特定发起程序标识符相关联。 若要将默认键与所有发起程序的标识符相关联，应用程序可以调用 [SetGroupPresharedKey](setgrouppresharedkey.md) 方法。 如果标识符和键之间存在显式关联，则显式关联指定的键优先于默认键。

**SetPresharedKeyForId** 属于未发布的 [MSiSCSI \_ SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关 **SetPresharedKeyForId** 方法的参数的说明，请参阅 [**SetPresharedKeyForId \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setpresharedkeyforid_in) 和 [**SetPresharedKeyForId \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_setpresharedkeyforid_out) 结构的成员说明。

实现 MSiSCSI SecurityConfigOperations WMI 类的微型端口驱动程序 \_ 必须支持 **SetPresharedKeyForId**。

 

