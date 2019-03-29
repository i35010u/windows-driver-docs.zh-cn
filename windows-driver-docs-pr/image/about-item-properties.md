---
title: 关于项属性
description: 关于项属性
ms.assetid: f8d00e29-ce7d-4949-a713-07755f495d6a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52e4f310e019d3d622e72179eb6f0fec985f1a22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564349"
---
# <a name="about-item-properties"></a>关于项属性





每个应用程序项树包含的项属性的集合。 （此属性集合是也称为属性流。）应用程序项目模型提供其自己的副本项树中，并允许修改属性相互独立的应用程序的每个应用程序。

驱动程序指定的属性，它们支持并定义这些属性的初始值。 当应用程序读取属性时，该驱动程序及其当前值更新必须刷新的任何属性。 例如，如果应用程序读取设备时间，然后驱动程序可以请求设备，为它的当前时间和更新设备时属性。 当应用程序将新值写入该属性时，WIA 服务要求驱动程序验证并将此值写入到该属性。

某些属性是强制性的一些设备类型。 例如，具有自动文档送纸器 (ADF) 的设备必须支持 ADF 属性。

**请注意**  你是否更熟悉 TWAIN 比起 WIA，它可能有助于了解 WIA 属性是与 TWAIN 功能。

 

 

 




