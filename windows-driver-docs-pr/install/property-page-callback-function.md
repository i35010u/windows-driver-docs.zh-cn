---
title: 属性页回调函数
description: 属性页回调函数
keywords:
- 设备属性页 WDK 设备安装，回调函数
- 属性页 WDK 设备安装，回调函数
- 自定义属性页 WDK 设备安装，回调函数
- 回调函数 WDK 属性页
- PSPCB_CREATE
- PSPCB_RELEASE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5dc1d6b8dc8ead82b13f83cf900d503b031cef82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796027"
---
# <a name="property-page-callback-function"></a>属性页回调函数





当提供程序为其设备或设备类创建属性页时，它将提供一个指向回调函数的指针。 回调函数将在创建属性页时调用一次，并在即将销毁时再次调用。

回调是 Windows SDK 文档中描述的 **PropSheetPageProc** 函数。 此函数必须能够处理 PSPCB_CREATE 和 PSPCB_RELEASE 操作。

创建属性页时，将使用 PSPCB_CREATE 消息调用回调。 为响应此消息，回调可以为与页关联的数据分配内存。 函数应返回 **TRUE** 以继续创建页面，如果不应创建页面，则返回 **FALSE** 。

当用户在页面的对话框上单击 **"确定"** 或 "**取消**" 或在 "**驱动程序**" 选项卡上单击 "**卸载**" 时，设备的属性页将被销毁。

销毁属性页时，将使用 PSPCB_RELEASE 消息调用回调。 函数应释放在创建属性页时分配的任何数据。 通常，这涉及释放 PROPSHEETPAGE 结构的 **lParam** 成员所引用的数据。 销毁页面时，将忽略返回值。

 

 





