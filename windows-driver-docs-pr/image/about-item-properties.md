---
title: 关于项属性
description: 关于项属性
ms.assetid: f8d00e29-ce7d-4949-a713-07755f495d6a
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1aba6c7215424c4c73a8921a0cc5fd71dce3ac4c
ms.sourcegitcommit: 40d7d538756767d26bbda636589f614f85a6fab3
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86020080"
---
# <a name="about-item-properties"></a>关于项属性

每个应用程序项树都包含项属性的集合。 此属性集合也称为属性流。 应用程序项模型为每个应用程序提供其自己的项树副本，使应用程序可以单独修改属性。

驱动程序指定它们支持的属性，并定义这些属性的初始值。 当应用程序读取某个属性时，驱动程序将更新必须使用其当前值刷新的所有属性。 例如，如果应用程序读取设备时间，则驱动程序可以询问设备当前时间，并更新 "设备时间" 属性。 当应用程序将新值写入属性时，WIA 服务会要求驱动程序验证此值并将其写入到属性。

某些属性对某些设备类型是必需的。 例如，具有自动文档送纸器（ADF）的设备必须支持 ADF 属性。

> [!NOTE]
> 如果你比 WIA 更熟悉 TWAIN，则了解 WIA 属性与 TWAIN 功能同义可能会很有帮助。
