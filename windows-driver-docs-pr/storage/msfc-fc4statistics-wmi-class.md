---
title: MSFC\_FC4STATISTICS WMI 类
description: MSFC\_FC4STATISTICS WMI 类
ms.assetid: 49cd4104-1fe8-46ec-9216-c5c078666c02
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f22986aa6596dc737489bd6b25e1d824307efcdd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542111"
---
# <a name="msfcfc4statistics-wmi-class"></a>MSFC\_FC4STATISTICS WMI 类


## <span id="ddk_msfc_fc4statistics_wmi_class_kr"></span><span id="DDK_MSFC_FC4STATISTICS_WMI_CLASS_KR"></span>


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 MSFC\_FC4STATISTICS WMI 类传递给报表的端口上的流量统计数据类型 Nx\_的端口指示以响应对的调用的 FC 4 协议[ **GetFC4Statistics** ](getfc4statistics.md) WMI 方法。

MSFC\_FC4STATISTICS 类定义中，如下所示*Hbaapi.mof*:

```cpp
class MSFC_FC4STATISTICS {
  [WmiDataId(1)] uint64  InputRequests;
  [WmiDataId(2)] uint64  OutputRequests;
  [WmiDataId(3)] uint64  ControlRequests;
  [WmiDataId(4)] uint64  InputMegabytes;
  [WmiDataId(5)] uint64  OutputMegabytes;
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**MSFC\_FC4STATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff562492)

没有与此 WMI 类相关联的方法。

 

 





