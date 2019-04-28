---
title: MSiSCSI\_InitiatorInstanceFailureEvent WMI 类
description: MSiSCSI\_InitiatorInstanceFailureEvent WMI 类
ms.assetid: 58ddfaf7-d2ec-4b06-8eef-f7b07285963d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9b1f6fd2def03572aed299f39619dbd344d451f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343148"
---
# <a name="msiscsiinitiatorinstancefailureevent-wmi-class"></a>MSiSCSI\_InitiatorInstanceFailureEvent WMI 类


## <span id="ddk_msiscsi_initiatorinstancefailureevent_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORINSTANCEFAILUREEVENT_WMI_CLASS_KR"></span>


MSiSCSI\_InitiatorInstanceFailureEvent WMI 类触发事件时发生了发起方实例失败。

因为此类与存储微型端口驱动程序的特定实例相关联，微型端口驱动程序必须注册使用的微型端口驱动程序管理的特定的物理设备对象 (PDO) 名称的类。

MSiSCSI\_InitiatorInstanceFailureEvent 类中定义*Mgmt.mof*。

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_InitiatorInstanceFailureEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff563028)数据结构。

 

 





