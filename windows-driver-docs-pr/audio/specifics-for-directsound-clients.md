---
title: 有关 DirectSound 客户端的具体信息
description: 有关 DirectSound 客户端的具体信息
ms.assetid: 95ef53d3-572d-478b-839b-0555e9051129
keywords:
- DirectSound WDK 音频非 PCM 波形格式
- 非 PCM 音频格式 WDK DirectSound
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e99263af89366e96537056cddb7d1e754f4854c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328635"
---
# <a name="specifics-for-directsound-clients"></a>有关 DirectSound 客户端的具体信息


## <span id="specifics_for_directsound_clients"></span><span id="SPECIFICS_FOR_DIRECTSOUND_CLIENTS"></span>


在 Microsoft Windows 2000 和 Windows 98，DirectSound 不支持非 PCM 格式，而不考虑 DirectSound 版本。 （但是，DirectSound 8 支持非 PCM 格式在 Windows 2000 SP2 和 Windows 98 SE + 修补程序。 此外，版本的 Windows XP 和更高版本中随附的 DirectSound 和 Windows Me，支持非 PCM 格式。）

若要确定 WDM 驱动程序是否支持特定波形格式，客户端可以尝试创建 DSBCAPS\_LOCHARDWARE 缓冲区以该格式保存在驱动程序并查看该尝试是否成功。 DirectSound API 提供了其他方法来发现支持哪些非 PCM 数据格式。

DirectSound 允许辅助 DSBCAPS\_LOCHARDWARE 缓冲区有任何有效[ **WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff538799)或[ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)所选驱动程序支持的格式。 在搜索中支持的格式的驱动程序的列表的格式，DirectSound 只检查格式包含 KSDATAFORMAT\_说明符\_DSOUND 说明符。

您可以扩展 DirectSound 应用程序使用通过首先创建描述格式的 WAVEFORMATEX 或 WAVEFORMATEXTENSIBLE 结构的非 PCM 格式。 接下来，加载到结构的指针**lpwfxFormat**传递给 DSBUFFERDESC 结构中的成员**CreateSoundBuffer**方法。 使用非 PCM 格式不需要对现有 DirectSound 代码的任何其他更改。 请注意，驱动程序通常支持的 PCM 数据的控件不太可能支持某些非 PCM 格式。 例如，ac-3 或 WMA Pro 格式支持的编码的数据的数字输出的卡不太可能支持 DSBCAPS\_CTRLPAN 或 DSBCAPS\_CTRLVOLUME 控件对该数据。 因此，尝试使用这些标志创建 DirectSound 缓冲区可能会失败。

DirectSound 播放，通过 VxD 驱动程序或旧 waveOut 驱动程序是仍受限于 PCM;不支持非 PCM 格式。

 

 




