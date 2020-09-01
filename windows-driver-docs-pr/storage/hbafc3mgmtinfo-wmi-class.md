---
title: HBAFC3MgmtInfo WMI 类
description: HBAFC3MgmtInfo WMI 类
ms.assetid: 7c3e5b7e-aed9-4d82-91d9-e0c7b8f5ddf6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 73b02cdd6673196c45ec51df93f02afc1ec9c69e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188533"
---
# <a name="hbafc3mgmtinfo-wmi-class"></a>HBAFC3MgmtInfo WMI 类


## <span id="ddk_hbafc3mgmtinfo_wmi_class_kr"></span><span id="DDK_HBAFC3MGMTINFO_WMI_CLASS_KR"></span>


WMI 客户端使用 HBAFC3MgmtInfo 类在 HBA 微型端口驱动程序中查询与光纤通道适配器关联的 FC3 管理信息。 FC3 是指光纤通道协议的公共服务层。 它定义了一组服务，这些服务在节点的多个端口上通用。 有关 "通用服务" 层的说明，请参阅 T11 委员会 *光纤通道 HBA API* 规范。

HBAFC3MgmtInfo 类在 *Hbaapi*中定义如下：

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

由 WMI 工具套件编译时，此类定义生成 [**HBAFC3MgmtInfo**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafc3mgmtinfo) 数据结构。 没有与此 WMI 类相关联的方法。

 

