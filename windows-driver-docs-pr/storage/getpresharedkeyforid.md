---
title: GetPresharedKeyForId
description: GetPresharedKeyForId
ms.assetid: cd83d1dc-7aa8-4514-a108-50aee91d272b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 489eee3ebee6454f80c0b0fd79ac30faa9412174
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837561"
---
# <a name="getpresharedkeyforid"></a>GetPresharedKeyForId


**GetPresharedKeyForId**方法报告是否将特定发起程序标识符（ID 配置为使用预共享密钥）的 Internet 密钥交换（IKE）标识有效负载。

当发起方在密钥交换中使用预共享密钥时，它会将该密钥与发起程序的标识符相关联，并将该标识符及其关联密钥传递到标识数据包的数据部分中的目标（也称为*标识负载*）。 如[RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)中所述，发起方在主动或 MAIN 模式 IKE 的第1阶段传递标识符及其关联的密钥。 标识负载允许目标以一种安全的方式标识发起方，并选择适合与特定发起程序的连接的安全策略。

但是，并非每个身份验证协商都使用预共享密钥。 **GetPresharedKeyForId**方法允许用户模式服务或管理应用程序确定是否为特定标识符配置了 IKE 标识有效负载的预共享密钥。

此 WMI 方法属于未发布的[MSiSCSI\_SECURITYCONFIGOPERATIONS WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关**GetPresharedKeyForId**方法的参数的说明，请参阅[**GetPresharedKeyForId\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_getpresharedkeyforid_in)和[**GetPresharedKeyForId\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_getpresharedkeyforid_out)结构的成员说明。

 

 





