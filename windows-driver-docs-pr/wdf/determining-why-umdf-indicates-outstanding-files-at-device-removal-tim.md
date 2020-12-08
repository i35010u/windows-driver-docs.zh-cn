---
title: UMDF 指示在设备删除时未完成的文件
description: 介绍如何使用 Wudfext.dll 来确定在删除设备时，该文件的原因会表明存在未完成的文件。
keywords:
- 调试方案 WDK UMDF，UMDF 指示在设备删除时未完成的文件
- UMDF WDK，调试方案，UMDF 指示在设备删除时未完成的文件
- UMDF WDK，UMDF 指示在设备删除时未完成的文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3908a6fb5b75e187c9fe670c7c496c8581eac58a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828945"
---
# <a name="determining-why-umdf-indicates-outstanding-files-at-device-removal-time"></a>确定 UMDF 在删除设备时指示文件未完成的原因


本主题介绍了如何将 Wudfext.dll 调试程序扩展与 User-Mode Driver Framework (UMDF) 版本1或2驱动程序一起使用，以确定在删除设备时，UMDF 指示存在未完成文件的原因。

对于 UMDF 版本1，你将使用在 wudfext.dll 中实现的扩展命令。 从 UMDF 版本2开始，你将使用在 wdfkd.dll 中实现的扩展命令。

若要确定 UMDF 为何指示未完成的文件，请执行以下步骤：

1.  使用 [**！ wudfext. umdevstack**](../debugger/-wudfext-umdevstack.md) (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfumdevstack.md) (umdf 2) 来转储设备堆栈。 转储包含未处理的 UMDF 堆栈内文件 (即，堆栈中的驱动程序创建的文件对象与应用程序或另一堆栈中的驱动程序所创建的文件对象相反) 。

2.  对于每个堆栈内文件，请运行 [**umfile**](../debugger/-wudfext-umfile.md) (umdf 1) 或！)  ([**wdfkd**](../debugger/-wdfkd-wdfumfile.md) ，以获取有关该文件的信息。

    输出包括挂起的 Irp 的列表。

3.  使用 [**！ wudfext. umirp**](../debugger/-wudfext-umirp.md) (umdf 1) 或 [**！ WDFKD wdfumirp**](../debugger/-wdfkd-wdfumirp.md) (umdf 2) 来确定每个 irp 的未完成原因，以获取有关 IRP 的信息。

    从每个 [**！ wudfext**](../debugger/-wudfext-umirp.md) 或 [**wdfumirp**](../debugger/-wdfkd-wdfumirp.md)的输出：

    -   确定 IRP 是否已完成。
    -   确定驱动程序创建的请求是由驱动程序显式删除还是由对象树隐式删除。

 

