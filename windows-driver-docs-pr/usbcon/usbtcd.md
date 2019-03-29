---
Description: USBTCD is the combination of a user-mode application and kernel-mode driver.
title: USBTCD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d8e248fed9356c98e46843caed4f538cfaf3faa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568174"
---
# <a name="usbtcd"></a>USBTCD


USBTCD 是用户模式应用程序和内核模式驱动程序的组合。 此工具将执行读取和写入操作。 初始化控件，大容量、 等时，数据传输的各种传输长度与测试设备。 对于 SuperMUTT 设备，USBTCD 将数据传输到流支持的大容量终结点。 它还可以作为链接 MDLs 发送的传输缓冲区。 在这种情况下，您可以传输缓冲区中指定的段数。

USBTCD 文件包含在[MUTT 软件包](https://msdn.microsoft.com/windows/hardware/jj590752)。

## <a name="usbtcd"></a>USBTCD


若要使用这些命令，必须为该设备的功能驱动程序加载 USBTCD 驱动程序 (USBTCD.sys)。 若要加载的设备驱动程序，运行 MUTTUtil 并指定**USBTCD.inf**。 此工具加载**USBTCD.sys**的所有连接的 USB 设备。

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateDriver usbtcd.inf
Return value: 0


c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078E&REV_8011 :             0  : USBTCD
Return value: 1
```

可以使用以下命令来度量 SuperMUTT 设备的大容量终结点相互传输的性能。

**Usbtcd – 性能 – 读取 1 100 2 10240000 0**

**Usbtcd – 性能 – 编写 1 100 0 10240000 0**

在上述命令中，USBTCD 从管道 2 读取使用 10240000 字节。 在第二个命令中，USBTCD 开始写操作使用 10240000 字节发送管道 0 到何处。 这两个命令，该工具执行 100 次的操作，且未指定超时值。

这些命令用于衡量性能的大容量的 MUTT 设备的终结点。 请注意，在这种情况下减少了传输大小。

**Usbtcd – 性能 – 读取 1 100 2 512000 0**

**Usbtcd – 性能 – 编写 1 100 0 512000 0**

这些命令测量数据流的大容量的 SuperMUTT 设备的终结点的数据传输的性能。 目前，设备固件尝试切换流每隔一毫秒发送新的流数以及 ERDY 到主机。 使用计时器在设备内实现。

**Usbtcd – sread 1 100 7 1 1024年 0**

**Usbtcd – 程序书写 1 100 6 1 1024年 0**

在上述命令，USBTCD 读取和写入 SuperMUTT 设备在大容量终结点中的特定流。 在第一个命令中，此工具将启动一个工作线程，从流使用的管道 7 关联的 1 中读取 1024 字节。 同样，第二个命令写入 1024 个字节进行流式处理 1 与管道 6 关联。 这两个命令，该工具执行 100 次的操作，且未指定超时值。

若要查看上 USBTCD 帮助，请运行以下命令：

**usbtcd -?**

该命令显示有关命令行选项的信息。 可以在命令行上指定传输大小、 详细级别、 传输超时和的详细信息。

## <a name="related-topics"></a>相关主题
[USB 测试工具](usb-test-tools.md)  
[MUTT 软件包中的工具](mutt-software-package.md)  
[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  



