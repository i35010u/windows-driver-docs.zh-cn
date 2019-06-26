---
title: 用户模式下函数
description: 用户模式下函数
ms.assetid: 1faa04b1-0bf0-494c-b55f-5c90c259c8f5
keywords:
- 强制反馈驱动程序 WDK HID，用户模式下函数
- 用户模式下函数 WDK 强制反馈
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 99c9fdae95b6ca32d716b2af17a32827bb8241b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385795"
---
# <a name="user-mode-functions"></a>用户模式下函数





DirectInput 力反馈效果驱动程序的实例创建通过创建由 CLSID，存储在名为的对象**OEMForceFeedback**游戏杆类型子项的注册表子项。

因为使用 DirectInput 的应用程序需要加载 OLE，效果驱动程序应小心，不要依赖于特定于 OLE 的行为。 例如，使用 DirectInput 的应用程序不能依赖以调用**CoFreeUnusedLibraries**方法。 DirectInput 执行标准的 COM 操作，以创建效果驱动程序对象的实例。 以下介绍了仅在可见的效果这应该没有效果驱动程序的实现。

DirectInput 释放最后一个效果驱动程序对象后，它将手动执行效果驱动程序 DLL 的 FreeLibrary。 因此，如果效果驱动程序 DLL 创建不影响驱动程序对象与关联的其他资源，它应手动 LoadLibrary 本身以人为地提高其 DLL 引用计数，从而防止从 FreeLibraryDirectInput 过早卸载 DLL。

具体而言，如果效果驱动程序 DLL 创建一个工作线程，效果驱动程序必须执行此人工 LoadLibrary 的操作，只要工作线程存在一样。 当不再需要工作线程 （例如，在从作为它的最后一个效果驱动程序对象的通知时已被破坏），工作线程应调用 FreeLibraryAndExitThread 方法以递减 DLL 引用计数并终止该线程。

所有量值并获得由 DirectInput 的有效值统一和线性范围内。 物理设备中的任何非线性必须由设备驱动程序处理，以便应用程序将线性设备。

用户模式下强制通过公开的反馈函数[IDirectInputEffectDriver](https://docs.microsoft.com/windows/desktop/api/dinputd/nn-dinputd-idirectinputeffectdriver)强制反馈效果驱动程序 DLL 必须实现接口。 有关这些函数的详细信息，请参阅 IDirectInputEffectDriver。

 

 




