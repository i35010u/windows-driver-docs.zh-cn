---
description: 如何运行压力与传输以及超级 MUTT 性能测试。
title: 如何对 MUTT 设备运行压力和传输性能测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4333f77e94c39c367919ac2f5047bfcaf999674
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009951"
---
# <a name="how-to-run-stress-and-transfer-performance-tests-for-mutt-devices"></a>如何对 MUTT 设备运行压力和传输性能测试


了解如何运行压力与传输以及超级 MUTT 性能测试。

压力测试和传输测试旨在实现总线协议和主机控制器软件的饱和。 这些测试对 MUTT 设备执行多个同时进行的 i/o 传输和取消。 MUTT 固件被设计为在这些测试期间无法传输。 这些故障可模拟控制器或 USB 驱动程序堆栈公开的错误情况，并在出现 "压力" USB 条件下。

## <a name="how-to-run-stress-and-transfer-tests"></a>如何运行压力测试和传输测试


1.  在将 MUTT 设备连接到可用端口的测试系统上，打开已提升权限的命令窗口。
2.  导航到测试文件夹，例如 **C： \\ usbTest**。
3.  传输和压力测试将通过同一脚本返回回。 若要运行脚本，请运行脚本 runtest.bat：

    **C： \\ usbTest \\runtest.bat**

编写的 .bat 文件会无限期地运行测试。 测试至少应运行30分钟。 若要进行更详尽的测试，请考虑在八小时内运行这些测试。 批处理文件包含可以执行的其他优化的注释。

若要退出所有测试，请在命令窗口中按 **ctrl-c** 。 如果系统不会在运行过程中生成错误检查并从命令窗口中完全退出，则测试运行被视为成功 (或正运行) 。 如果该工具不能完全退出，则表明传输未完成，必须调查。

## <a name="how-to-run-supermutt-performance-tests"></a><a href="" id="supermutt-perf"></a>如何运行 SuperMUTT 性能测试


1.  在将 SuperMUTT 附加到 xHCI 控制器的测试系统上打开提升的命令窗口。
2.  导航到测试文件夹，例如 **C： \\ usbTest**。
3.  运行名为 **FX3Perf.bat** 的脚本以启动测试运行。

## <a name="related-topics"></a>相关主题
[USB](../index.yml)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)