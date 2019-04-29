---
title: 创建 WIA 微驱动程序
description: 创建 WIA 微驱动程序
ms.assetid: 4f453569-d768-47fb-9b70-ebb51e303cf0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f77d905d77de2217b7fde09f510771391e70a92
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386325"
---
# <a name="creating-a-wia-microdriver"></a>创建 WIA 微驱动程序





在类似的方式进行控制许多平板扫描仪。 模型之间的常见行为已被提取到的由 Microsoft 提供通用驱动程序称为 WIA 平板驱动程序。 此驱动程序调用 DLL，名为 microdriver，扫描程序供应商提供，用于实现任何所需的特定于设备的行为。 以及 microdriver WIA 平板驱动程序然后可以用作 WIA 微型驱动程序。 使用 microdriver 的优点是很容易实现和调试。 并非所有扫描仪可以都受 microdriver。 它是最适合于简单的设备 （不带双面打印器或其他高级功能），或当需要基本功能驱动程序时。

**请注意**  WIA microdrivers 在本部分中所述将 WIA 1.0。 目前 WIA 2.0 没有相应 WIA microdriver 模型。 如果开发 WIA microdriver，若要支持 WIA 2.0 的 Windows 版本的计算机上运行 (Windows Vista 或更高版本)，此 WIA microdriver 将工作等任何其他 WIA 1.0 设备，并且将由在 WIA 1.0 兼容性模式下的 WIA 2.0 应用程序。

 

下图显示在 WIA microdriver 体系结构的组件。

![说明 wia microdriver 体系结构中的组件的关系图](images/art-6.png)

WIA 平板驱动程序通过调用中 microdriver 的 WIA microdriver 函数来处理来自 WIA 服务请求。 Microdriver 必须实现每个函数。 一个[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)结构传递给 microdriver 来存储和通信扫描参数，例如扫描窗口和解决方法。 WIA 平板驱动程序从 SCANINFO 结构中，读取值，但永远不会将其写入。 它负责 microdriver 设置 SCANINFO 成员。

Microdriver 不应存储一次扫描，任何参数，但应依赖于存储中的值[ **SCANINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff547361)结构。 这一点对于支持多个应用程序访问设备。 如果在同一时间将两个应用程序设置了在同一设备上扫描，则只有一份运行 microdriver。 在此情况下使用任一具体取决于应用程序正在尝试访问设备的两个不同 SCANINFO 结构调用 microdriver。

 

 




