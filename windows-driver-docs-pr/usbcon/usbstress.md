---
description: 'USBStress 是用户模式应用程序 ( # A0) 和驱动程序安装包（用于内核模式驱动程序，usbstress.sys）的组合。'
title: USBStress
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81f3c862876ff4d277e11235d023e087dbfd027a
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010501"
---
# <a name="usbstress"></a>USBStress


USBStress 是用户模式应用程序 ( # A0) 和驱动程序安装包（用于内核模式驱动程序，usbstress.sys）的组合。

这些文件包含在 [MUTT](./mutt-software-package.md)软件包中。

## <a name="usbstress"></a>USBStress


USBStress 是一组集中在整个 USB 驱动程序堆栈和 USB 通用父驱动程序 ( # A0) 以及控制器及其上游集线器上的测试。 USBStress 随机选择测试并配置附加的测试设备。 由于测试的随机性质，建议你应在24小时内运行 USBStress，以允许更多的测试组合。

该工具可对测试设备进行各种传输长度的控制、大容量、同步的数据传输。 对于 SuperMUTT 设备，USBTCD 将数据传输到大容量终结点支持的流。

USBStress 驱动程序在很大程度上是自驱动的，也就是说，大多数 i/o 请求由驱动程序生成，而不是由应用程序生成。 驱动程序使用计时器和工作项来生成 i/o 和执行其他操作。 驱动程序检查注册表以确定是否应该运行其测试。 外部程序设置该注册表项。 此驱动程序的目标是在各种操作中创建尽可能多的并发性，以清理争用情况和同步问题。

此列表总结了 USBStress 执行的测试：

-   选择 "挂起" （带远程唤醒）。
-   大容量、中断和同步终结点上的并发读取/写入请求和取消。
-   并发字符串传输请求和取消。
-   批量终结点和取消的并发中止管道。
-   随机重置为意外-删除并重新枚举。
-   随机重置为意外-删除并重新枚举，并使重新枚举失败。
-   随机选择可用的备用接口。
-   随机指示设备卡住每个第 n 个控制传输。
-   随机指示 MUTT Pack (如果连接) 断开 VBUS 与暴露的下游端口的连接。
-   随机指示 MUTT Pack (如果连接的) 在暴露的下游端口上模拟超出当前状态。
-   随机指示 MUTT Pack (如果连接) 在集线器上执行硬件重置。

若要为 MUTT 设备安装 usbstress.sys 驱动程序，请将 MuttUtil 与 `-UpdateDriver ` 选项一起使用：

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