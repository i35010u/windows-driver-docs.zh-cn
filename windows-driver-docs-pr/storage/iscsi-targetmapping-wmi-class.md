---
title: ISCSI\_TargetMapping WMI 类
description: ISCSI\_TargetMapping WMI 类
ms.assetid: b2c4634a-852b-471a-8764-025780e36c0f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 70477f5fd6992813b7796db21b0b56db2be70e95
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546904"
---
# <a name="iscsitargetmapping-wmi-class"></a>ISCSI\_TargetMapping WMI 类


## <span id="ddk_iscsi_targetmapping_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETMAPPING_WMI_CLASS_KR"></span>


ISCSI\_TargetMapping WMI 类将映射到 64 位 iSCSI Lun 的组的发起程序的主机系统本地定义的逻辑单元号 (Lun) 的集合。 单独的 64 位 iSCSI LUN 不唯一标识它所代表的逻辑单元。 但是，iSCSI LUN 和名称的目标的逻辑单元属于 does 唯一地标识网络中的任意位置的逻辑单元。

管理应用程序可以使用 ISCSI\_TargetMapping WMI 类，以指定什么 Lun 将分配给远程逻辑单元在本地枚举时。

此类定义的映射是与特定目标登录会话关联。 [MSiSCSI\_TargetMappings WMI 类](msiscsi-targetmappings-wmi-class.md)描述所有与特定适配器实例相关联的映射。

此类定义中，如下所示*Common.mof*。

```cpp
class ISCSI_TargetMapping {
  [WmiDataId(1), description("OS Scsi bus number target 
    is mapped to. If 0xffffffff then any value can be picked
    by the miniport.") : amended]
    uint32  OSBus;
  [WmiDataId(2), description("OS Scsi Target number target
    is mapped to. If 0xffffffff then any value can be picked
    by the miniport.") : amended]
    uint32  OSTarget;
  [WmiDataId(3), Description("Unique Session ID for the 
    target mapping") : amended] 
    uint64  UniqueSessionId;
  [WmiDataId(4), description("Count of LUNs mapped for this 
    target") : amended]
    uint32  LUNCount;
  [WmiDataId(5), MaxLen(MAX_ISCSI_NAME_LEN),
     description("Target Name") : amended]
    string  TargetName;
  [WmiDataId(6), Description("TRUE if session created from a
    persistent login") : amended]
    boolean  FromPersistentLogin;
  [WmiDataId(7), WmiSizeIs("LunCount"),
    description("List of LUNs mapped for this target") : 
    amended]
    ISCSI_LUNList  LUNList[];
};
```

 

 





