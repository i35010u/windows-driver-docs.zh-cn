---
title: MSFC \_ HBAPORTSTATISTICS WMI 类
description: MSFC \_ HBAPORTSTATISTICS WMI 类
ms.assetid: 275e4a50-6500-4a23-a0ae-ddd232da42f0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 57f3907fb7d5b91c58c84bc10565ff46631c03cc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185895"
---
# <a name="msfc_hbaportstatistics-wmi-class"></a>MSFC \_ HBAPORTSTATISTICS WMI 类


## <span id="ddk_msfc_hbaportstatistics_wmi_class_kr"></span><span id="DDK_MSFC_HBAPORTSTATISTICS_WMI_CLASS_KR"></span>


WMI 客户端使用 MSFC \_ HBAPortStatistics 类来查询 hba 微型端口驱动程序，以获取与 hba 上端口相关的统计信息。

MSFC \_ HBAPPortStatistics 类在 *Hbaapi*中定义如下：

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

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ HBAPortStatistics**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportstatistics)

没有与此 WMI 类相关联的方法。

 

