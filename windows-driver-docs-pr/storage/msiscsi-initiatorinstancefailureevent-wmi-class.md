---
title: MSiSCSI \_ INITIATORINSTANCEFAILUREEVENT WMI 类
description: MSiSCSI \_ INITIATORINSTANCEFAILUREEVENT WMI 类
ms.assetid: 58ddfaf7-d2ec-4b06-8eef-f7b07285963d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f5cdae3121b0d530145f33793d15da65bb9815fc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185889"
---
# <a name="msiscsi_initiatorinstancefailureevent-wmi-class"></a>MSiSCSI \_ INITIATORINSTANCEFAILUREEVENT WMI 类


## <span id="ddk_msiscsi_initiatorinstancefailureevent_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORINSTANCEFAILUREEVENT_WMI_CLASS_KR"></span>


\_当发起方实例发生故障时，MSiSCSI INITIATORINSTANCEFAILUREEVENT WMI 类将触发事件。

由于此类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理 (PDO) 的特定物理设备对象的名称注册该类。

MSiSCSI \_ InitiatorInstanceFailureEvent 类在 *管理 mof*中定义。

```cpp
class MSiSCSI_InitiatorInstanceFailureEvent : WMIEvent {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [read, WmiDataId(1),
    ISCSI_INITIATOR_NODE_FAILURE_TYPE_QUALIFIERS, 
    WmiVersion(1)] 
    ISCSI_INITIATOR_NODE_FAILURE_TYPE  FailureType;
  [read, WmiDataId(2), WmiVersion(1),
    MaxLen(MAX_ISCSI_NAME_LEN)] 
    string  RemoteNodeName;
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ InitiatorInstanceFailureEvent**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_initiatorinstancefailureevent) 数据结构。

 

