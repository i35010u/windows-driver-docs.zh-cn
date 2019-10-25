---
title: 有关 DirectSound 客户端的具体信息
description: 有关 DirectSound 客户端的具体信息
ms.assetid: 95ef53d3-572d-478b-839b-0555e9051129
keywords:
- DirectSound WDK 音频，非 PCM 波浪格式
- 非 PCM 音频格式 WDK，DirectSound
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89761885dcca3e73779b3f60057fcfd2e806bb6a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830119"
---
# <a name="specifics-for-directsound-clients"></a>有关 DirectSound 客户端的具体信息


## <span id="specifics_for_directsound_clients"></span><span id="SPECIFICS_FOR_DIRECTSOUND_CLIENTS"></span>


在 Microsoft Windows 2000 和 Windows 98 上，DirectSound 不支持非 PCM 格式，无论 DirectSound 版本如何。 （但是，DirectSound 8 支持 Windows 2000 SP2 和 Windows 98 SE + 修补程序的非 PCM 格式。 此外，Windows XP 及更高版本和 Windows Me 附带的 DirectSound 版本支持非 PCM 格式。）

若要确定 WDM 驱动程序是否支持特定的波形格式，客户端可以尝试在该格式的驱动程序上创建 DSBCAPS\_LOCHARDWARE 缓冲区，并查看尝试是否成功。 DirectSound API 不提供其他方法来发现支持的非 PCM 数据格式。

DirectSound 允许辅助 DSBCAPS\_LOCHARDWARE 缓冲区使用所选驱动程序支持的任何有效[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)或[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)格式。 在驱动程序的支持格式列表中搜索格式时，DirectSound 仅检查包含 KSDATAFORMAT\_说明符的格式\_DSOUND 说明符。

通过首先创建用于描述格式的 WAVEFORMATEX 或 WAVEFORMATEXTENSIBLE 结构，可以扩展 DirectSound 应用程序以使用非 PCM 格式。 接下来，将指向结构的指针加载到传递给**CreateSoundBuffer**方法的 DSBUFFERDESC 结构的**lpwfxFormat**成员中。 使用非 PCM 格式不需要对现有的 DirectSound 代码进行任何其他更改。 请注意，某些非 PCM 格式不可能支持驱动程序通常支持 PCM 数据的控件。 例如，支持以 AC-3 或 WMA Pro 格式编码的数据的数字输出的卡不太可能支持 DSBCAPS\_CTRLPAN 或 DSBCAPS\_CTRLVOLUME 控件。 因此，尝试创建具有这些标志的 DirectSound 缓冲区可能会失败。

通过 VxD 驱动程序或旧式 waveOut 驱动程序的 DirectSound 播放仍限于 PCM;不支持非 PCM 格式。

 

 




