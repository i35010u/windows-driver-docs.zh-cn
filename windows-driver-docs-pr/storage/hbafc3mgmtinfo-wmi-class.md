---
title: HBAFC3MgmtInfo WMI 类
description: HBAFC3MgmtInfo WMI 类
ms.assetid: 7c3e5b7e-aed9-4d82-91d9-e0c7b8f5ddf6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fe97654f5c4723d16951d88b9901c10af1a4b5d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383100"
---
# <a name="hbafc3mgmtinfo-wmi-class"></a>HBAFC3MgmtInfo WMI 类


## <span id="ddk_hbafc3mgmtinfo_wmi_class_kr"></span><span id="DDK_HBAFC3MGMTINFO_WMI_CLASS_KR"></span>


WMI 客户端使用 HBAFC3MgmtInfo 类来查询与光纤通道适配器相关联的 FC3 管理信息的 HBA 微型端口驱动程序。 FC3 指光纤通道协议的常见服务层。 它定义一组跨多个端口节点的一些常见的服务。 有关常见服务层的说明，请参阅 T11 委员会*光纤通道 HBA API*规范。

HBAFC3MgmtInfo 类定义中，如下所示*Hbaapi.mof*:

```cpp
class HBAFC3MgmtInfo {
  [Description ("Unique identifier for the adapter. This"
    "identifier must be unique among all adapters. "
    "The same value for the identifier must be used "
    "for the same adapter in other classes that expose "
    "adapter information") : amended,
   WmiRefClass("MSFC_FibreChannelAdapter"),
   WmiRefProperty("UniqueAdapterId"), WmiDataId(1) 
     uint64  UniqueAdapterId;
// CIM_FibreChannelAdapter REF
  [HBAType("HBA_WWN"), WmiDataId(2)] uint8  wwn[8];
  [WmiDataId(3)] uint32  unittype;
  [WmiDataId(4)] uint32  PortId;
  [WmiDataId(5)] uint32  NumberOfAttachedNodes;
  [WmiDataId(6)] uint16  IPVersion;
  [WmiDataId(7)] uint16  UDPPort;
  [WmiDataId(8)] uint8  IPAddress[16];
  [WmiDataId(9)] uint16 reserved;
  [WmiDataId(10)] uint16  TopologyDiscoveryFlags;
  [WmiDataId(11)] uint32  reserved1;
};
```

此类定义时编译的 WMI 工具套件，生成[ **HBAFC3MgmtInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556032)数据结构。 没有与此 WMI 类相关联的方法。

 

 





