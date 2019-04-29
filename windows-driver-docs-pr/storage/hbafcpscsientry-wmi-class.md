---
title: HBAFCPScsiEntry WMI 类
description: HBAFCPScsiEntry WMI 类
ms.assetid: b20b1e07-38b4-47b0-a870-51e0865fd256
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b2391ac38f8d7d42f1da98f62b61b52c2e1563f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383092"
---
# <a name="hbafcpscsientry-wmi-class"></a>HBAFCPScsiEntry WMI 类


## <span id="ddk_hbafcpscsientry_wmi_class_kr"></span><span id="DDK_HBAFCPSCSIENTRY_WMI_CLASS_KR"></span>


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 HBAFCPScsiEntry 类来存储生成的唯一标识 SCSI 逻辑单元的操作系统的信息并将其适配器。 此类用于构造为逻辑单元的操作系统信息和 FCP 标识符之间的绑定。 此绑定的说明，请参阅[ **HBAFCPBindingEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556034)。 光纤通道协议的说明，请参阅 T11 委员会*dpANS SCSI 的光纤通道协议*规范。

HBAFCPScsiEntry 类定义中，如下所示*Hbaapi.mof*:

```cpp
class HBAFCPScsiEntry {
  [HBAType("HBA_FCPID"), WmiDataId(1)] HBAFCPID  FCPId;
  [HBAType("HBA_LUID"), WmiDataId(2)] uint8  Luid[256];
  [HBAType("HBA_SCSIID"), WmiDataId(3)] HBAScsiID  ScsiId;
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**HBAFCPScsiEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556040)

没有与此 WMI 类相关联的方法。

 

 





