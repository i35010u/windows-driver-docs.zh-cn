---
title: MSFC \_ FC4STATISTICS WMI 类
description: MSFC \_ FC4STATISTICS WMI 类
ms.assetid: 49cd4104-1fe8-46ec-9216-c5c078666c02
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 04a909a787245b70e68db544c14d0a3530d3e36a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186891"
---
# <a name="msfc_fc4statistics-wmi-class"></a>MSFC \_ FC4STATISTICS WMI 类


## <span id="ddk_msfc_fc4statistics_wmi_class_kr"></span><span id="DDK_MSFC_FC4STATISTICS_WMI_CLASS_KR"></span>


支持 T11 委员会 *光纤通道 HBA API* 规范的 hba 微型端口驱动程序使用 MSFC \_ FC4STATISTICS WMI 类来报告类型为 Nx 端口的端口上的流量统计信息，以 \_ 响应对 [**GetFC4Statistics**](getfc4statistics.md) WMI 方法的调用。

MSFC \_ FC4STATISTICS 类在 *Hbaapi*中定义如下：

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

[**MSFC \_ FC4STATISTICS**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

没有与此 WMI 类相关联的方法。

 

