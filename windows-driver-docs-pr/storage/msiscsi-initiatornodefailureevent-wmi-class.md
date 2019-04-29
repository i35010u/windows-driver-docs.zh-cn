---
title: MSiSCSI\_InitiatorNodeFailureEvent WMI 类
description: MSiSCSI\_InitiatorNodeFailureEvent WMI 类
ms.assetid: 2e542667-4da8-447b-b625-2cd27d52da61
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 66639c294f1eaf5b7b055c9496ce909eea4dd435
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382530"
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

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_InitiatorNodeFailureEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563046)数据结构。

 

 





