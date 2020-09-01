---
title: AddConnectionToSession
description: AddConnectionToSession
ms.assetid: c2762e75-8732-4c48-83a9-24ccd39218eb
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9fe8ce545531454d3e51735cf369aefc9f1aa120
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190661"
---
# <a name="addconnectiontosession"></a>AddConnectionToSession


**AddConnectionToSession**方法指示用于管理 iSCSI 发起程序 HBA 的微型端口驱动程序，以将新连接添加到登录会话。

支持 [MSiSCSI \_ 操作类](msiscsi-operations-wmi-class.md) 的微型端口驱动程序必须至少为此方法提供存根，但方法的功能的实现是可选的。 如果该方法未实现添加连接功能，它应该返回错误。

**AddConnectionToSession** 属于未发布的 MSISCSI \_ 操作 WMI 类。 有关 **AddConnectionToSession** 方法的参数的说明，请参阅 [**AddConnectionToSession \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_addconnectiontosession_in) 和 [**AddConnectionToSession \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_addconnectiontosession_out) 结构的成员说明。

 

