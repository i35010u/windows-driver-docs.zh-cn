---
title: 音频驱动程序结构
description: 音频驱动程序结构
ms.assetid: 8257342f-474a-42b3-809d-96fdeede398b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e3734729886afe5fb2f203381ab6f9cd88949f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331502"
---
# <a name="audio-drivers-structures"></a>音频驱动程序结构

## <span id="ddk_audio_drivers_structures_ks"></span><span id="DDK_AUDIO_DRIVERS_STRUCTURES_KS"></span>

本部分介绍使用 WDM 音频微型端口驱动程序的结构。 结构的列表如下所示：

[**APO\_REG\_属性**](https://msdn.microsoft.com/library/windows/hardware/dn425140)

[**APOInitBaseStruct**](https://msdn.microsoft.com/library/windows/hardware/jj151545)

[**APOInitSystemEffects**](https://msdn.microsoft.com/library/windows/hardware/jj151546)

[**APOInitSystemEffects2**](https://msdn.microsoft.com/library/windows/hardware/dn659347)

[**AudioFXExtensionParams**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/ns-audioenginebaseapo-audiofxextensionparams)

[**DMUS\_KERNEL\_EVENT**](https://msdn.microsoft.com/library/windows/hardware/ff536340)

[**DRMFORWARD**](https://msdn.microsoft.com/library/windows/hardware/ff536350)

[**DRMRIGHTS**](https://msdn.microsoft.com/library/windows/hardware/ff536355)

[**DS3DVECTOR**](https://msdn.microsoft.com/library/windows/hardware/ff536367)

[**KSAC3\_ALTERNATE\_AUDIO**](https://msdn.microsoft.com/library/windows/hardware/ff537055)

[**KSAC3\_BIT\_STREAM\_MODE**](https://msdn.microsoft.com/library/windows/hardware/ff537077)

[**KSAC3\_DIALOGUE\_LEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537078)

[**KSAC3\_DOWNMIX**](https://msdn.microsoft.com/library/windows/hardware/ff537079)

[**KSAC3\_错误\_隐蔽**](https://msdn.microsoft.com/library/windows/hardware/ff537080)

[**KSAC3\_语言\_代码**](https://msdn.microsoft.com/library/windows/hardware/ff537081)

[**KSAC3\_ROOM\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/ff537082)

[**KSAUDIO\_通道\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff537083)

[**KSAUDIO\_COPY\_PROTECTION**](https://msdn.microsoft.com/library/windows/hardware/ff537084)

[**KSAUDIO\_DYNAMIC\_RANGE**](https://msdn.microsoft.com/library/windows/hardware/ff537085)

[**KSAUDIO\_MIC\_ARRAY\_GEOMETRY**](https://msdn.microsoft.com/library/windows/hardware/ff537087)

[**KSAUDIO\_麦克风\_协调**](https://msdn.microsoft.com/library/windows/hardware/ff537086)

[**KSAUDIO\_MIX\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/ff537090)

[**KSAUDIO\_MIXCAP\_TABLE**](https://msdn.microsoft.com/library/windows/hardware/ff537088)

[**KSAUDIO\_MIXLEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537089)

[**KSAUDIO\_PACKETSIZE\_约束**](https://msdn.microsoft.com/library/windows/hardware/dn965561)

[**KSAUDIO\_PACKETSIZE\_CONSTRAINTS2**](https://msdn.microsoft.com/library/windows/hardware/mt761740)

[**KSAUDIO\_PACKETSIZE\_PROCESSINGMODE\_约束**](https://msdn.microsoft.com/library/windows/hardware/dn965562)

[**KSAUDIO\_POSITION**](https://msdn.microsoft.com/library/windows/hardware/ff537091)

[**KSAUDIO\_POSITIONEX**](https://msdn.microsoft.com/library/windows/hardware/ff537092)

[**KSAUDIO\_PREFERRED\_STATUS**](https://msdn.microsoft.com/library/windows/hardware/ff537093)

[**KSAUDIO\_PRESENTATION\_POSITION**](https://msdn.microsoft.com/library/windows/hardware/hh450865)

[**KSAUDIOENGINE\_缓冲区\_大小\_范围**](https://msdn.microsoft.com/library/windows/hardware/hh450864)

[**KSAUDIOENGINE\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/hh450862)

[**KSAUDIOENGINE\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/hh831854)

[**KSDATAFORMAT\_DSOUND**](https://msdn.microsoft.com/library/windows/hardware/ff537094)

[**KSDATAFORMAT\_WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff537095)

[**KSDATARANGE\_AUDIO**](https://msdn.microsoft.com/library/windows/hardware/ff537096)

[**KSDATARANGE\_音乐**](https://msdn.microsoft.com/library/windows/hardware/ff537097)

[**KSDRMAUDIOSTREAM\_CONTENTID**](https://msdn.microsoft.com/library/windows/hardware/ff537099)

[**KSDSOUND\_BUFFERDESC**](https://msdn.microsoft.com/library/windows/hardware/ff537121)

[**KSDS3D\_BUFFER\_ALL**](https://msdn.microsoft.com/library/windows/hardware/ff537101)

[**KSDS3D\_BUFFER\_CONE\_ANGLES**](https://msdn.microsoft.com/library/windows/hardware/ff537103)

[**KSDS3D\_HRTF\_FILTER\_FORMAT\_MSG**](https://msdn.microsoft.com/library/windows/hardware/ff537104)

[**KSDS3D\_HRTF\_INIT\_MSG**](https://msdn.microsoft.com/library/windows/hardware/ff537106)

[**KSDS3D\_HRTF\_PARAMS\_MSG**](https://msdn.microsoft.com/library/windows/hardware/ff537108)

[**KSDS3D\_ITD\_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff537110)

[**KSDS3D\_ITD\_PARAMS\_MSG**](https://msdn.microsoft.com/library/windows/hardware/ff537114)

[**KSDS3D\_LISTENER\_ALL**](https://msdn.microsoft.com/library/windows/hardware/ff537116)

[**KSDS3D\_LISTENER\_ORIENTATION**](https://msdn.microsoft.com/library/windows/hardware/ff537119)

[**KSJACK\_说明**](ksjack-description.md)

[**KSJACK\_DESCRIPTION2**](ksjack-description2.md)

[**KSJACK\_接收器\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff537140)

[**KSMUSICFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff537142)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSP\_DRMAUDIOSTREAM\_CONTENTID**](https://msdn.microsoft.com/library/windows/hardware/ff537492)

[**KSP\_PINMODE**](https://msdn.microsoft.com/library/windows/hardware/dn457711)

[KSRTAUDIO 结构](https://msdn.microsoft.com/library/windows/hardware/ff537500)

[**KSTELEPHONY\_CALLCONTROL**](https://msdn.microsoft.com/library/windows/hardware/mt169883)

[**KSTELEPHONY\_CALLINFO**](https://msdn.microsoft.com/library/windows/hardware/mt169884)

[**KSTELEPHONY\_PROVIDERCHANGE**](https://msdn.microsoft.com/library/windows/hardware/mt169885)

[**KSTOPOLOGY\_ENDPOINTID**](https://msdn.microsoft.com/library/windows/hardware/mt169886)

[**KSTOPOLOGY\_ENDPOINTIDPAIR**](https://msdn.microsoft.com/library/windows/hardware/mt169887)

[**LOOPEDSTREAMING\_POSITION\_EVENT\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff537505)

[**MDEVICECAPSEX**](https://docs.microsoft.com/windows/desktop/api/mmddk/ns-mmddk-mdevicecapsex)

[**MIDIOPENDESC**](https://msdn.microsoft.com/library/windows/hardware/ff537518)

[**RTAUDIO\_GETREADPACKET\_信息**](https://msdn.microsoft.com/library/windows/hardware/mt169891)

[**RTAUDIO\_SETWRITEPACKET\_INFO**](https://msdn.microsoft.com/library/windows/hardware/mt169892)

[**SOUNDDETECTOR\_PATTERNHEADER**](https://msdn.microsoft.com/library/windows/hardware/dn957513)

[**合成器\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff538460)

[**合成器\_PORTPARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff538467)

[**合成器\_统计信息**](https://msdn.microsoft.com/library/windows/hardware/ff538473)

[**SYNTHCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff538424)

[**SYNTHDOWNLOAD**](https://msdn.microsoft.com/library/windows/hardware/ff538429)

[**SYNTHVOICEPRIORITY\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff538452)

[**SYSAUDIO\_ATTACH\_VIRTUAL\_SOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff538480)

[**SYSAUDIO\_CREATE\_VIRTUAL\_SOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff538485)

[**SYSAUDIO\_INSTANCE\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff538490)

[**SYSAUDIO\_SELECT\_GRAPH**](https://msdn.microsoft.com/library/windows/hardware/ff538500)

[**UNCOMPRESSEDAUDIOFORMAT**](https://docs.microsoft.com/windows/desktop/api/audiomediatype/ns-audiomediatype-uncompressedaudioformat)

[**WAVEFORMATEX**](https://msdn.microsoft.com/library/windows/hardware/ff538799)

[**WAVEFORMATEXTENSIBLE**](https://msdn.microsoft.com/library/windows/hardware/ff538802)
