---
title: MSFC\_HBAPortStatistics WMI 类
description: MSFC\_HBAPortStatistics WMI 类
ms.assetid: 275e4a50-6500-4a23-a0ae-ddd232da42f0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d2d31243a8e03ebd9a28daaa9b45e11c949a5633
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522658"
---
# <a name="msfchbaportstatistics-wmi-class"></a>MSFC\_HBAPortStatistics WMI 类


## <span id="ddk_msfc_hbaportstatistics_wmi_class_kr"></span><span id="DDK_MSFC_HBAPORTSTATISTICS_WMI_CLASS_KR"></span>


WMI 客户端使用 MSFC\_HBAPortStatistics 类，查询统计信息的 HBA 微型端口驱动程序与 HBA 上的端口。

MSFC\_HBAPPortStatistics 类定义中，如下所示*Hbaapi.mof*:

```cpp
class MSFC_HBAPortStatistics
{
  [ WmiDataId(1) ]
  sint64 SecondsSinceLastReset;
  [ WmiDataId(2) ]
  sint64 TxFrames;
  [ WmiDataId(3) ]
  sint64 TxWords;
  [ WmiDataId(4) ]
  sint64 RxFrames;
  [ WmiDataId(5) ]
  sint64 RxWords;
  [ WmiDataId(6) ]
  sint64 LIPCount;
  [ WmiDataId(7) ]
  sint64 NOSCount;
  [ WmiDataId(8) ]
  sint64 ErrorFrames;
  [ WmiDataId(9) ]
  sint64 DumpedFrames;
  [ WmiDataId(10) ]
  sint64 LinkFailureCount;
  [ WmiDataId(11) ]
  sint64 LossOfSyncCount;
  [ WmiDataId(12) ]
  sint64 LossOfSignalCount;
  [ WmiDataId(13) ]
  sint64 PrimitiveSeqProtocolErrCount;
  [ WmiDataId(14) ]
  sint64 InvalidTxWordCount;
  [WmiDataId(15) ]
  sint64 InvalidCRCCount;
};
```

通过 WMI 工具套件在编译时此类定义将生成以下数据结构：

[**MSFC\_HBAPortStatistics**](https://msdn.microsoft.com/library/windows/hardware/ff562512)

没有与此 WMI 类相关联的方法。

 

 





