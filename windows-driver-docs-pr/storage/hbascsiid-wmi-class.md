---
title: HBAScsiID WMI 类
description: HBAScsiID WMI 类
ms.assetid: ca2ebe3f-bc0b-4723-8dff-00478d9baac3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 781e5e91d9b470e463c55de93078bf62f5e20f93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385221"
---
# <a name="hbascsiid-wmi-class"></a>HBAScsiID WMI 类


## <span id="ddk_hbascsiid_wmi_class_kr"></span><span id="DDK_HBASCSIID_WMI_CLASS_KR"></span>


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 HBAScsiID 类通过设备的名称标识的逻辑单元中的操作系统和其 SCSI 信息。

HBAScsiID 类 Hbaapi.mof 中定义，如下所示：

```cpp
class HBAScsiID { 
  [WmiDataId(1)] uint32  ScsiBusNumber;
  [WmiDataId(2)] uint32  ScsiTargetNumber;
  [WmiDataId(3)] uint32  ScsiOSLun;
  [WmiDataId(4),MAX(257)] uint16  OSDeviceName[];
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**HBAScsiID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbascsiid)

没有与此 WMI 类相关联的方法。

 

 





