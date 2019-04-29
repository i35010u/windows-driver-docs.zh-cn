---
title: HBAFCPBindingEntry WMI 类
description: HBAFCPBindingEntry WMI 类
ms.assetid: 58993d0d-2044-430d-b8f6-5ea3b68d460b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8b8321ad5255213e4320db015468247a97786a27
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383094"
---
# <a name="hbafcpbindingentry-wmi-class"></a>HBAFCPBindingEntry WMI 类


## <span id="ddk_hbafcpbindingentry_wmi_class_kr"></span><span id="DDK_HBAFCPBINDINGENTRY_WMI_CLASS_KR"></span>


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 HBAFCPBindingEntry 类来定义操作系统使用 SCSI 设备进行标识的信息之间的绑定和光纤通道协议 (FCP) 设备的标识符。 光纤通道协议的说明，请参阅 T11 委员会*dpANS SCSI 的光纤通道协议*规范。 标识逻辑单元的操作系统数据和 FCP 标识符的绑定的说明，请参阅 T11 委员会*光纤通道 HBA API*规范。

HBAFCPBindingEntry 类定义中，如下所示*Hbaapi.mof*:

```cpp
class HBAFCPBindingEntry {
  [HBAType("HBA_FCPBINDINGTYPE"),
    Values{"TO_D_ID", "TO_WWN", "TO_OTHER"},
    ValueMap{"0", "1", "2"},
    WmiDataId(1)] uint32  Type;
  [HBAType("HBA_FCPSCSIENTRY"), WmiDataId(3)] HBAScsiID  ScsiId;
  [HBAType("HBA_FCID"), WmiDataId(2)] HBAFCPID  FCPId;
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**HBAFCPBindingEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556034)

没有与此 WMI 类相关联的方法。

 

 





