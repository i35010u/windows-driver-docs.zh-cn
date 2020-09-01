---
title: SetupPreferredAudioDevices
description: SetupPreferredAudioDevices
ms.assetid: cc6b7da4-335d-4629-ba54-32aa32a1eb09
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20a10a315a20ec141674df470685d76553c82e8b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210403"
---
# <a name="setuppreferredaudiodevices"></a>SetupPreferredAudioDevices


## <span id="ddk_setuppreferredaudiodevices_ks"></span><span id="DDK_SETUPPREFERREDAUDIODEVICES_KS"></span>


SetupPreferredAudioDevices 关键字表示首选音频设备，即音频系统在系统包含一个或多个音频设备时默认情况下启用的设备。 此关键字是特定于媒体类的，由 Microsoft Windows Millennium Edition/Windows 98、Microsoft Windows 2000、Windows XP 和 Windows Vista 支持。 Windows 7 中不支持 SetupPreferredAudioDevicesis。

创建音频设备时，应用程序可以选择使用默认 (或首选) 设备，而不是显式指定设备。  (示例，请参阅 Microsoft Windows SDK 文档中的 [**waveOutOpen**](/previous-versions/dd743866(v=vs.85)) 和 **DirectSoundCreate** 函数的说明。 ) 

音频系统将在系统注册表中跟踪当前首选音频设备。 当用户通过安装新的音频设备升级系统时，安装设备的专有 INF 文件通常会更新注册表，以将新设备指定为首选音频设备。

SetupPreferredAudioDevices 关键字可以出现在注册表更新指令中的 " **添加注册表" 部分** 中 (参阅 [**inf AddReg 指令**](../install/inf-addreg-directive.md)) 的音频设备的 inf 文件。 此指令的格式如下：

*rootkey*， \[ *reg 子项* \] SetupPreferredAudioDevices \[ *flags* \] ， \[ *dword 值*\]

指令指示音频系统使用设备的音频功能作为播放声音、录音和 MIDI 音乐的默认值。 安装之后，这三个默认值将显示在 " **音频** " 选项卡下的 "声音和多媒体" 控制面板中。用户可以使用 "控制面板" 更改默认设备。

指令的 *dword 值* 参数指定一个 dword 值，该值应为非零值才能启用指令。 如果此值为零，则指令不起作用。 由于 Windows Me/98 不支持 REG \_ DWORD 注册表数据类型，因此， *dword 值* 通常表示为4字节的注册表 \_ 二进制类型，而不是 dword (例如，如 "01，00，00，00" 而不是 "0x00000001" ) 。 可以通过将指令的*flags*参数设置为 "1" (FLG ADDREG BINVALUETYPE) ，以原始二进制格式指定*dword 值*参数 \_ \_ 。

此指令在设备驱动程序安装时生效。 如果在安装新设备时，另一台设备占用首选设备角色，则该指令会使新设备担任首选设备的角色，从而将其他设备从此角色中取代。

升级或重新安装已安装的设备的驱动程序时，您可能希望避免更改用户当前首选设备，以便播放声音、录制声音以及 MIDI 音乐。 如果是这样，请 \_ \_ 在 *flags* 参数中设置 FLG ADDREG NOCLOBBER 位，这会使指令只有在这是设备的初始安装时才会生效。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例是 INF 文件的一部分，该文件演示如何使用 SetupPreferredAudioDevices 关键字：

```inf
  AddReg = XYZ-Audio-Device.AddReg
  ...
  [XYZ-Audio-Device.AddReg]
  HKR,,SetupPreferredAudioDevices,3,01,00,00,00
```

该示例末尾的指令指定名为 "XYZ-Audio-Device" 的设备现在是首选音频设备。 HKR 是音频设备在注册表中的根密钥。 *Flags*参数设置为3，即 FLG \_ ADDREG \_ BINVALUETYPE 和 FLG \_ ADDREG NOCLOBBER 的按位 or \_ 。 如果设备已安装并且仅升级其驱动程序，则后者会阻止设备的现有首选设备注册表项被覆盖。 指令末尾的四个字节指定一个非零值，这是启用指令所必需的。

在 Windows Vista 中，使用 SetupPreferredAudioDevices 关键字的当前实现，将其 *dword 值* 设置为奇数的任何音频终结点都可以设置为默认设备。 若要确保将正确的终结点设置为默认设备，请确保最后公开包含相关终结点的 KS 筛选器。 由于 AudioEndpointBuilder 服务用来填充属性存储和设置默认设备的算法，必须执行此操作。

 

