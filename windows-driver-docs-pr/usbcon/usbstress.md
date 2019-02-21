---
Description: USBStress is the combination of a user-mode application (usbstress.exe) and driver installation package for the kernel-mode driver, usbstress.sys.
title: USBStress
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a321240256a9550d82e9b72ef96eaf8d0cd33cfa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546182"
---
# <a name="usbstress"></a>USBStress


USBStress 是用户模式应用程序 (usbstress.exe) 和内核模式驱动程序的驱动程序安装包的组合 usbstress.sys。

这些文件包括在[MUTT 软件包](https://msdn.microsoft.com/windows/hardware/jj590752)。

## <a name="usbstress"></a>USBStress


USBStress 是一组测试侧重于整个 USB 驱动程序堆栈和 USB 通用父驱动程序 (Usbccgp.sys) 和控制器和其上游的中心。 USBStress 随机选择测试，并配置附加的测试设备。 由于测试的随机特性，我们建议您应运行 USBStress 24 小时时间段内以允许更多的测试组合。

此工具将执行控制，大容量、 等时，数据传输的各种传输长度与测试设备。 对于 SuperMUTT 设备，USBTCD 将数据传输到流支持的大容量终结点。

USBStress 驱动程序是很大程度上自驱动，也就是说，大多数 I/O 请求都由驱动程序并不是应用程序。 驱动程序使用计时器和工作项来生成 I/O 以及执行其他操作。 该驱动程序会检查注册表，以确定是否应运行其测试。 外部程序设置该注册表项。 此驱动程序的目标是尽可能以彻底的争用条件和同步问题的各种操作之间创建太多并发。

此表总结了 USBStress 执行的测试：

-   选择性挂起远程唤醒。
-   在大容量、 中断，并同步终结点和取消的并发读/写请求。
-   并发字符串传输请求和取消。
-   在大容量终结点和取消的并发中止管道。
-   意外删除和重新枚举的随机重置。
-   意外删除和重新枚举和失败重新枚举的随机重置。
-   随机选择一个可用的备用接口。
-   随机指示设备操作计划的每个第 n 个控制传输。
-   随机指示 MUTT 包 （如果已连接） 以断开 VBUS 与公开的下游端口的连接。
-   随机指示 MUTT 包 （如果已连接），以模拟过流公开下游端口上的情况。
-   随机指示 MUTT 包 （如果已连接） 来执行硬件集线器上重置。

若要安装 MUTT 设备 usbstress.sys 驱动程序，请使用与 MuttUtil`-UpdateDriver `选项：

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateDriver usbstress.inf
Return value: 0


c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078E&REV_8011 :             0  : USBSTRESS
Return value: 1
```

## <a name="related-topics"></a>相关主题
[USB 测试工具](usb-test-tools.md)  
[MUTT 软件包中的工具](mutt-software-package.md)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



