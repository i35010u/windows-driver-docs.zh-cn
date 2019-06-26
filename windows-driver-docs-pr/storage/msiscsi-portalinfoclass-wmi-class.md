---
title: MSiSCSI\_PortalInfoClass WMI 类
description: MSiSCSI\_PortalInfoClass WMI 类
ms.assetid: f22c36a9-28be-4de1-9e80-0f0c1bd6473d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 218de0b4f5f1d84cf714ce8d8499417a0bf0406a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384685"
---
# <a name="msiscsiportalinfoclass-wmi-class"></a>MSiSCSI\_PortalInfoClass WMI 类


## <span id="ddk_msiscsi_portalinfoclass_wmi_class_kr"></span><span id="DDK_MSISCSI_PORTALINFOCLASS_WMI_CLASS_KR"></span>


MSiSCSI\_PortalInfoClass WMI 类公开的 iSCSI 门户集合有关的信息。

因为此类与存储微型端口驱动程序的特定实例相关联，微型端口驱动程序必须注册使用的微型端口驱动程序管理的特定的物理设备对象 (PDO) 名称的类。

MSiSCSI\_PortalInfoClass 类中定义*Mgmt.mof*。

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_PortalInfoClass** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_msiscsi_portalinfoclass)数据结构。

 

 





