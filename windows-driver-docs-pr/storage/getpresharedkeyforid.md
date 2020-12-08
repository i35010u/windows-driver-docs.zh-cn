---
title: GetPresharedKeyForId
description: GetPresharedKeyForId
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cbf2192ed6c9046cb0dc71cd17c800018320edb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804545"
---
# <a name="getpresharedkeyforid"></a>GetPresharedKeyForId


**GetPresharedKeyForId** 方法报告是否为特定发起程序标识符 (IKE) 标识有效负载 (ID 配置为使用预共享密钥。

当发起方在密钥交换中使用预共享密钥时，它会将该密钥与发起程序的标识符相关联，并将该标识符及其关联密钥传递到标识包的数据部分中的目标 (也称为 *标识有效负载*) 。 如 [RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)中所述，发起方在主动或 MAIN 模式 IKE 的第1阶段传递标识符及其关联的密钥。 标识负载允许目标以一种安全的方式标识发起方，并选择适合与特定发起程序的连接的安全策略。

但是，并非每个身份验证协商都使用预共享密钥。 **GetPresharedKeyForId** 方法允许用户模式服务或管理应用程序确定是否为特定标识符配置了 IKE 标识有效负载的预共享密钥。

此 WMI 方法属于未发布的 [MSiSCSI \_ SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关 **GetPresharedKeyForId** 方法的参数的说明，请参阅 [**GetPresharedKeyForId \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_getpresharedkeyforid_in) 和 [**GetPresharedKeyForId \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_getpresharedkeyforid_out) 结构的成员说明。

 

