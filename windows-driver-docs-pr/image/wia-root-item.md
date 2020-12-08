---
title: WIA 根项
description: WIA 根项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 865625e17ab6d6c2eb9fd9f9c65ae6f746a1442d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826459"
---
# <a name="wia-root-item"></a>WIA 根项





WIA 根项是表示设备本身的文件夹项。 WIA 根项标记有 **WiaItemTypeRoot** 和 **WiaItemTypeDevice** ，并包含如下所示的设备属性：

-   制造商名称

-   设备名称

-   驱动程序属性 (包括驱动程序版本和用户界面 CLSID) 

图像处理应用程序通过调用 Microsoft Windows SDK 文档)  (中所述的 **IWiaDevMgr：： CreateDevice** 方法获取 WIA 项树中的根项。 然后，应用程序使用根项来枚举树，从而获得对单个子项的访问权限。

 

 




