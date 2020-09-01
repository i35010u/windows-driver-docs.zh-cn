---
title: MSiSCSI \_ INITIATORNODEFAILUREEVENT WMI 类
description: MSiSCSI \_ INITIATORNODEFAILUREEVENT WMI 类
ms.assetid: 2e542667-4da8-447b-b625-2cd27d52da61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 19fef874dacaac7db86a2771dcfc4c9612ad23d7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190941"
---
# <a name="msiscsi_initiatornodefailureevent-wmi-class"></a>MSiSCSI \_ INITIATORNODEFAILUREEVENT WMI 类


## <span id="ddk_msiscsi_initiatornodefailureevent_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORNODEFAILUREEVENT_WMI_CLASS_KR"></span>


\_当节点发生故障时，MSiSCSI INITIATORNODEFAILUREEVENT WMI 类将触发事件。

由于此类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理 (PDO) 的特定物理设备对象的名称注册该类。

\_当节点发生故障时，MSiSCSI INITIATORNODEFAILUREEVENT WMI 类将触发事件。 此类在 *管理 mof*中定义。

```cpp
class MSiSCSI_InitiatorNodeFailureEvent : WMIEvent {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [read, WmiDataId(1), WmiTimeStamp, WmiVersion(1)] 
    uint64  FailureTime;
  [read, WmiDataId(2),
    ISCSI_INITIATOR_FAILURE_TYPE_QUALIFIERS, WmiVersion(1)] 
    ISCSI_INITIATOR_FAILURE_TYPE  FailureType;
  [read, WmiDataId(3), WmiVersion(1),
    MaxLen(MAX_ISCSI_NAME_LEN)] 
    string  TargetFailureName;
  [read, WmiDataId(4), WmiVersion(1)] 
  ISCSI_IP_Address  TargetFailureAddr;
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ InitiatorNodeFailureEvent**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_initiatornodefailureevent) 数据结构。

 

