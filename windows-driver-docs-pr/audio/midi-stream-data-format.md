---
title: MIDI 流数据格式
description: MIDI 流数据格式
ms.assetid: c179cf74-7493-4c27-97bd-5eb4d0dffbe6
keywords:
- MIDI 流数据格式 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a83e61b2ae0dc6aba078bbf9f884f0506f471d2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211401"
---
# <a name="midi-stream-data-format"></a>MIDI 流数据格式


## <span id="midi_stream_data_format"></span><span id="MIDI_STREAM_DATA_FORMAT"></span>


此示例使用 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 结构来描述 MIDI 流的数据格式。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT);
  DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
 DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_MIDI);
  DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
```

 

