---
title: 属性页回调函数
description: 属性页回调函数
ms.assetid: 3f4d7247-2a12-4889-9fc0-a28f58046c7b
keywords:
- 设备属性页 WDK 设备安装，回调函数
- 属性页 WDK 设备安装，回调函数
- 自定义属性页 WDK 设备安装，回调函数
- 回调函数 WDK 属性页
- PSPCB_CREATE
- PSPCB_RELEASE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 073d60910095ba829a0d348d28cb48bf80104164
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391984"
---
# <a name="property-page-callback-function"></a>属性页回调函数





当提供程序创建其设备或设备类的属性页时，它提供的回调函数的指针。 回调函数是被调用一次时创建的属性页并再次时即将销毁。

在回调**PropSheetPageProc** Windows SDK 文档中所述的函数。 此函数必须能够处理 PSPCB_CREATE 和 PSPCB_RELEASE 操作。

在创建属性页时，将使用 PSPCB_CREATE 消息调用回调。 响应此消息，该回调可以为与页关联的数据分配内存。 该函数应返回 **，则返回 TRUE**若要继续创建页或**FALSE**如果应创建页。

当用户单击销毁设备的属性页**确定**或**取消**上的页对话框的或单击**卸载**上**的驱动程序**选项卡。

当销毁属性页时，使用 PSPCB_RELEASE 消息调用回调。 该函数应释放已分配的属性页创建时的任何数据。 通常情况下，这涉及释放所引用的数据**lParam** PROPSHEETPAGE 结构中的成员。 当正在销毁页时，将忽略返回值。

 

 





