---
title: MS\_SMHBA\_SASPHYSTATISTICS WMI 类
description: MS\_SMHBA\_SASPHYSTATISTICS WMI 类
ms.assetid: 72afc856-8232-492f-b8d2-4e88dd9fe723
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7aa2011419a088058d243cdbbbf0a4e2643448ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844525"
---
# <a name="ms_smhba_sasphystatistics-wmi-class"></a>MS\_SMHBA\_SASPHYSTATISTICS WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_SASPHYSTATISTICS 类来公开与适配器端口关联的统计信息。 每个端口都应有此类的一个实例。

MS\_SMHBA\_SASPHYSTATISTICS 类在*Hbaapi*中定义如下：

```cpp
class MS_SMHBA_SASPHYSTATISTICS
{
    [WmiDataId(1)]
    sint64 SecondsSinceLastReset;

    [WmiDataId(2)]
    sint64 TxFrames;

    [WmiDataId(3)]
    sint64 TxWords;

    [WmiDataId(4)]
    sint64 RxFrames;

    [WmiDataId(5)]
    sint64 RxWords;

    [WmiDataId(6)]
    sint64 InvalidDwordCount;

    [WmiDataId(7)]
    sint64 RunningDisparityErrorCount;

    [WmiDataId(8)]
    sint64 LossofDwordSyncCount;

    [WmiDataId(9)]
    sint64 PhyResetProblemCount;
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS\_SMHBA\_SASPHYSTATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_sasphystatistics)

没有与此 WMI 类相关联的方法。

 

 





