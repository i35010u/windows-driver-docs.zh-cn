---
title: MSFC\_FC4STATISTICS WMI 类
description: MSFC\_FC4STATISTICS WMI 类
ms.assetid: 49cd4104-1fe8-46ec-9216-c5c078666c02
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b262a64b51adba4c8afa36a9f86aad3da0163c61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842864"
---
# <a name="msfc_fc4statistics-wmi-class"></a>MSFC\_FC4STATISTICS WMI 类


## <span id="ddk_msfc_fc4statistics_wmi_class_kr"></span><span id="DDK_MSFC_FC4STATISTICS_WMI_CLASS_KR"></span>


支持 T11 委员会*光纤通道 HBA API*规范的 hba 微型端口驱动程序使用 MSFC\_FC4STATISTICS WMI 类来报告类型为\_Nx 的端口上的流量统计信息（对于指示的 FC 协议为响应调用[**GetFC4Statistics**](getfc4statistics.md) WMI 方法。

*Hbaapi*中的 MSFC\_FC4STATISTICS 类定义如下：

```cpp
class MSFC_FC4STATISTICS {
  [WmiDataId(1)] uint64  InputRequests;
  [WmiDataId(2)] uint64  OutputRequests;
  [WmiDataId(3)] uint64  ControlRequests;
  [WmiDataId(4)] uint64  InputMegabytes;
  [WmiDataId(5)] uint64  OutputMegabytes;
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

没有与此 WMI 类相关联的方法。

 

 





