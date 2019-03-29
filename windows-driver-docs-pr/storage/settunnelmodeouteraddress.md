---
title: SetTunnelModeOuterAddress
description: SetTunnelModeOuterAddress
ms.assetid: 0f67a15c-5077-460a-923c-8d86cc79a1bb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b339a44e37ef94b1a7fc6482c8df593ff4f8002b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575510"
---
# <a name="settunnelmodeouteraddress"></a>SetTunnelModeOuterAddress


**SetTunnelModeOuterAddress**允许管理的应用程序指定一个端口使用 HBA 发起程序的隧道模式外部地址。

在隧道模式下，内部加密 IP 数据包将嵌套在外部 IP 数据包包含安全网关的地址。 **SetTunnelModeOuterAddress**方法允许管理的应用程序指示与通过指定端口的 IP 数据包相关联的安全网关的地址。

发起方 HBA 或 HBA 微型端口驱动程序应保留的默认隧道模式外部地址中非易失性存储非易失性存储是否可用

**SetTunnelModeOuterAddress**属于未发布[MSiSCSI\_SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关参数的说明**SetTunnelModeOuterAddress**方法，请参阅成员的说明[ **SetTunnelModeOuterAddress\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff566187)并[ **SetTunnelModeOuterAddress\_出**](https://msdn.microsoft.com/library/windows/hardware/ff566190)结构。

微型端口驱动程序实现 MSiSCSI\_SecurityConfigOperations WMI 类必须支持**SetTunnelModeOuterAddress**。

 

 





