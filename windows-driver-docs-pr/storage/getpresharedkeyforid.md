---
title: GetPresharedKeyForId
description: GetPresharedKeyForId
ms.assetid: cd83d1dc-7aa8-4514-a108-50aee91d272b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d86bdb59a5f3fce3b826d1e86eda5dfd57adba4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354063"
---
# <a name="getpresharedkeyforid"></a>GetPresharedKeyForId


**GetPresharedKeyForId**方法报告是否 Internet 密钥交换 (IKE) 标识负载以用于特定的发起程序标识符 （ID 配置为使用预共享的密钥。

当发起程序使用预共享的密钥在密钥交换时，它将密钥与发起程序标识符相关联，并将标识符和与其关联的键传递给标识数据包的数据部分中的目标 (也称为*标识有效负载*)。 发起方的标识符和与其关联的键在过程中传递的积极或主模式 IKE，第 1 阶段中所述[RFC 2407](https://go.microsoft.com/fwlink/p/?linkid=64840)。 标识有效负载允许标识是安全的方式发起程序，并选择适合于与该特定的发起程序的连接的安全策略的目标。

但是，并非每个身份验证协商使用预共享的密钥。 **GetPresharedKeyForId**方法允许在用户模式服务或管理应用程序以确定是否使用预共享密钥配置的 IKE 标识有效负载为特定的标识符。

此 WMI 方法属于未发布[MSiSCSI\_SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关参数的说明**GetPresharedKeyForId**方法，请参阅成员的说明[ **GetPresharedKeyForId\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff554973)和[ **GetPresharedKeyForId\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff554975)结构。

 

 





