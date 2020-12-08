---
title: HBAScsiID WMI 类
description: HBAScsiID WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5fd9763b0ae2d6db114dde0b21b9c005c56c9992
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804481"
---
# <a name="hbascsiid-wmi-class"></a>HBAScsiID WMI 类


## <span id="ddk_hbascsiid_wmi_class_kr"></span><span id="DDK_HBASCSIID_WMI_CLASS_KR"></span>


支持 T11 委员会 *光纤通道 HBA API* 规范的 hba 微型端口驱动程序使用 HBAScsiID 类，通过操作系统中设备的名称及其 SCSI 信息来识别逻辑单元。

HBAScsiID 类在 Hbaapi 中定义如下：

```cpp
class HBAScsiID { 
  [WmiDataId(1)] uint32  ScsiBusNumber;
  [WmiDataId(2)] uint32  ScsiTargetNumber;
  [WmiDataId(3)] uint32  ScsiOSLun;
  [WmiDataId(4),MAX(257)] uint16  OSDeviceName[];
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**HBAScsiID**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid)

没有与此 WMI 类相关联的方法。

 

