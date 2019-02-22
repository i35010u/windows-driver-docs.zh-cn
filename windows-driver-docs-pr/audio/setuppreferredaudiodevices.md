---
title: SetupPreferredAudioDevices
description: SetupPreferredAudioDevices
ms.assetid: cc6b7da4-335d-4629-ba54-32aa32a1eb09
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1811c10c9ac649c7e58d5f7c7cd6b89946664d39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525409"
---
# <a name="setuppreferredaudiodevices"></a>SetupPreferredAudioDevices


## <span id="ddk_setuppreferredaudiodevices_ks"></span><span id="DDK_SETUPPREFERREDAUDIODEVICES_KS"></span>


SetupPreferredAudioDevices 关键字表示首选音频设备，这是当系统包含一个音频系统默认情况下启用的设备或更多的音频设备。 此关键字是媒体类特定且受 Microsoft Windows Millennium Edition/Windows 98、 Microsoft Windows 2000、 Windows XP 和 Windows Vista。 不支持在 Windows 7 中的 SetupPreferredAudioDevicesis。

当创建音频设备，而不是显式指定设备的应用程序可以选择要使用默认值 （或首选） 设备。 (有关示例，请参阅的说明[ **waveOutOpen** ](https://msdn.microsoft.com/library/windows/desktop/dd743866)并**DirectSoundCreate** Microsoft Windows SDK 文档中的函数。)

跟踪系统注册表中的当前首选音频设备的音频系统。 在用户通过安装新的音频设备升级一个系统，通常安装在设备的专有 INF 文件更新注册表，以将新设备指定为首选音频设备。

SetupPreferredAudioDevices 关键字可以出现在中的注册表更新指令**添加注册表部分**(请参阅[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)) 的 INF 文件音频设备。 此指令的格式如下：

*reg rootkey*， \[*注册表子项*\]SetupPreferredAudioDevices \[*标志*\]， \[ *dword 值*\]

指令指示音频系统声音播放、 声音录制和播放 MIDI 音乐作为默认值使用设备的音频功能。 安装完成后，这些三个默认值显示在声音和多媒体控制面板下**音频**选项卡。用户可以使用控制面板更改默认设备。

该指令*dword 值*参数指定应为非零值以启用该指令的 DWORD 值。 如果此值为零，则指令无效。 因为 Windows Me / 98 不支持将 REG\_DWORD 注册表数据类型，但是， *dword 值*通常都表示为 4 字节 REG\_作为一个 dword 值 （例如，作为"01,00,00,00"而不是二进制类型而不是"0x00000001")。 *Dword 值*参数可以通过设置的指令指定以原始二进制格式*标志*为"1"的参数 (FLG\_ADDREG\_BINVALUETYPE)。

该指令将在安装设备的驱动程序的时间生效。 如果另一台设备在安装新设备时占用的首选设备角色，该指令会导致新的设备采用首选设备，因此显示此角色的其他设备的角色。

当升级或重新安装已安装的设备驱动程序时，你可能想要避免更改用户的当前首选设备所做选择声音播放、 声音录制和播放 MIDI 音乐。 如果是这样，设置 FLG\_ADDREG\_NOCLOBBER 位*标志*参数，这会导致指令以仅当这是设备的初始安装时，才会生效。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

下面的示例是演示如何使用 SetupPreferredAudioDevices 关键字 INF 文件的一部分：

```inf
  AddReg = XYZ-Audio-Device.AddReg
  ...
  [XYZ-Audio-Device.AddReg]
  HKR,,SetupPreferredAudioDevices,3,01,00,00,00
```

该示例末尾处的指令指定名为"XYZ 音频设备"的设备现在是首选音频设备。 HKR 是注册表中的音频设备的根项。 *标志*参数设置为 3，这是按位或的 FLG\_ADDREG\_BINVALUETYPE 和 FLG\_ADDREG\_NOCLOBBER。 后者会阻止设备的现有首选设备注册表条目被覆盖，如果已安装设备，并且只是在升级其驱动程序。 指令的末尾处的四个字节指定非零值，必须启用指令。

在 Windows Vista 中，与任何音频终结点的 SetupPreferredAudioDevices 关键字的当前实现使用其*dword 值*设置为奇数数目可以设置为默认设备。 若要确保正确的终结点被设置为默认设备，请确保包含相关终结点的 KS 筛选器公开上一次。 必须执行此操作由于 AudioEndpointBuilder 服务用来填充属性存储和设置默认设备的算法。

 

 





