---
title: HBAFCPBindingEntry WMI 类
description: HBAFCPBindingEntry WMI 类
ms.assetid: 58993d0d-2044-430d-b8f6-5ea3b68d460b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2fe6daf3abcff6c3009a378aaa6855d81256d9c5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188821"
---
# <a name="hbafcpbindingentry-wmi-class"></a>HBAFCPBindingEntry WMI 类


## <span id="ddk_hbafcpbindingentry_wmi_class_kr"></span><span id="DDK_HBAFCPBINDINGENTRY_WMI_CLASS_KR"></span>


支持 T11 委员会 *光纤通道 HBA API* 规范的 hba 微型端口驱动程序使用 HBAFCPBindingEntry 类定义操作系统用于标识 SCSI 设备的信息与设备的光纤通道协议 (FCP) 标识符之间的绑定。 有关光纤通道协议的说明，请参阅 T11 委员会的 *dpANS 光纤通道用于 SCSI* 规范的协议。 有关标识逻辑单元和 FCP 标识符的操作系统数据之间的此绑定的说明，请参阅 T11 委员会 *光纤通道 HBA API* 规范。

HBAFCPBindingEntry 类在 *Hbaapi*中定义如下：

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

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**HBAFCPBindingEntry**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)

没有与此 WMI 类相关联的方法。

 

