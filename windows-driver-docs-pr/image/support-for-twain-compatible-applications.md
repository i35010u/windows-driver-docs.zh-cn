---
title: TWAIN 兼容应用程序的支持
description: TWAIN 兼容应用程序的支持
ms.assetid: 8135178f-a432-4200-81c3-8e12112637f4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f85504c59a7a4fec15c56901e971785ce8c582fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526197"
---
# <a name="support-for-twain-compatible-applications"></a>TWAIN 兼容应用程序的支持





为了支持 TWAIN 与专用功能的应用程序，WIA 驱动程序可以使用一种技术称为*直通*功能。 传递的机制是指与 WIA 驱动程序，使用数据源管理器和 TWAIN 兼容性层作为中介 TWAIN 兼容的应用程序进行通信的方式。 请务必注意，仅在 Windows XP 和更高版本的操作系统版本中支持 TWAIN 功能传递。

TWAIN 兼容的应用程序和 WIA 驱动程序之间的所有通信将首先都转到数据源管理器 (*twain\_32.dll*)，这反过来调用 TWAIN 兼容性层 (*wiadss.dll*). TWAIN 兼容性层然后调用**IWiaItemExtras::Escape**方法，调用**IStiUSD::Escape**方法。 TWAIN 兼容性层只能调用**IWiaItemExtras::Escape**方法。 驱动程序开发人员应只关心设备接收**IStiUSD::Escape**调用。 有关详细信息**IWiaItemExtras::Escape**，请参阅 Microsoft Windows SDK 文档。

**请注意**   TWAIN 直通功能的目的是向驱动程序编写人员在进行从 TWAIN 驱动程序转换为 WIA 驱动程序提供支持。 它不是为了将 TWAIN 功能添加到 WIA 驱动程序。 如果您 WIA 的驱动程序不需要为 TWAIN 的支持，您不应此功能添加到您的驱动程序。

 

本部分讨论了以下主题：

[启用了 TWAIN 功能传递到 WIA 的驱动程序](enabling-twain-capability-pass-through-in-a-wia-driver.md)

[使用 IStiUSD 转义方法](using-the-istiusd-escape-method.md)

 

 




