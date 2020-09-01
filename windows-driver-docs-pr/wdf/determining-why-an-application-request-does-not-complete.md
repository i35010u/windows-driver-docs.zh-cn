---
title: 确定应用程序请求无法完成的原因
description: 本主题介绍如何将 Wudfext.dll 调试程序扩展与用户模式驱动程序框架结合使用， (UMDF) 第1版或第2版驱动程序，以确定应用程序请求未完成的原因。
ms.assetid: 33a09277-1e00-4f91-b2ab-b2541091628f
keywords:
- UMDF WDK，应用程序请求未完成
- 调试方案 WDK UMDF，应用程序请求未完成
- UMDF WDK，调试方案，应用程序请求未完成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2089749875b60431bb949d2af03ae34f07a5f6e4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191027"
---
# <a name="determining-why-an-application-request-does-not-complete"></a>确定应用程序请求无法完成的原因


本主题介绍如何将 Wudfext.dll 调试程序扩展与用户模式驱动程序框架结合使用， (UMDF) 第1版或第2版驱动程序，以确定应用程序请求未完成的原因。

对于 UMDF 版本1，你将使用在 wudfext.dll 中实现的扩展命令。 从 UMDF 版本2开始，你将使用在 wdfkd.dll 中实现的扩展命令。

你可以执行以下步骤来确定应用程序请求无法完成的原因：

1.  使用 [**！ wudfext. umirps**](../debugger/-wudfext-umirps.md) (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfumirps.md) (UMDF 2) 以显示主机进程中 (irp) 的所有未完成的用户模式 i/o 请求包。 每个用户模式 IRP 的信息包括原始内核模式 IRP，已为其创建用户模式 IRP。

    确定对应于应用程序所源自的内核模式 IRP 的用户模式 IRP。

2.  使用 [**！ wudfext. umirp**](../debugger/-wudfext-umirp.md) (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfumirp.md) (UMDF 2) 获取有关特定用户模式 IRP 的信息。

    用户模式 IRP 的信息包括堆栈位置。 如果知道堆栈位置，可以确定正在处理 IRP 的位置。 堆栈位置0表示 UMDF (下的堆栈，即内核模式堆栈或其他一些子系统，如 Microsoft Win32 或 Winsock) 。

3.  如果 IRP 位于驱动程序的层上 (即驱动程序处理 IRP) 的层，请执行以下步骤：
    1.  查看在驱动程序层设置的 i/o 队列。 你可以使用 [**！ wudfdevicequeues**](../debugger/-wudfext-wudfdevicequeues.md) (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfdevicequeues.md) (UMDF 2) 来查看在你的驱动程序层设置的所有 i/o 队列。 你还可以使用 [**！ wudfext. wudfqueue**](../debugger/-wudfext-wudfqueue.md) (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfqueue.md) (umdf 2) 获取有关特定队列的信息。

    2.  如果有多个请求未完成，可使用 [**！ wudfext. wudfrequest**](../debugger/-wudfext-wudfrequest.md) (umdf 1) 或 [**！ WDFKD wdfrequest**](../debugger/-wdfkd-wdfrequest.md) (umdf 2) 获取有关请求的信息，其中包括基础用户模式 IRP。 通过用户模式 IRP 信息，你可以确定你感兴趣的请求。
    3.  验证请求是否由队列或驱动程序拥有。 此信息显示为 [**！ wudfext. wudfqueue**](../debugger/-wudfext-wudfqueue.md) 或 [**wdfqueue wdfkd**](../debugger/-wdfkd-wdfqueue.md)的输出的一部分。 根据队列或驱动程序是否拥有请求，执行下列验证之一：
        -   如果请求属于队列，请检查队列的状态以确定队列未将请求传递给驱动程序的原因。
        -   如果请求由驱动程序所有，则检查主机进程中的线程，以确定线程在处理请求时是否停滞或死锁。

4.  如果 IRP 位于另一个 UMDF 驱动程序层，则可以对该层重复前面的步骤。 请记住，可以使用 [**！ wudfext. umdevstack**](../debugger/-wudfext-umdevstack.md) (umdf 1) 或 [**！ wdfkd**](../debugger/-wdfkd-wdfumdevstack.md) (umdf 2) 查看有关所有堆栈层的信息。

5.  如果 IRP 超出了 UMDF 堆栈 (例如，如果堆栈位置0是当前正在处理 IRP 的位置) ，则确定相应的内核模式 IRP 未完成的原因。

 

