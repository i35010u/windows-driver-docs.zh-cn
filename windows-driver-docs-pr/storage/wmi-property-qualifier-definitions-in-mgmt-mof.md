---
title: Mgmt.mof 中的 WMI 属性限定符定义
description: Mgmt.mof 中的 WMI 属性限定符定义
ms.assetid: 2d8e7e83-6304-459f-b9d8-b40365834bb7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 588511a40c6d7efd18954c0cf18e784180934199
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193047"
---
# <a name="wmi-property-qualifier-definitions-in-mgmtmof"></a>Mgmt.mof 中的 WMI 属性限定符定义


## <span id="ddk_wmi_property_qualifier_definitions_in_mgmt_mof_kr"></span><span id="DDK_WMI_PROPERTY_QUALIFIER_DEFINITIONS_IN_MGMT_MOF_KR"></span>


在 *管理* 中定义的 WMI 限定符指定了 iscsi 发现库和其他管理软件可用来报告从 iSCSI 发起程序检索到的信息的一些数据格式。

*管理 mof*文件定义以下 WMI 属性限定符：

[ISCSI \_ 连接 \_ 状态 \_ 类型 \_ 限定符](iscsi-connection-state-type-qualifiers.md)

[ISCSI \_ 连接 \_ 协议 \_ 类型 \_ 限定符](iscsi-connection-protocol-type-qualifiers.md)

[ISCSI \_ 会话 \_ 类型 \_ 限定符](iscsi-session-type-qualifiers.md)

[ISCSI \_ 标头 \_ 完整性 \_ 类型 \_ 限定符](iscsi-header-integrity-type-qualifiers.md)

[ISCSI \_ 数据 \_ 完整性 \_ 类型 \_ 限定符](iscsi-data-integrity-type-qualifiers.md)

[ISCSI \_ 门户 \_ 类型 \_ 限定符](iscsi-portal-type-qualifiers.md)

[ISCSI \_ 发起程序 \_ 节点 \_ 故障 \_ 类型 \_ 限定符](iscsi-initiator-node-failure-type-qualifiers.md)

[ISCSI \_ 发起程序 \_ 失败 \_ 类型 \_ 限定符](iscsi-initiator-failure-type-qualifiers.md)

如果您将上述某个限定符应用于 WMI 类定义中的数据字段，则它表示您可以将在限定符定义中指示的任何整数值分配给相应的结构成员。

因此，WMI 属性限定符类似于枚举，因为限定符表示一组整数值。 但在 *Iscsimgt* 中，WMI 工具套件不会生成对应于 *管理*中的限定符的枚举声明，这两种方法都不会生成与限定符值相对应的一组符号常量定义。

有关 WMI 属性限定符的一般讨论，请参阅 [Wmi 属性限定符](../kernel/wmi-property-qualifiers.md)。

 

