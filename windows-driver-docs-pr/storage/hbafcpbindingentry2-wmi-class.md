---
title: HBAFCPBindingEntry2 WMI 类
description: HBAFCPBindingEntry2 WMI 类
ms.assetid: b9423b59-1d55-4487-bebb-e3eb786fc1be
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b222dd737c0213c96320535bb8dc19681b208d30
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842744"
---
# <a name="hbafcpbindingentry2-wmi-class"></a>HBAFCPBindingEntry2 WMI 类


## <span id="ddk_hbafcpbindingentry2_wmi_class_kr"></span><span id="DDK_HBAFCPBINDINGENTRY2_WMI_CLASS_KR"></span>


支持 T11 委员会*光纤通道 HBA API*规范的 hba 微型端口驱动程序使用 HBAFCPBindingEntry2 类定义操作系统用于标识 SCSI 设备上的逻辑单元的信息与逻辑单元的光纤通道协议（FCP）标识符。 有关 FCP 的说明，请参阅 T11 委员会的*dpANS 光纤通道的 SCSI 规范协议*。 有关 SCSI 标识符与 FCP 标识符之间的绑定的说明，请参阅 T11 委员会*光纤通道 HBA API*规范。

HBAFCPBindingEntry2 类在*Hbaapi*中定义如下：

```cpp
class HBAFCPBindingEntry2 {
  [WmiDataId(1), HBA_BIND_TYPE_QUALIFIERS] HBA_BIND_TYPE  Type;
  [HBAType("HBA_FCPSCSIENTRY"), WmiDataId(4)] HBAScsiID  ScsiId;
  [HBAType("HBA_FCID"), WmiDataId(2)] HBAFCPID  FCPId;
  [HBAType("HBA_LUID"), WmiDataId(3)] uint8  Luid[256];
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**HBAFCPBindingEntry2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry2)

没有与此 WMI 类相关联的方法。

 

 





