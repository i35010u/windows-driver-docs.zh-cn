---
title: DeleteInitiatorNodeName
description: DeleteInitiatorNodeName
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bfd50d6f48cd3c2e5f5059b21b1afacfed2b8741
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835347"
---
# <a name="deleteinitiatornodename"></a>DeleteInitiatorNodeName


**DeleteInitiatorNodeName** 方法通知微型端口驱动程序，该驱动程序管理 HBA 发起程序，指示的 iSCSI 节点名称不再有效。 在某些情况下，发起方 Hba 使用质询握手身份验证协议中的节点名称 (CHAP) 身份验证。

实现 [MSiSCSI \_ 操作 WMI 类](msiscsi-operations-wmi-class.md) 的微型端口驱动程序无需支持此方法。

MSiSCSI \_ 操作 WMI 类未发布。 有关 **DeleteInitiatorNodeName** 方法的参数的说明，请参阅 [**DeleteInitiatorNodeName \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_deleteinitiatornodename_in) 和 [**DeleteInitiatorNodeName \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_deleteinitiatornodename_out) 结构的成员说明。

 

