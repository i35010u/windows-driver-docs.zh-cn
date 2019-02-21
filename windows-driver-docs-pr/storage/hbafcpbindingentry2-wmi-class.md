---
title: HBAFCPBindingEntry2 WMI 类
description: HBAFCPBindingEntry2 WMI 类
ms.assetid: b9423b59-1d55-4487-bebb-e3eb786fc1be
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9acb390634053749ecbe75d83e9a7c6eba9382fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523208"
---
# <a name="hbafcpbindingentry2-wmi-class"></a>HBAFCPBindingEntry2 WMI 类


## <span id="ddk_hbafcpbindingentry2_wmi_class_kr"></span><span id="DDK_HBAFCPBINDINGENTRY2_WMI_CLASS_KR"></span>


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 HBAFCPBindingEntry2 类来定义操作系统用来标识上的逻辑单元信息之间的绑定SCSI 设备和逻辑单元的光纤通道协议 (FCP) 标识符。 FCP 的说明，请参阅 T11 委员会*dpANS SCSI 的光纤通道协议*规范。 SCSI 和 FCP 标识符的绑定的说明，请参阅 T11 委员会*光纤通道 HBA API*规范。

HBAFCPBindingEntry2 类定义中，如下所示*Hbaapi.mof*:

```cpp
class HBAFCPBindingEntry2 {
  [WmiDataId(1), HBA_BIND_TYPE_QUALIFIERS] HBA_BIND_TYPE  Type;
  [HBAType("HBA_FCPSCSIENTRY"), WmiDataId(4)] HBAScsiID  ScsiId;
  [HBAType("HBA_FCID"), WmiDataId(2)] HBAFCPID  FCPId;
  [HBAType("HBA_LUID"), WmiDataId(3)] uint8  Luid[256];
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**HBAFCPBindingEntry2**](https://msdn.microsoft.com/library/windows/hardware/ff556035)

没有与此 WMI 类相关联的方法。

 

 





