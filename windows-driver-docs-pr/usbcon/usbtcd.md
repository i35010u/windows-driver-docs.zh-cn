---
description: USBTCD 是用户模式应用程序和内核模式驱动程序的组合。
title: USBTCD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1da859bb5e60044239ba8f07277dc30f45bcba18
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92356027"
---
# <a name="usbtcd-package"></a>USBTCD 包

USBTCD 是用户模式应用程序和内核模式驱动程序的组合。 该工具执行读写操作。 它启动与测试设备之间的各种传输长度的控制、大容量、同步数据传输。 对于 SuperMUTT 设备，USBTCD 将数据传输到大容量终结点支持的流。 它还可以将传输缓冲区作为链式 MDLs 发送。 在这种情况下，可以指定传输缓冲区中的段数。

USBTCD 文件包含在 [MUTT](./index.md)软件包中。

## <a name="usbtcd"></a>USBTCD

若要使用这些命令，必须将 USBTCD 驱动程序 ( # A0) 作为设备的函数驱动程序加载。 若要加载设备的驱动程序，请运行 MUTTUtil 并指定 **USBTCD**。 此工具为所有连接的 USB 设备加载 **USBTCD.sys** 。

``` syntax
c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -UpdateDriver usbtcd.inf
Return value: 0


c:\Program Files (x86)\USBTest\x64>MuttUtil.exe -list
       :    : HARDWARE ID                    :  PROBLEM CODE  : DRIVER
DEVICE :  0 : USB\VID_045E&PID_078E&REV_8011 :             0  : USBTCD
Return value: 1
```

你可以使用以下命令来测量与 SuperMUTT 设备的大容量终结点之间的传输性能。

```console
Usbtcd –perf –read 1 100 2 10240000 0

Usbtcd –perf –write 1 100 0 10240000 0
```

在上述命令中，USBTCD 从管道2读取10240000字节。 在第二个命令中，USBTCD 开始一个写入操作，其中10240000字节发送到管道0。 对于这两个命令，该工具执行操作100次，并且不指定超时值。

这些命令用于测量 MUTT 设备的批量终结点的性能。 请注意，在这种情况下，传输大小会降低。

```console
Usbtcd –perf –read 1 100 2 512000 0

Usbtcd –perf –write 1 100 0 512000 0
```

这些命令测量 SuperMUTT 设备的批量终结点流的数据传输性能。 目前，设备固件每隔一毫秒就会尝试切换流，同时向主机发送一个 ERDY 和新的流号。 使用设备内的计时器实现。

```console
Usbtcd –sread 1 100 7 1 1024 0

Usbtcd –swrite 1 100 6 1 1024 0
```

在上述命令中，USBTCD 读取和写入 SuperMUTT 设备的大容量终结点中的特定流。 在第一个命令中，该工具启动一个工作线程，该工作线程读取与管道7关联的流1中的1024个字节。 同样，第二个命令将1024字节写入与管道6关联的流1。 对于这两个命令，该工具执行操作100次，并且不指定超时值。

若要查看有关 USBTCD 的帮助，请运行以下命令：

```console
usbtcd -?
```

命令显示有关命令行选项的信息。 可以在命令行上指定传输大小、详细级别、传输超时等。

## <a name="related-topics"></a>相关主题

[MUTT 软件包中的工具](mutt-software-package.md)  

[Microsoft USB 测试工具 (MUTT) 设备](microsoft-usb-test-tool--mutt--devices.md)  
