---
title: 输出缓冲区大小
description: 输出缓冲区大小
ms.assetid: 386cc6f7-2fab-474a-b997-9ba2457ada0c
keywords:
- 数据交集处理程序 WDK 音频，输出缓冲区大小
- 输出缓冲区 WDK 音频
- 缓冲区大小 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3b2240172bbb759c621d5aa47570007c7f544e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567917"
---
# <a name="output-buffer-size"></a>输出缓冲区大小


## <span id="output_buffer_size"></span><span id="OUTPUT_BUFFER_SIZE"></span>


微型端口驱动程序[ **IMiniport::DataRangeIntersection** ](https://msdn.microsoft.com/library/windows/hardware/ff536764)方法将复制到调用方分配的缓冲区中指定的协商的数据格式的结构。 该方法的*OutputBufferLength*参数以字节为单位指定缓冲区的大小。 请注意，格式结构的大小因所选的格式。 为了避免超出缓冲区末尾写入**DataRangeIntersection**方法应首先验证分配的缓冲区是否足够大，以包含格式。

有关 mono 或立体声格式中，输出缓冲区的最小大小是**sizeof**([**KSDATAFORMAT\_WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff537095)) 或**sizeof**([**KSDATAFORMAT\_DSOUND**](https://msdn.microsoft.com/library/windows/hardware/ff537094))，取决于是否已选择 WAVEFORMATEX 或 DirectSound 格式。

如果批格式支持两个以上声道[ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)的结尾处嵌入的结构[**KSDATAFORMAT\_WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff537095)结构展开此项可占用额外的字节数相等的不同之处

**sizeof**([**WAVEFORMATEXTENSIBLE**](https://msdn.microsoft.com/library/windows/hardware/ff538802)) - **sizeof**([**WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff538799))

 

 




