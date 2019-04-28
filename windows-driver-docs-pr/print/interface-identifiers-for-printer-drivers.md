---
title: 打印机驱动程序的接口标识符
description: 打印机驱动程序的接口标识符
ms.assetid: 8182cba5-4461-4ca0-8b01-342519609b1f
keywords:
- COM 接口 WDK 打印，接口标识符
- 接口标识符 WDK 打印
- 插件 WDK 打印，接口标识符
- 标识符 WDK 打印机
- Guid WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51226fb598705b363f86d120c5a8ba807e98e4b6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345290"
---
# <a name="interface-identifiers-for-printer-drivers"></a>打印机驱动程序的接口标识符





Prcomoem.h 中定义一组的 Guid。 每个这些 Guid 是一个用于打印机驱动程序 （Unidrv 和 Pscript5） 和插件之间进行通信的 COM 接口的接口标识符。

对于 Windows 2000 和 Windows XP 中，定义以下 Guid:

**IID\_IPrintOemUI**
**IID\_IPrintOemUI2** （Pscript5 UI 插件在 Windows XP 和更高版本的 Windows 操作系统上） **IID\_IPrintOemDriverUI**
**IID\_IPrintCoreUI2** （Pscript5 UI 插件在 Windows XP 和更高版本的 Windows 操作系统上） **IID\_IPrintOemUni**
**IID\_IPrintOemUni2** （Unidrv 呈现插件在 Windows XP 和更高版本的 Windows 操作系统上） **IID\_IPrintOemUni3** （Unidrv 呈现插件在 Windows Vista 和更高版本的 Windows 操作系统上） **IID\_IPrintOemDriverUni**
**IID\_IPrintOemPS**
**IID\_IPrintOemPS2** （Pscript5 呈现插件在 Windows XP 和更高版本的 Windows 操作系统上） **IID\_IPrintOemDriverPS**
**IID\_IPrintCorePS2** （Pscript5 呈现插件在 Windows XP 和更高版本的 Windows 操作系统上） 的每个 GUID标识一个接口的一个版本。 如果定义一个接口的新版本，则新的 GUID 添加到列表。

用户界面插件和呈现插件必须确定它们支持的接口版本。 打印机驱动程序 （Unidrv 或 Pscript5） 调用的即插即用接**iunknown:: Queryinterface**方法 （Windows SDK 文档中所述），指定接口标识符作为输入。 如果插件支持指定的版本，该方法必须返回一个指向返回状态为 S 接口\_确定。 否则，它必须返回 E\_NOINTERFACE。 该驱动程序启动的最新版本的接口标识符，继续调用**QueryInterface**与早期的版本标识符，直到该方法返回 S\_确定或驱动程序用完的列表版本标识符。

同样，提供 Unidrv 和 Pscript5 **iunknown:: Queryinterface**方法[IPrintOemDriverUI](iprintoemdriverui-com-interface.md)， [IPrintCoreUI2](iprintcoreui2-com-interface.md)， [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)， [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)，或[IPrintCorePS2](iprintcoreps2-com-interface.md) COM 接口。 插件应调用相应的接口**QueryInterface**方法以确定驱动程序的受支持接口版本，并接收的接口指针。

 

 




