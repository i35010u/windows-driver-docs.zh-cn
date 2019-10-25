---
title: SetTunnelModeOuterAddress
description: SetTunnelModeOuterAddress
ms.assetid: 0f67a15c-5077-460a-923c-8d86cc79a1bb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2ae9f9f3d1dcec580694a633ba4d3904eb744e1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842607"
---
# <a name="settunnelmodeouteraddress"></a>SetTunnelModeOuterAddress


使用**SetTunnelModeOuterAddress** ，管理应用程序可以指定端口在发起方 HBA 上使用的隧道模式外部地址。

在隧道模式下，内部加密的 IP 数据包嵌套在包含安全网关地址的外部 IP 数据包中。 使用**SetTunnelModeOuterAddress**方法，管理应用程序可以指示与通过指定端口传递的 IP 数据包关联的安全网关的地址。

如果可使用非易失性存储，发起方 HBA 或 HBA 微型端口驱动程序应在非易失性存储中维护默认的隧道模式外部地址

**SetTunnelModeOuterAddress**属于未发布的[MSISCSI\_SecurityConfigOperations WMI 类](msiscsi-securityconfigoperations-wmi-class.md)。 有关**SetTunnelModeOuterAddress**方法的参数的说明，请参阅[**SetTunnelModeOuterAddress\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_settunnelmodeouteraddress_in)和[**SetTunnelModeOuterAddress\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_settunnelmodeouteraddress_out)结构的成员说明。

实现 MSiSCSI\_SecurityConfigOperations WMI 类的微型端口驱动程序必须支持**SetTunnelModeOuterAddress**。

 

 





