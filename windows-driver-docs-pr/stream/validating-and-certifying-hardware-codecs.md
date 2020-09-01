---
title: 验证和认证硬件编解码器
description: 验证和验证硬件编解码器
ms.assetid: 8cf96aac-78ba-41f0-b9d0-48948f704262
keywords:
- 硬件编解码器 WDK AVStream，验证
- 硬件编解码器 WDK AVStream，验证
- 硬件编解码器支持 WDK AVStream、验证和认证
ms.date: 06/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: f2e05de79a16bc79e1f3177ec550cae990803cd2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184369"
---
# <a name="validating-and-certifying-hardware-codecs"></a>验证和验证硬件编解码器

如果供应商提供的 AVStream 微型驱动程序包括基于硬件的编解码器支持，或已实现自定义 MFT 以支持硬件，则必须提供一个 x.509 证书链，在驱动程序 INF 文件中指定一个 "业绩" 值，并 \_ 在驱动程序中实施 KSPROPSETID OPMVideoOutput。

## <a name="obtaining-a-x509-certificate"></a>获取 x.509 证书

硬件支持的媒体基础转换 (MFT) 编码器或解码器必须提供一个有效的 Microsoft 签名 x.509 证书，该证书指定 CodecMeritCertificationPolicy EKU (扩展密钥用法) 证书扩展。 若要为硬件加速编解码器授权，必须参与 PVP-OPM 许可计划。 若要请求许可材料，请联系 [Windows Media License 协议](mailto://wmla@microsoft.com) 别名。

## <a name="specifying-merit"></a>指定优点

在 INF 文件的 AddReg 节中，设置 DWORD 类型 MFTMerit 注册表值：

```INF
[myVideoDecoder.Reader.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%shedVideoDecoder.Reader.FriendlyName%
HKR,,MFTMerit,0x00010001,7
```

## <a name="implementing-kspropsetid_opmvideooutput"></a>实现 KSPROPSETID \_ OPMVideoOutput

KSPROPSETID \_ OPMVideoOutput 属性集显示在用于 Windows 7 和更高版本的 Windows SDK 中的 *Ksopmapi* 和 *Opmapi* 头文件中。

从 *Ksopmapi* 文件的以下摘录中定义属性集和方法：

```cpp
#ifdef DEFINE_GUIDSTRUCT
#define STATIC_KSPROPSETID_OPMVideoOutput \
0x6f414bb, 0xf43a, 0x4fe2, 0xa5, 0x66, 0x77, 0x4b, 0x4c, 0x81, 0xf0, 0xdb
DEFINE_GUIDSTRUCT("06F414BB-F43A-4fe2-A566-774B4C81F0DB", KSPROPSETID_OPMVideoOutput);
#define KSPROPSETID_OPMVideoOutput DEFINE_GUIDNAMED(KSPROPSETID_OPMVideoOutput)
#endif

typedef enum
{
    //  Output is OPM_RANDOM_NUMBER followed by certificate
    KSMETHOD_OPMVIDEOOUTPUT_STARTINITIALIZATION = 0,

    //  Input OPM_ENCRYPTED_INITIALIZATION_PARAMETERS
    //  Output OPM_STANDARD_INFORMATION
    KSMETHOD_OPMVIDEOOUTPUT_FINISHINITIALIZATION = 1,

    //  Input is OPM_GET_INFO_PARAMETERS, output is OPM_REQUESTED_INFORMATION
    //  Use KsMethod - both input and output in the buffer (not after the KSMETHOD structure)
    KSMETHOD_OPMVIDEOOUTPUT_GETINFORMATION = 2
} KSMETHOD_OPMVIDEOOUTPUT;
```

用户模式组件 \_ 通过 AVStream 代理 MFT 上的 **IKsControl** 接口访问 KSPROPSETID OPMVideoOutput。 有关显示 OPMVideoOutput 方法处理程序例程实现的代码示例，请参阅 [编解码器验证](codec-merit-validation.md)。

有关 OPM 的特定于驱动程序的信息，请参阅 [支持输出保护管理器](../display/supporting-output-protection-manager.md)。

有关 OPM 的特定于应用程序的信息，请参阅 [使用输出保护管理器](/windows/win32/medfound/using-output-protection-manager)。