---
title: Mgmt.mof 中的 WMI 属性限定符定义
description: Mgmt.mof 中的 WMI 属性限定符定义
ms.assetid: 2d8e7e83-6304-459f-b9d8-b40365834bb7
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 82a2ab76b3ad2623b17851a9d094c5ef3870b7dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357224"
---
# <a name="wmi-property-qualifier-definitions-in-mgmtmof"></a>Mgmt.mof 中的 WMI 属性限定符定义


## <span id="ddk_wmi_property_qualifier_definitions_in_mgmt_mof_kr"></span><span id="DDK_WMI_PROPERTY_QUALIFIER_DEFINITIONS_IN_MGMT_MOF_KR"></span>


在中定义的 WMI 限定符*Mgmt.mof*指定某些 iSCSI 发现库和其他管理软件可以使用报告的信息从 iSCSI 发起程序检索到的数据格式。

*Mgmt.mof*文件定义以下 WMI 属性限定符：

[ISCSI\_连接\_状态\_类型\_限定符](iscsi-connection-state-type-qualifiers.md)

[ISCSI\_连接\_协议\_类型\_限定符](iscsi-connection-protocol-type-qualifiers.md)

[ISCSI\_会话\_类型\_限定符](iscsi-session-type-qualifiers.md)

[ISCSI\_标头\_完整性\_类型\_限定符](iscsi-header-integrity-type-qualifiers.md)

[ISCSI\_数据\_完整性\_类型\_限定符](iscsi-data-integrity-type-qualifiers.md)

[ISCSI\_PORTAL\_TYPE\_QUALIFIERS](iscsi-portal-type-qualifiers.md)

[ISCSI\_发起方\_节点\_失败\_类型\_限定符](iscsi-initiator-node-failure-type-qualifiers.md)

[ISCSI\_发起方\_失败\_类型\_限定符](iscsi-initiator-failure-type-qualifiers.md)

如果您将一个前面的限定符应用于 WMI 类定义中的数据字段时，它表示可分配任何相应的结构成员的限定符的定义中指示的整数值。

因此，WMI 属性限定符类似于一个枚举，因为限定符表示一组整数值。 但 WMI 工具套件不会生成在枚举声明*Iscsimgt.h*对应于中的限定符*Mgmt.mof*，它既不会生成一组符号常量定义的对应于限定符值。

有关 WMI 属性限定符的一般讨论，请参阅[WMI 属性限定符](https://msdn.microsoft.com/library/windows/hardware/ff566365)。

 

 





