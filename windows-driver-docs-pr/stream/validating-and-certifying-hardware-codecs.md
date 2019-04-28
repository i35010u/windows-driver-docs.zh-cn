---
title: 验证和认证硬件编解码器
description: 验证和认证硬件编解码器
ms.assetid: 8cf96aac-78ba-41f0-b9d0-48948f704262
keywords:
- 硬件编解码器 WDK AVStream 验证
- 硬件编解码器 WDK AVStream 认证
- 硬件编解码器支持 WDK AVStream，验证和认证
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 679ba0e2cb5db52f0834cb430bcb1339f0c71c4c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337812"
---
# <a name="validating-and-certifying-hardware-codecs"></a>验证和认证硬件编解码器


如果你供应商提供 AVStream 微型驱动程序提供基于硬件的编解码器支持，或已实现自定义的 MFT 以支持您的硬件，您必须提供 X.509 证书链中，在驱动程序 INF 文件中，指定荣誉奖值和实现 KSPROPSETID\_OPMVideoOutput 驱动程序中的。

### <a name="obtaining-an-x509-certificate"></a>**获取 X.509 证书**

媒体基础转换 (MFT) 编码器或解码器所支持的硬件必须提供有效的 Microsoft 签名的 X.509 证书，指定 CodecMeritCertificationPolicy EKU （扩展密钥用法） 证书扩展。 若要向硬件加速编解码器，必须参与 PVP OPM 许可计划。 若要请求授权的材料，请联系[Windows 媒体许可协议](mailto://wmla@microsoft.com)别名。

### <a name="specifying-merit"></a>**指定价值**

在您的 INF 文件 AddReg 部分中，DWORD 类型 MFTMerit 注册表值的设置：

```INF
[myVideoDecoder.Reader.AddReg]
HKR,,CLSID,,%Proxy.CLSID%
HKR,,FriendlyName,,%shedVideoDecoder.Reader.FriendlyName%
HKR,,MFTMerit,0x00010001,7
```

### <a name="implementing-kspropsetidopmvideooutput"></a>**实现 KSPROPSETID\_OPMVideoOutput**

KSPROPSETID\_中公开 OPMVideoOutput 属性集*Ksopmapi.h*并*Opmapi.h*标头文件，在 Windows SDK 适用于 Windows 7 和更高版本中随附。

以下内容摘自中定义的属性集和方法*Ksopmapi.h*文件：

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

用户模式组件访问 KSPROPSETID\_通过 OPMVideoOutput **IKsControl** AVStream 代理 MFT 上的接口。 有关显示 OPMVideoOutput 方法的实现处理程序例程的代码示例，请参阅[编解码器荣誉奖验证](codec-merit-validation.md)。

有关 OPM 特定于驱动程序的信息，请参阅[支持输出保护管理器](https://msdn.microsoft.com/library/windows/hardware/ff569879)。 有关 OPM 特定于应用程序的信息，请参阅[使用输出 Protection Manager](https://go.microsoft.com/fwlink/p/?linkid=155059)。
