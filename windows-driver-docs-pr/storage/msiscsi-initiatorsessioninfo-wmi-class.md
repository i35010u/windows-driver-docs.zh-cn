---
title: MSiSCSI \_ INITIATORSESSIONINFO WMI 类
description: MSiSCSI \_ INITIATORSESSIONINFO WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 13094a06d3a75af2ee035d033a8f7c987192a1f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804429"
---
# <a name="msiscsi_initiatorsessioninfo-wmi-class"></a>MSiSCSI \_ INITIATORSESSIONINFO WMI 类


## <span id="ddk_msiscsi_initiatorsessioninfo_wmi_class_kr"></span><span id="DDK_MSISCSI_INITIATORSESSIONINFO_WMI_CLASS_KR"></span>


MSiSCSI \_ INITIATORSESSIONINFO WMI 类公开与属于指示 HBA 发起程序的会话和集合相关联的信息。

由于此类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理 (PDO) 的特定物理设备对象的名称注册该类。

MSiSCSI \_ InitiatorSessionInfo 类在 *管理 mof* 中定义。

```cpp
class MSiSCSI_InitiatorSessionInfo {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [WmiDataId(1), DisplayName("Adapter Id") : amended, 
    DisplayInHex, description("Id that is globally unique to
    each instance of each adapter. Using the address of the 
    Adapter Extension is a good idea.") : amended]
    uint64  UniqueAdapterId;
  [WmiDataId(2), read, DisplayName("Count of Elements in 
    SessionsList array") : amended,
    cpp_quote(
    "\n    // Number of elements in SessionList array\n"),
    Description("Number of elements in SessionList array") : 
    amended] 
    uint32  SessionCount;
  [WmiDataId(3), read, DisplayName("List Of Sessions") :
    amended, Description("Variable length array of sessions.
    SessionCount specifies the number of elements in the 
    array") : amended, WmiSizeIs("SessionCount")]  
    ISCSI_SessionStaticInfo  SessionsList[];
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ InitiatorSessionInfo**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_initiatorsessioninfo) 数据结构。

 

