---
title: HBAFCPID WMI 类
description: HBAFCPID WMI 类
ms.assetid: 6b0d0f79-a7a8-4341-955b-2c3068936a1d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a11b0843b31e1d804c6e9ab47a0d26da778ede40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546996"
---
# <a name="hbafcpid-wmi-class"></a>HBAFCPID WMI 类


## <span id="ddk_hbafcpid_wmi_class_kr"></span><span id="DDK_HBAFCPID_WMI_CLASS_KR"></span>


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 HBAFCPID 类来定义为逻辑单元的光纤通道协议 (FCP) 标识符。 FCP 标识符指定的名称的逻辑单元将位于的计算机以及通过它可以访问的 HBA 端口。

微型端口驱动程序使用此标识符为逻辑单元中构造操作系统用于标识逻辑单元的信息和 FCP 标识符之间的绑定。 这种类型的绑定有关的信息，请参阅[ **HBAFCPBindingEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556034)。 光纤通道协议的说明，请参阅 T11 委员会*dpANS SCSI 的光纤通道协议*规范。

HBAFCPID 类定义中，如下所示*Hbaapi.mof*:

```cpp
class HBAFCPID {
  [WmiDataId(1)] uint32  Fcid;
  [HBAType("HBA_WWN"), WmiDataId(2)] uint8  NodeWWN[8];
  [HBAType("HBA_WWN"), WmiDataId(3)] uint8  PortWWN[8];
  [WmiDataId(4)] uint64  FcpLun;
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**HBAFCPID**](https://msdn.microsoft.com/library/windows/hardware/ff556038)

没有与此 WMI 类相关联的方法。

 

 





