---
title: 渲染插件简介
description: 渲染插件简介
ms.assetid: 7e6756ca-822a-4386-bcbd-363a10b1b2a3
keywords:
- 呈现插件 WDK 打印，有关呈现插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de9f3f3b8a1eaada94961329a2b9010eed22c646
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385398"
---
# <a name="introduction-to-rendering-plug-ins"></a>渲染插件简介





当将对新打印机设备的支持添加到任一[Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)(Unidrv) 或[Microsoft PostScript 的打印机驱动程序](microsoft-postscript-printer-driver.md)(Pscript)，可以实现 COM 接口方法若要修改的数据，该驱动程序将发送到打印后台处理程序。

通过提供用户模式 DLL 来完成此自定义。 此 DLL 被称为*呈现插件*。

它支持以下两种类型的自定义项：

-   提供自定义的版本的一些图形 DDI 的渲染函数。

-   实现特定于 Unidrv 的或特定于 Pscript 的 COM 接口方法修改该呈现的图像或扫描行数据流或数据流发送到后台处理程序之前在特定的注入点处插入 Postscript 代码。

**请注意**  呈现插件应永远不会生成一个窗口直接。 适用于 Windows Vista 及更高版本，您可以通过使用异步用户通知 XML 架构，提供异步事件通知消息的客户端计算机到 asyncui.xsd。 有关详细信息，请参阅[异步用户通知架构](https://docs.microsoft.com/windows-hardware/drivers/print/asynchronous-user-notification-schema)...

 

 

 




