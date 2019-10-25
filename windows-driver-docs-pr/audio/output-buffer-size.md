---
title: 输出缓冲区大小
description: 输出缓冲区大小
ms.assetid: 386cc6f7-2fab-474a-b997-9ba2457ada0c
keywords:
- 数据交集处理程序 WDK 音频，输出缓冲区大小
- 输出缓冲 WDK 音频
- 缓冲区大小 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50a62ecf80dc891555c0261378ec321809783346
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832548"
---
# <a name="output-buffer-size"></a>输出缓冲区大小


## <span id="output_buffer_size"></span><span id="OUTPUT_BUFFER_SIZE"></span>


微型端口驱动程序的[**IMiniport：:D atarangeintersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)方法将指定协商数据格式的结构复制到由调用方分配的缓冲区中。 方法的*OutputBufferLength*参数指定缓冲区的大小（以字节为单位）。 请注意，格式结构的大小因所选格式而异。 为了避免写入超过缓冲区的末尾， **DataRangeIntersection**方法应首先验证分配的缓冲区是否足够大以包含格式。

对于 mono 或立体声格式，输出缓冲区的最小大小为**sizeof**（[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)）或**sizeof**（[**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)），具体取决于 WAVEFORMATEX 或 DirectSound已选择 "格式"。

如果波形格式支持两个以上的通道，则嵌入在[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)结构末尾的[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)结构将展开，以占用等于此差异的额外字节数

**sizeof**（[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)）- **sizeof**（[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)）

 

 




