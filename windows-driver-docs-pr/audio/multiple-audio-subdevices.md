---
title: 多个音频子设备
description: 多个音频子设备
ms.assetid: 1654a2b3-7bec-4438-8cb5-b3136c8e66cc
keywords:
- 多功能音频设备 WDK，子设备
- 多子设备 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a22d039208e639ea72cadfccb9f88b94c3c91459
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363208"
---
# <a name="multiple-audio-subdevices"></a>多个音频子设备


## <span id="multiple_audio_subdevices"></span><span id="MULTIPLE_AUDIO_SUBDEVICES"></span>


多功能设备可以包含两个或多个音频子设备。 例如，适配器驱动程序可能会使八个通道音频设备要向系统公开为四个立体声通道。 在编写的适配器驱动程序来公开这种方式中的多个子设备时，应将子设备有关的信息合并到您的驱动程序[启动序列](startup-sequence.md)和 INF 文件。

首先，您的适配器驱动程序应在启动序列期间公开作为单独的实例的端口/微型端口驱动程序对每个立体声子。 Microsoft Windows Driver Kit (WDK) 实现中的示例适配器的几个`InstallSubdevice`函数用于创建和注册的系统端口驱动程序、 微型端口驱动程序，以及一组要绑定到此对的资源组成子。 在启动期间，您的驱动程序应调用其`InstallSubdevice`函数一次为每个立体声子，并指定每个端口/微型端口驱动程序对的唯一名称。

此外，你将分配给此对的唯一名称必须与您的驱动程序 INF 文件中指定 KSNAME 字符串匹配。 例如，您的驱动程序可能将分配名称"Wave1"和"Wave2"到两个子设备在启动期间，如下所示：

```inf
  InstallSubdevice(..., "Wave1",...);
  InstallSubdevice(..., "Wave2",...);
```

在这种情况下，相同的名称应出现在 INF 文件：

```inf
  KSNAME_Wave1="Wave1"
  KSNAME_Wave2="Wave2"
```

INF 文件应添加包含这些名称的接口：

```inf
  AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave1%,Test.Interface.Wave1
  AddInterface=%KSCATEGORY_AUDIO%,%KSNAME_Wave2%,Test.Interface.Wave2
```

INF 文件应创建**AddReg**部分 (请参阅[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)) 以便将有关这些接口的信息添加到注册表：

```inf
  [Test.Interface.Wave1]
  AddReg=Test.I.Wave1.AddReg

  [Test.Interface.Wave2]
  AddReg=Test.I.Wave2.AddReg
```

**AddReg**部分还应指定的每个子的注册表项：

```inf
  [Test.I.Wave1.AddReg]
  HKR,,CLSID,,%Proxy.CLSID%
  HKR,,FriendlyName,,%Test.Wave1.szName%

  [Test.I.Wave2.AddReg]
  HKR,,CLSID,,%Proxy.CLSID%
  HKR,,FriendlyName,,%Test.Wave2.szName%
```

最后，INF 文件应定义这些子设备的友好名称：

```inf
  Test.Wave1.szName="Punch"
  Test.Wave2.szName="Judy"
```

友好名称显示音频控件面板中标识子设备。

 

 




