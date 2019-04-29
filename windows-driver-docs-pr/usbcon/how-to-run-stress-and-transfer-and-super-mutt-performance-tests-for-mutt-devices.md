---
Description: 如何运行压力和传输和超级 MUTT 性能测试。
title: 如何对 MUTT 设备运行压力和传输性能测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d254c6e79297fa8ede9d4d7718afda88e3f03296
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366040"
---
# <a name="how-to-run-stress-and-transfer-performance-tests-for-mutt-devices"></a>如何对 MUTT 设备运行压力和传输性能测试


了解如何运行压力和传输和超级 MUTT 性能测试。

压力和传输测试面向饱和总线协议和主机控制器软件。 这些测试执行多个同时进行的 I/O 传输和取消到 MUTT 设备。 MUTT 固件进行编程，这些测试中失败传输。 这些故障模拟错误条件的控制器或 USB 驱动程序堆栈紧张 USB 条件下，会面临。

## <a name="how-to-run-stress-and-transfer-tests"></a>如何运行压力和传输测试


1.  打开提升的命令窗口上的测试系统具有 MUTT 设备连接到可用端口。
2.  导航到测试的文件夹，例如**c:\\usbTest**。
3.  传输和压力测试通过同一个脚本连续不断地运行。 若要运行它们，请运行脚本 runtest.bat:

    **C:\\usbTest\\runtest.bat**

所编写的.bat 文件将无限期运行的测试。 至少 30 分钟运行测试。 对于更详尽的测试，请考虑运行 8 小时一次这些测试。 批处理文件包含可进行其他优化的注释。

若要退出所有测试，请按**Ctrl + C**命令窗口中。 如果系统不会生成运行和退出完全从命令窗口期间的错误检查，测试运行被视为可成功 （或一个正运行）。 如果该工具不会完全退出，则它表示传输没有完成，且必须进行调查。

## <a href="" id="supermutt-perf"></a>如何运行 SuperMUTT 性能测试


1.  打开提升的命令窗口具有 SuperMUTT 附加到 xHCI 控制器的测试系统上。
2.  导航到测试的文件夹，例如**c:\\usbTest**。
3.  运行脚本名为**FX3Perf.bat**启动测试运行。

## <a name="related-topics"></a>相关主题
[USB](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



