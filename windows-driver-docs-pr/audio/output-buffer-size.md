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
ms.openlocfilehash: c36eeb51c46b622df398dc796bdb76ec00f976f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364332"
---
# <a name="output-buffer-size"></a>输出缓冲区大小


## <span id="output_buffer_size"></span><span id="OUTPUT_BUFFER_SIZE"></span>


微型端口驱动程序[ **IMiniport::DataRangeIntersection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-datarangeintersection)方法将复制到调用方分配的缓冲区中指定的协商的数据格式的结构。 该方法的*OutputBufferLength*参数以字节为单位指定缓冲区的大小。 请注意，格式结构的大小因所选的格式。 为了避免超出缓冲区末尾写入**DataRangeIntersection**方法应首先验证分配的缓冲区是否足够大，以包含格式。

有关 mono 或立体声格式中，输出缓冲区的最小大小是**sizeof**([**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)) 或**sizeof**([**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_dsound))，取决于是否已选择 WAVEFORMATEX 或 DirectSound 格式。

如果批格式支持两个以上声道[ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)的结尾处嵌入的结构[**KSDATAFORMAT\_WAVEFORMATEX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex)结构展开此项可占用额外的字节数相等的不同之处

**sizeof**([**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-waveformatextensible)) - **sizeof**([**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex))

 

 




