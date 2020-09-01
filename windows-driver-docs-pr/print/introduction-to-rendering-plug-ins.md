---
title: 渲染插件简介
description: 渲染插件简介
ms.assetid: 7e6756ca-822a-4386-bcbd-363a10b1b2a3
keywords:
- 呈现插件 WDK 打印，关于呈现插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b9d93739d941229527640b1e4393a670118d53c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205887"
---
# <a name="introduction-to-rendering-plug-ins"></a>渲染插件简介





当你向 [Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md) (Unidrv) 或 [microsoft PostScript 打印机驱动程序](microsoft-postscript-printer-driver.md) (Pscript) 中添加对新打印机设备的支持时，你可以实现 COM 接口方法来修改驱动程序发送到打印后台处理程序的数据。

可以通过提供用户模式 DLL 完成此自定义。 此 DLL 称为 *呈现插件*。

它支持以下两种类型的自定义：

-   提供某些图形 DDI 呈现功能的自定义版本。

-   实现特定于 Unidrv 或特定于 Pscript 的 COM 接口方法，这些方法在将数据流发送到后台处理程序之前修改呈现的图像或扫描行数据流，或在特定注入点处插入 Postscript 代码。

**注意**   呈现插件绝不会直接生成窗口。 对于 Windows Vista 和更高版本，可以通过使用异步用户通知 XML 架构 asyncui，向客户端计算机提供异步事件通知消息。 有关详细信息，请参阅 [异步用户通知架构](./asynchronous-user-notification-schema.md)。

 

 

