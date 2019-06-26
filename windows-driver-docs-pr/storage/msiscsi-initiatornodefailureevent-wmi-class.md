---
title: MSiSCSI\_InitiatorNodeFailureEvent WMI 类
description: MSiSCSI\_InitiatorNodeFailureEvent WMI 类
ms.assetid: 2e542667-4da8-447b-b625-2cd27d52da61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 50af3d823d7933ef87c3728b34717dec72ef7c98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370453"
---
# <a name="msiscsiinitiatornodefailureevent-wmi-class"></a>MSiSCSI\_InitiatorNodeFailureEvent WMI 类


## <span id="ddk_msiscsi_initiatornodefailureevent_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORNODEFAILUREEVENT_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorNodeFailureEvent WMI 类触发事件时发生节点故障。

因为此类与存储微型端口驱动程序的特定实例相关联，微型端口驱动程序必须注册使用的微型端口驱动程序管理的特定的物理设备对象 (PDO) 名称的类。

MSiSCSI\_InitiatorNodeFailureEvent WMI 类触发事件时发生节点故障。 此类中定义*Mgmt.mof*。

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_InitiatorNodeFailureEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_msiscsi_initiatornodefailureevent)数据结构。

 

 





