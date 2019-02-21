---
title: MS\_SMHBA\_SASPHYSTATISTICS WMI 类
description: MS\_SMHBA\_SASPHYSTATISTICS WMI 类
ms.assetid: 72afc856-8232-492f-b8d2-4e88dd9fe723
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 57f77419a5dab6d18461bbe37a3eb83b3d744ae8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522608"
---
# <a name="mssmhbasasphystatistics-wmi-class"></a>MS\_SMHBA\_SASPHYSTATISTICS WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_SASPHYSTATISTICS 类来公开与适配器端口相关联的统计信息。 应为每个端口的此类的一个实例。

MS\_SMHBA\_SASPHYSTATISTICS 类定义，如下所示在*Hbaapi.mof*:

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

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SMHBA\_SASPHYSTATISTICS**](https://msdn.microsoft.com/library/windows/hardware/ff563175)

没有与此 WMI 类相关联的方法。

 

 





