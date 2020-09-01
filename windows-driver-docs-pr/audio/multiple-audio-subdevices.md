---
title: 多个音频子设备
description: 多个音频子设备
ms.assetid: 1654a2b3-7bec-4438-8cb5-b3136c8e66cc
keywords:
- 多功能音频设备 WDK，subdevices
- 多 subdevices WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 635e35f55afa95679de0ce13566c02311a9ada7d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210561"
---
# <a name="multiple-audio-subdevices"></a>多个音频子设备


## <span id="multiple_audio_subdevices"></span><span id="MULTIPLE_AUDIO_SUBDEVICES"></span>


多功能设备可以包含两个或更多音频 subdevices。 例如，适配器驱动程序可能会允许8通道音频设备以四个立体声通道的形式公开给系统。 编写适配器驱动程序以这种方式公开多个 subdevices 时，应将有关 subdevices 的信息合并到驱动程序的 [启动序列](startup-sequence.md) 和 INF 文件中。

首先，适配器驱动程序应在启动序列过程中，将每个立体声 subdevice 公开为端口/微型端口驱动程序对的单独实例。 Microsoft Windows 驱动程序工具包中的几个示例适配器 (WDK) 实现一个 `InstallSubdevice` 函数，该函数创建并注册由系统端口驱动程序、微型端口驱动程序和一组要绑定到此对的一组资源组成的 subdevice。 在启动过程中，驱动程序应 `InstallSubdevice` 为每个立体声 subdevice 调用一次其函数，并为每个端口/微型端口驱动程序对指定唯一的名称。

此外，分配给此对的唯一名称必须与在驱动程序的 INF 文件中指定的 KSNAME 字符串匹配。 例如，在启动过程中，驱动程序可能将名称 "Wave1" 和 "Wave2" 分配给两个 subdevices，如下所示：

```inf
  InstallSubdevice(..., "Wave1",...);
  InstallSubdevice(..., "Wave2",...);
```

在这种情况下，INF 文件中应显示相同的名称：

```inf
  KSNAME_Wave1="Wave1"
  KSNAME_Wave2="Wave2"
```

INF 文件应添加包含以下名称的接口：

```inf
  AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave1%,Test.Interface.Wave1
  AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave2%,Test.Interface.Wave2
```

INF 文件应创建 **AddReg** 节 (参阅 [**INF AddReg 指令**](../install/inf-addreg-directive.md)) 以便将有关这些接口的信息添加到注册表中：

```inf
  [Test.Interface.Wave1]
  AddReg=Test.I.Wave1.AddReg

  [Test.Interface.Wave2]
  AddReg=Test.I.Wave2.AddReg
```

**AddReg**节还应为每个 subdevice 指定注册表项：

```inf
  [Test.I.Wave1.AddReg]
  HKR,,CLSID,,%Proxy.CLSID%
  HKR,,FriendlyName,,%Test.Wave1.szName%

  [Test.I.Wave2.AddReg]
  HKR,,CLSID,,%Proxy.CLSID%
  HKR,,FriendlyName,,%Test.Wave2.szName%
```

最后，INF 文件应定义这些 subdevices 的友好名称：

```inf
  Test.Wave1.szName="Punch"
  Test.Wave2.szName="Judy"
```

友好名称显示在 "音频控制面板" 中以识别 subdevices。

 

