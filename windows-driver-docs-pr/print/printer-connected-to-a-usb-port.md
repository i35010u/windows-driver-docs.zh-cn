---
title: 连接到 USB 端口的打印机
description: 连接到 USB 端口的打印机
ms.assetid: 85e238e1-4dc1-4720-b383-d6aaed72e560
keywords:
- USB 打印机 WDK
- 总线类型的打印机驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c46f2f38e1f7cfc558616bb65103793175c45916
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380673"
---
# <a name="printer-connected-to-a-usb-port"></a>连接到 USB 端口的打印机





当通过 USB 端口连接通用串行总线 (USB) 打印机时，USB 总线驱动程序将创建一个物理设备对象 (PDO)*硬件 ID*窗体 VIDvvPIDpp，并*兼容 ID*类\_7。 *Devnode*这是创建下枚举\\USB\\ ...类\_7 并识别通过 USB 端口连接的打印机设备。 插加载类上使用兼容 ID 匹配项的 usbprint.sys\_从 usbprint.inf 7。

从用于加载任何 USB 打印机设备的 usbprint.sys usbprint.inf 项是：

```cpp
[Microsoft]
%USBPRINT.DeviceDesc% = USBPRINT_Inst,USB\Class_07,GENERIC_USB_PRINTER
```

Usbprint.sys 查询插打印机获取 1284年字符串，并生成与并行总线枚举器兼容的硬件 ID。 (有关详细信息，请参阅[USBPRINT 接口](usb-printing.md)。)它创建其 devnode 是枚举下一个物理设备对象 (PDO)\\USBPRINT，并具有两个硬件 Id，采用以下形式：

```cpp
USBPRINT\Company_NameModelNam1234
```

下图显示了通过 USB 端口连接的打印机驱动程序堆栈。

![usb 打印机插](images/pnpusb01.png)

下面的示例演示中的条目[ **INF 制造商部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section) ，可以用来安装 USB 或其他总线类型的打印机驱动程序。 如果 USB 总线上安装打印机，第一行可保证级别 0 硬件 ID 匹配项。 第二行可保证级别 0 硬件 ID 匹配项，如果另一个总线上安装打印机。 有关详细信息，请参阅[安装自定义插件和播放的打印机驱动程序](installing-a-custom-plug-and-play-printer-driver.md)。

```cpp
 "Model Name XYZ" = Install_Section_XYZ, USBPRINT\Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs  
"Model Name XYZ" = Install_Section_XYZ, Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs
```

 

 




