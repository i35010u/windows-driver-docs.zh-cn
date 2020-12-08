---
title: AddConnectionToSession
description: AddConnectionToSession
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1f7e38c48c4ac7e1705f8d3b26ce652534e6225d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804807"
---
# <a name="addconnectiontosession"></a>AddConnectionToSession


**AddConnectionToSession** 方法指示用于管理 iSCSI 发起程序 HBA 的微型端口驱动程序，以将新连接添加到登录会话。

支持 [MSiSCSI \_ 操作类](msiscsi-operations-wmi-class.md) 的微型端口驱动程序必须至少为此方法提供存根，但方法的功能的实现是可选的。 如果该方法未实现添加连接功能，它应该返回错误。

**AddConnectionToSession** 属于未发布的 MSISCSI \_ 操作 WMI 类。 有关 **AddConnectionToSession** 方法的参数的说明，请参阅 [**AddConnectionToSession \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_addconnectiontosession_in) 和 [**AddConnectionToSession \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_addconnectiontosession_out) 结构的成员说明。

 

