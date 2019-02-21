---
title: PROPSETID\_时间码\_读取器
description: PROPSETID\_时间码\_读取器
ms.assetid: 7f115ba5-a6b7-4bae-a562-7e84a98ef420
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52a7a56f06ce0b21d2367c8896c0cd110f2de1ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521676"
---
# <a name="propsetidtimecodereader"></a>PROPSETID\_时间码\_读取器


## <span id="ddk_propsetid_timecode_reader_ks"></span><span id="DDK_PROPSETID_TIMECODE_READER_KS"></span>


PROPSETID\_时间码\_读取器属性集从外部设备中检索时间代码的信息。

KSPROPERTY\_中的时间码枚举*ksmedia.h*指定此集的属性。

对设置此属性是可选的仅支持外部视频捕获设备的微型驱动程序应实现的支持。

[**KSPROPERTY\_时间码\_读取器**](ksproperty-timecode-reader.md)

[**KSPROPERTY\_ATN\_读取器**](ksproperty-atn-reader.md)

[**KSPROPERTY\_RTC\_读取器**](ksproperty-rtc-reader.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMTimecodeReader**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档） 提供对此集的属性的访问。

 

 





