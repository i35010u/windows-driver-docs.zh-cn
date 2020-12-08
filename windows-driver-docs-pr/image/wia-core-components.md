---
title: WIA 核心组件
description: WIA 核心组件
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8367ff875385fc8d5c03969513479a81f8acc475
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788705"
---
# <a name="wia-core-components"></a>WIA 核心组件

下图显示了 WIA 组件。

![说明 wia 核心组件的关系图](images/stiwhist.png)

WIA 服务 (*wiaservc.dll*) 由名为 *svchost.exe* 的泛型主机托管。 *Wiaservc.dll* 与图) 中标记为 USD1、USD2 和 USD3 (的一个或多个用户模式静止图像驱动程序通信，每个驱动程序都与特定类型的内核模式驱动程序通信。 Windows 提供三种类型的总线抽象： USB、SCSI 和串行 ( *usbscan.sys*、 *scsiscan.sys* 和 *serscan.sys*) 。

在客户端，应用程序可以是与 TWAIN 兼容的应用程序 (请参阅 [对 TWAIN-Compatible 应用程序](support-for-twain-compatible-applications.md)) 或 WIA 应用程序的支持。 TWAIN 应用程序将调入数据源管理器，该管理器又调用 *wiadss.dll*，这种转换组件与 *sti.dll* 的实例进行通信。 *Sti.dll* 是与 WIA 服务通信的存根。 与此相反，WIA 应用程序会直接调用 *sti.dll*。
