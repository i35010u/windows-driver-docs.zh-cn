---
title: MSFC \_ FCADAPTERHBAATTRIBUTES WMI 类
description: MSFC \_ FCADAPTERHBAATTRIBUTES WMI 类
ms.assetid: fa0ff9c2-e7cc-4000-bd18-ade953e57dcc
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9c66cd6d8c9b86974c367b610a42bf5e6a53a834
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184087"
---
# <a name="msfc_fcadapterhbaattributes-wmi-class"></a>MSFC \_ FCADAPTERHBAATTRIBUTES WMI 类


## <span id="ddk_msfc_fcadapterhbaattributes_wmi_class_kr"></span><span id="DDK_MSFC_FCADAPTERHBAATTRIBUTES_WMI_CLASS_KR"></span>


支持 T11 委员会 *光纤通道 HBA API* 规范的 hba 微型端口驱动程序使用 MSFC \_ FCAdapterHBAAttributes WMI 类来公开与光纤通道适配器关联的属性信息。

MSFC \_ FCAdapterHBAAttributes 类在 *Hbaapi*中定义如下：

```cpp
class MSFC_FCAdapterHBAAttributes {
  [key] 
  string InstanceName;
  boolean Active;
  [Description ("Unique identifier for the adapter. This"
                "identifier must be unique among all"
                "adapters. The same value for the "
                "identifier must be used for the same"
                "adapter in other classes that expose"
                "adapter information") : amended,
   WmiRefClass("MSFC_FibreChannelAdapter"),
   WmiRefProperty("UniqueAdapterId"),
   WmiDataId(1)] uint64  UniqueAdapterId;
  [HBA_STATUS_QUALIFIERS, WmiDataId(2)] HBA_STATUS HBAStatus;
  [HBAType("HBA_WWN"),WmiDataId(3)] uint8  NodeWWN[8];
  [WmiDataId(4)] uint32  VendorSpecificID;
  [WmiDataId(5)] uint32 NumberOfPorts;
  [WmiDataId(6)] string  Manufacturer;
  [MaxLen(64), WmiDataId(7)] string SerialNumber; 
  [MaxLen(256), WmiDataId(8)] string Model; 
  [MaxLen(256), WmiDataId(9)] string ModelDescription; 
  [MaxLen(256), WmiDataId(10)] string NodeSymbolicName; 
  [MaxLen(256), WmiDataId(11)] string HardwareVersion; 
  [MaxLen(256), WmiDataId(12)] string DriverVersion; 
  [MaxLen(256), WmiDataId(13)] string OptionROMVersion; 
  [MaxLen(256), WmiDataId(14)] string FirmwareVersion; 
  [MaxLen(256), WmiDataId(15)] string DriverName; 
  [MaxLen(256), WmiDataId(16)] string MfgDomain;
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ FCAdapterHBAAttributes**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fcadapterhbaattributes)

没有与此 WMI 类相关联的方法。

 

