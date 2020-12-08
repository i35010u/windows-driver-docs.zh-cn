---
title: 打印机驱动程序的接口标识符
description: 打印机驱动程序的接口标识符
keywords:
- COM 接口 WDK 打印，接口标识符
- 接口标识符 WDK 打印
- 插件 WDK 打印，接口标识符
- 标识符 WDK 打印机
- Guid WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11faa04e6933b40f1d09b88d3fb6005af4187a37
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835647"
---
# <a name="interface-identifiers-for-printer-drivers"></a>打印机驱动程序的接口标识符





一组 Guid 是在 prcomoem 中定义的。 其中每个 Guid 都是用于打印机驱动程序之间通信的 COM 接口的接口标识符 (Unidrv 和 Pscript5) 和插件。

对于 Windows 2000 和 Windows XP，定义以下 Guid：

**IID \_IPrintOemUI** 
 **IID \_ IPrintOemUI2** (windows xp 和更高版本上的 windows 操作系统上的 Pscript5 UI 插件) **iid \_ IPrintOemDriverUI** 
 **iid \_ IPrintCoreUI2** (windows xp 上的 windows xp 和更高版本的 windows 操作系统上的 Pscript5 ui 插件) **iid \_ IPrintOemUni** 
 **iid \_ IPrintOemUni2** (Unidrv 在 windows xp 和更高版本的 windows 操作系统上呈现插件) **iid \_ IPrintOemUni3** (Unidrv render 插件-在 windows Vista 和更高版本的 windows 操作系统上，) **iid \_ IPrintOemDriverUni** 
 **iid \_ IPrintOemPS** 
 **iid \_ IPrintOemPS2** (Pscript5 在 windows xp 和更高版本的 windows 操作系统上呈现插件) **iid \_ IPrintOemDriverPS** 
 **iid \_ IPrintCorePS2** (Pscript5 在 windows xp 和更高版本的 windows 操作系统上呈现插件) 每个 GUID 标识一个接口的一个版本。 如果定义了新版本的接口，则会向列表中添加一个新的 GUID。

用户界面插件和呈现插件必须标识它们支持的接口版本。 打印机驱动程序 (Unidrv 或 Pscript5) 调用 Windows SDK 文档) 中 (所述的插件的 **IUnknown：： QueryInterface** 方法，并将接口标识符指定为输入。 如果插件支持指定的版本，则该方法必须返回指向接口的指针以及返回状态 \_ "正常"。 否则，它必须返回 E \_ NOINTERFACE。 该驱动程序从最新版本的接口标识符开始，并继续使用早期版本的标识符调用 **QueryInterface** ，直到该方法返回 S \_ OK 或驱动程序用完版本标识符列表。

同样，Unidrv 和 Pscript5 提供 [IPrintOemDriverUI](iprintoemdriverui-com-interface.md)、 [IPrintCoreUI2](iprintcoreui2-com-interface.md)、 [IPrintOemDriverUni](iprintoemdriveruni-com-interface.md)、 [IPrintOemDriverPS](iprintoemdriverps-com-interface.md)或 [IPrintCorePS2](iprintcoreps2-com-interface.md) COM 接口的 **IUnknown：： QueryInterface** 方法。 插件应该调用相应接口的 **QueryInterface** 方法来确定驱动程序的受支持接口版本并接收接口指针。

 

 




