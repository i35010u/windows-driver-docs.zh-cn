---
title: DirectMusic 流数据格式
description: DirectMusic 流数据格式
ms.assetid: f3aae6c0-6b9d-43fa-9ef1-d6702017f55d
keywords:
- DirectMusic WDK 音频，流数据格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3fee9fdb2a64abf6aeb0b586c7359e409057aef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833520"
---
# <a name="directmusic-stream-data-format"></a>DirectMusic 流数据格式


## <span id="directmusic_stream_data_format"></span><span id="DIRECTMUSIC_STREAM_DATA_FORMAT"></span>


此示例使用[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)结构来描述 DirectMusic 流的数据格式。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT);
  DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
 DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_DIRECTMUSIC);
  DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
```

 

 




