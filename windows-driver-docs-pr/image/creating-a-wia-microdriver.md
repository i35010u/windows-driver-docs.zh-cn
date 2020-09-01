---
title: 创建 WIA 微驱动程序
description: 创建 WIA 微驱动程序
ms.assetid: 4f453569-d768-47fb-9b70-ebb51e303cf0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca477307338a98a28a8dab8feb92b670f1d17dd5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191733"
---
# <a name="creating-a-wia-microdriver"></a>创建 WIA 微驱动程序





许多平板扫描仪的控制方式类似。 模型之间的常见行为已抽象到 Microsoft 提供的通用驱动程序（称为 WIA 平板驱动程序）。 此驱动程序调用由扫描程序供应商提供的名为 microdriver 的 DLL，该 DLL 实现任何所需的特定于设备的行为。 然后，可以将 WIA 平板驱动程序与 microdriver 一起用作 WIA 微型驱动程序。 使用 microdriver 的优点是非常易于实现和调试。 并非所有扫描仪都可以通过 microdriver 支持。 它最适用于无双面打印器或其他高级) 功能 (的简单设备，或者需要基本功能驱动程序时。

**注意**   本部分介绍的 WIA microdrivers 为 WIA 1.0。 当前没有 WIA 2.0 对应的 WIA microdriver 模型。 如果你开发的 WIA microdriver 在具有支持 WIA 2.0 (Windows Vista 或更) 高版本的 Windows 版本的计算机上运行，则此 WIA microdriver 将像任何其他 WIA 1.0 设备一样工作，并将在 WIA 1.0 兼容模式下由 WIA 2.0 应用程序使用。

 

下图显示了 WIA microdriver 结构中的组件。

![说明 wia microdriver 体系结构中的组件的关系图](images/art-6.png)

WIA 平板驱动程序通过调用 microdriver 中的 WIA microdriver 函数来处理来自 WIA 服务的请求。 Microdriver 必须实现其中每个函数。 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo)结构会传递到 microdriver，以存储和传达扫描参数，如扫描窗口和分辨率。 WIA 平板驱动程序读取 SCANINFO 结构中的值，但绝不会写入这些值。 Microdriver 负责设置 SCANINFO 成员。

Microdriver 不应存储任何扫描参数，但应依赖于存储在 [**SCANINFO**](/windows-hardware/drivers/ddi/wiamicro/ns-wiamicro-_scaninfo) 结构中的值。 这对于支持多个应用程序对设备的访问很重要。 如果两个应用程序同时在同一台设备上设置扫描，则仅有一个 microdriver 的副本在运行。 在这种情况下，将使用两个不同 SCANINFO 结构中的一个结构调用 microdriver，具体取决于尝试访问设备的应用程序。

 

