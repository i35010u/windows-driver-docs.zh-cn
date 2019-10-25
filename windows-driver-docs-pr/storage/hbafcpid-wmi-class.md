---
title: HBAFCPID WMI 类
description: HBAFCPID WMI 类
ms.assetid: 6b0d0f79-a7a8-4341-955b-2c3068936a1d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f2b8d5193f9afad12b778eea527e8c23c9c02a8a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823801"
---
# <a name="hbafcpid-wmi-class"></a>HBAFCPID WMI 类


## <span id="ddk_hbafcpid_wmi_class_kr"></span><span id="DDK_HBAFCPID_WMI_CLASS_KR"></span>


支持 T11 委员会*光纤通道 HBA API*规范的 hba 微型端口驱动程序使用 HBAFCPID 类为逻辑单元定义光纤通道协议（FCP）标识符。 FCP 标识符指定逻辑单元所在的计算机的名称以及可通过其访问的 HBA 端口。

微型端口驱动程序使用此标识符来构造操作系统用于标识逻辑单元的信息与逻辑单元的 FCP 标识符之间的绑定。 有关此类绑定的信息，请参阅[**HBAFCPBindingEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpbindingentry)。 有关光纤通道协议的说明，请参阅 T11 委员会的*dpANS 光纤通道用于 SCSI*规范的协议。

HBAFCPID 类在*Hbaapi*中定义如下：

```cpp
class HBAFCPID {
  [WmiDataId(1)] uint32  Fcid;
  [HBAType("HBA_WWN"), WmiDataId(2)] uint8  NodeWWN[8];
  [HBAType("HBA_WWN"), WmiDataId(3)] uint8  PortWWN[8];
  [WmiDataId(4)] uint64  FcpLun;
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**HBAFCPID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpid)

没有与此 WMI 类相关联的方法。

 

 





