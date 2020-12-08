---
title: MSiSCSI \_ PORTALINFOCLASS WMI 类
description: MSiSCSI \_ PORTALINFOCLASS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9a28240f533904838ced539345009c311ecab3bc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796469"
---
# <a name="msiscsi_portalinfoclass-wmi-class"></a>MSiSCSI \_ PORTALINFOCLASS WMI 类


## <span id="ddk_msiscsi_portalinfoclass_wmi_class_kr"></span><span id="DDK_MSISCSI_PORTALINFOCLASS_WMI_CLASS_KR"></span>


MSiSCSI \_ PORTALINFOCLASS WMI 类公开有关 iSCSI 门户集合的信息。

由于此类与存储微型端口驱动程序的特定实例相关联，因此微型端口驱动程序必须使用微型端口驱动程序管理 (PDO) 的特定物理设备对象的名称注册该类。

MSiSCSI \_ PortalInfoClass 类在 *管理 mof* 中定义。

```cpp
class MSiSCSI_PortalInfoClass {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [WmiDataId(1), read, DisplayName("Count of Elements in
    iScsiPortalInfo array") : amended,
    cpp_quote(
    "\n    // Number of elements in  iScsiPortalInfo
    array\n"),
    Description("Number of elements in iScsiPortalInfo
    array") : amended] 
    uint32  PortalInfoCount;
  [WmiDataId(2), read, DisplayName("List Of Portals") :
    amended, Description("Variable length array of
    iScsiPortalInfo. PortalInfoCount specifies the 
    number of elements in the array") : amended,
    WmiSizeIs("PortalInfoCount")] 
    ISCSI_PortalInfo  PortalInformation[];
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ PortalInfoClass**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_portalinfoclass) 数据结构。

 

