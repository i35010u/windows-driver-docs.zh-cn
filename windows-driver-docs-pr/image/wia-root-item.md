---
title: WIA 根项
description: WIA 根项
ms.assetid: cf4d1056-3437-4ba7-8a87-421e91afd02a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 414ba5d4bf0d4c72d16eeadfd6ebc708a186f605
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352655"
---
# <a name="wia-root-item"></a>WIA 根项





WIA 根项是表示设备本身的文件夹项。 WIA 根项标记有**WiaItemTypeRoot**并**WiaItemTypeDevice**和包含设备属性，例如：

-   制造商名称

-   设备名称

-   驱动程序属性 （包括驱动程序版本和 CLSID 的用户界面）

图像处理应用程序通过调用获取 WIA 项树中的根项**IWiaDevMgr::CreateDevice**方法 （Microsoft Windows SDK 文档中所述）。 然后，应用程序使用的根项目要枚举的树中，从而获得单独的子项目的访问权限。

 

 




