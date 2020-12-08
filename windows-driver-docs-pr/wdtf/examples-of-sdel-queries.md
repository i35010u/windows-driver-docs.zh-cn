---
title: SDEL 查询示例
description: SDEL 查询中使用的设备关系标记的示例
keywords:
- SDEL
- SDEL 查询
ms.date: 09/03/2020
ms.localizationpriority: medium
ms.openlocfilehash: f92c0d4f9d53e48b93b0fcf3e549ad09ea535748
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785383"
---
# <a name="examples-of-sdel-queries"></a>SDEL 查询示例

有关 SDEL 查询中使用的设备关系令牌的详细信息，请参阅 [SDEL 中的设备关系令牌](device-relation-tokens-in-sdel.md)。

## <a name="examples-of-simple-device-relation-tokens-in-sdel-queries"></a>SDEL 查询中简单设备关系标记的示例

以下 SDEL 查询返回连接到计算机并安装的设备的集合。 此 SDEL 查询将返回所有已连接设备的类，无论设备是否已启用 (启动) 。

```command
var Devices = WDTF.DeviceDepot.Query("IsAttached");
```

SDEL 设备关系令牌还可以筛选查询结果。 例如，以下 SDEL 查询将返回计算机中已启动并具有作为 USB 类设备的父设备的设备集合。

```command
var Devices = WDTF.DeviceDepot.Query("IsStarted AND ancestor/(Class='USB')");
```

以下 SDEL 查询返回连接并安装在计算机中的设备的集合，无论它们是否已启动，以及是否具有存储卷、多媒体或网络适配器的类特性。

```command
var Devices = WDTF.DeviceDepot.Query("IsPhantom=False AND (Volume::DriveLetter OR class='Media' OR class='Net')");
```

## <a name="examples-of-combined-device-relation-tokens-in-sdel-queries"></a>SDEL 查询中组合设备关系标记的示例

如果使用 SDEL 设备关系令牌并在令牌中追加 "-或-self"，则生成的查询将返回包含设备的包含集合。
例如，以下 SDEL 查询返回计算机上界定闭合的设备的集合，或者包含软盘控制器、硬盘控制器或1394主机总线控制器。

```command
var Devices = WDTF.DeviceDepot.Query("above-or-self/(Class='HDC' OR Class='1394' OR  Class='FDC')");
```

作为另一个示例，此 SDEL 查询返回具有以下属性的设备的集合：

- 设备已连接并安装在计算机中。
- 设备是以下设备之一：
- 设备是一种显示类型设备，可以禁用该设备，并且具有某种与父设备的子关系。
- 设备是最顶层的 HID 类类型，与父设备的总线关系 (，根集线器) 除外。

```command
var Devices = WDTF.DeviceDepot.Query("IsAttached AND ((IsDisableable AND descendant-or-self/(Class='Display')) OR child/(Class='HIDClass') )" );
```
