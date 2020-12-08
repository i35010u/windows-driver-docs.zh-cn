---
title: ISCSI \_ TARGETMAPPING WMI 类
description: ISCSI \_ TARGETMAPPING WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aef49fd5290aa42386f317a9d6fc43780a6f0ef0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811635"
---
# <a name="iscsi_targetmapping-wmi-class"></a>ISCSI \_ TARGETMAPPING WMI 类


## <span id="ddk_iscsi_targetmapping_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETMAPPING_WMI_CLASS_KR"></span>


ISCSI \_ TARGETMAPPING WMI 类将在发起方主机系统上本地定义的 lun)  (逻辑单元号的集合映射到一组64位 ISCSI lun。 64位 iSCSI LUN 本身不能唯一标识它所表示的逻辑单元。 但是，iSCSI LUN 和逻辑单元所属的目标的名称在网络中的任何位置都可以唯一地标识逻辑单元。

管理应用程序可以使用 ISCSI \_ TARGETMAPPING WMI 类来指定在本地枚举远程逻辑单元时将向其分配的 lun。

此类定义的映射与特定目标登录会话关联。 [MSiSCSI \_ TargetMappings WMI 类](msiscsi-targetmappings-wmi-class.md)描述与特定适配器实例关联的所有映射。

此类在 *Common mof* 中定义为：

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

 

 





