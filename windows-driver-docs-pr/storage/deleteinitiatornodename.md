---
title: DeleteInitiatorNodeName
description: DeleteInitiatorNodeName
ms.assetid: 955ff574-a73b-42fa-8302-1012de5c9fee
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4147aa89857ad760b382f08cdca11ced637a2a6d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192675"
---
# <a name="deleteinitiatornodename"></a>DeleteInitiatorNodeName


**DeleteInitiatorNodeName**方法通知微型端口驱动程序，该驱动程序管理 HBA 发起程序，指示的 iSCSI 节点名称不再有效。 在某些情况下，发起方 Hba 使用质询握手身份验证协议中的节点名称 (CHAP) 身份验证。

实现 [MSiSCSI \_ 操作 WMI 类](msiscsi-operations-wmi-class.md) 的微型端口驱动程序无需支持此方法。

MSiSCSI \_ 操作 WMI 类未发布。 有关 **DeleteInitiatorNodeName** 方法的参数的说明，请参阅 [**DeleteInitiatorNodeName \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_deleteinitiatornodename_in) 和 [**DeleteInitiatorNodeName \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_deleteinitiatornodename_out) 结构的成员说明。

 

