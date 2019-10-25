---
title: HBAFCPScsiEntry WMI 类
description: HBAFCPScsiEntry WMI 类
ms.assetid: b20b1e07-38b4-47b0-a870-51e0865fd256
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1b32ed1fae4a96c40c5ded2a8bb6bf2393b393ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842525"
---
# <a name="hbafcpscsientry-wmi-class"></a>HBAFCPScsiEntry WMI 类


## <span id="ddk_hbafcpscsientry_wmi_class_kr"></span><span id="DDK_HBAFCPSCSIENTRY_WMI_CLASS_KR"></span>


支持 T11 委员会*光纤通道 HBA API*规范的 hba 微型端口驱动程序使用 HBAFCPScsiEntry 类存储操作系统生成的、唯一标识 SCSI 逻辑单元及其适配器的信息。 此类用于在操作系统信息与逻辑单元的 FCP 标识符之间构造绑定。 有关此绑定的说明，请参阅[**HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)。 有关光纤通道协议的说明，请参阅 T11 委员会的*dpANS 光纤通道用于 SCSI*规范的协议。

HBAFCPScsiEntry 类在*Hbaapi*中定义如下：

```cpp
class HBAFCPScsiEntry {
  [HBAType("HBA_FCPID"), WmiDataId(1)] HBAFCPID  FCPId;
  [HBAType("HBA_LUID"), WmiDataId(2)] uint8  Luid[256];
  [HBAType("HBA_SCSIID"), WmiDataId(3)] HBAScsiID  ScsiId;
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**HBAFCPScsiEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpscsientry)

没有与此 WMI 类相关联的方法。

 

 





