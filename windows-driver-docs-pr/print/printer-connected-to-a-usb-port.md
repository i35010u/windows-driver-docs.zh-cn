---
title: 连接到 USB 端口的打印机
description: 连接到 USB 端口的打印机
keywords:
- USB 打印机 WDK
- 总线类型打印机驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84da99531eae8337725046f814aecf71361fe72d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807351"
---
# <a name="printer-connected-to-a-usb-port"></a>连接到 USB 端口的打印机





当使用 usb 端口的通用串行总线 (USB) 打印机连接时，USB 总线驱动程序将创建一个物理设备对象 (PDO) ，其 *硬件 ID* 格式为 VIDvvPIDpp，并具有 *兼容 ID* 类 \_ 7。 此的 *devnode* 在 "枚举 \\ USB ..." 下创建 \\ 类 \_ 7 并标识通过 USB 端口连接的打印机设备。 即插即用加载 usbprint.sys 使用 usbprint 中类7上的兼容 ID 匹配 \_ 。

Usbprint 中用于为任何 USB 打印机设备加载 usbprint.sys 的条目是：

```cpp
[Microsoft]
%USBPRINT.DeviceDesc% = USBPRINT_Inst,USB\Class_07,GENERIC_USB_PRINTER
```

Usbprint.sys 查询即插即用的打印机以获取1284字符串，并生成与并行总线枚举器兼容的硬件 ID。  (有关详细信息，请参阅 [USBPRINT 接口](usb-printing.md)。 ) 它将创建一个物理设备对象 (PDO) ，该对象的 Devnode 在枚举 \\ USBPRINT 下，并具有以下格式的两个硬件 id：

```cpp
USBPRINT\Company_NameModelNam1234
```

下图显示了通过 USB 端口连接的打印机的驱动程序堆栈。

![usb 打印机的即插即用](images/pnpusb01.png)

以下示例显示了 [**INF 制造商部分**](../install/inf-manufacturer-section.md) 中可用于安装 USB 或其他总线类型打印机驱动程序的条目。 如果打印机安装在 USB 总线上，第一行可保证级别0的硬件 ID 匹配。 如果打印机安装在另一台总线上，则第二行保证排名0的硬件 ID 匹配。 有关详细信息，请参阅 [安装自定义即插即用打印机驱动程序](installing-a-custom-plug-and-play-printer-driver.md)。

```cpp
 "Model Name XYZ" = Install_Section_XYZ, USBPRINT\Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs  
"Model Name XYZ" = Install_Section_XYZ, Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs
```

 

