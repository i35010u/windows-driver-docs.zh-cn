---
title: 支持兼容 TWAIN 的应用程序
description: 支持兼容 TWAIN 的应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17bfed88a7c285fe6a5cbb2ff0b9b70cdd5d73bc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838031"
---
# <a name="support-for-twain-compatible-applications"></a>支持兼容 TWAIN 的应用程序





为了支持具有私有功能的 TWAIN 应用程序，WIA 驱动程序可以使用称为 *传递* 功能的技术。 直通机制是指与 TWAIN 兼容的应用程序与 WIA 驱动程序通信的方式，使用数据源管理器和 TWAIN 兼容层作为中介。 必须注意的是，只有 Windows XP 和更高版本的操作系统版本支持 TWAIN 功能直通。

与 TWAIN 兼容的应用程序和 WIA 驱动程序之间的所有通信都首先进入数据源管理器 (*TWAIN \_32.dll*) ，后者又会调用 twain 兼容层 (*wiadss.dll*) 。 然后，TWAIN 兼容层调用 **IWiaItemExtras：： escape** 方法，该方法调用 **IStiUSD：： escape** 方法。 TWAIN 兼容层只调用 **IWiaItemExtras：： Escape** 方法。 驱动程序开发人员只应关注接收 **IStiUSD：： Escape** 调用的设备。 有关 **IWiaItemExtras：： Escape** 的详细信息，请参阅 Microsoft Windows SDK 文档。

**注意**   TWAIN 传递功能的目的是为了向从 TWAIN 驱动程序转换为 WIA 驱动程序的驱动程序编写器提供支持。 它不是为了向 WIA 驱动程序添加 TWAIN 功能而设计的。 如果 WIA 驱动程序不需要支持 TWAIN，则不应将此功能添加到您的驱动程序中。

 

以下是本节中要讨论的主题：

[在 WIA 驱动程序中启用 TWAIN 功能传递](enabling-twain-capability-pass-through-in-a-wia-driver.md)

[使用 IStiUSD 转义方法](using-the-istiusd-escape-method.md)

 

 




