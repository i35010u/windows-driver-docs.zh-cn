---
title: 连接到 LPT 端口的打印机
description: 连接到 LPT 端口的打印机
ms.assetid: fbc71ae8-9b63-4667-b9d6-fdff9100d70b
keywords:
- LPT 枚举器 WDK 打印机
- 并行端口 WDK，打印机连接
- 并行的枚举器 WDk 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47eedb2de388de7a6f65aa3fff62f631c95a9f18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380024"
---
# <a name="printer-connected-to-an-lpt-port"></a>连接到 LPT 端口的打印机





LPT 枚举器的示例[总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540704)。 LPT 枚举器能够获取标识信息从符合 LPT 端口硬件*IEEE 1284 扩展功能端口协议和 ISA 接口标准*。

Windows 2000 或更高版本系统启动时，配置管理器将调用 LPT 枚举器枚举到 LPT 端口连接的 IEEE 1284 兼容设备。 对于每个找到的设备，配置管理器都会调用打印机类安装程序。 打印机类安装程序调用**SetupDi**-前缀[设备安装函数](https://msdn.microsoft.com/library/windows/hardware/ff541299)，其中获取信息从[打印机 INF 文件](printer-inf-files.md)。

对于与并行连接的打印机，并行的枚举器创建*devnode*加上一个唯一*硬件 ID*从其接收来自打印机的 1284年字符串生成。

示例 1284年字符串是：

```cpp
"MANUFACTURER:Hewlett-Packard;COMMAND SET:PJL,MLC,PCL,POSTSCRIPT;MODEL:HP Color LaserJet 550;CLASS:PRINTER;COMMENT:HP LaserJet;"
```

从此 1284年字符串并行枚举器将生成以下硬件 ID:

```cpp
LPTENUM\Hewlett-PackardHP_Co3115
```

硬件 ID 由枚举器前缀后, 跟制造商名称、 模型名称和循环冗余校验 (CRC) 代码组成。 从制造商和型号字符串生成的 CRC 代码，即硬件 ID 的最后四位数。 字符串中的空格替换为下划线。

若要从设备读取 1284 ID 字符串，将发送[ **IOCTL\_PAR\_查询\_设备\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff544076)。 请注意后台处理程序将重定向 LPT*x*符号链接 (其中*x*是 LPT 数字 1、 2 或 3） 到后台处理程序的命名管道，这意味着，如果正在后台处理程序，然后 parport 永远看不见 Ioctl 发送到型 LPTx。

并行连接插打印机 devnode 置于下**HKLM\\系统\\CurrentControlSet\\枚举\\LPTENUM**并且具有单个硬件 ID 的窗体：

```cpp
LPTENUM\Company_NameModelNam1234
```

按照下一步的代码示例图中显示驱动程序堆栈。

将正确"即插"窗体 LPTENUM 的硬件 ID 的 INF 代码\\*公司\_NameModelNam1234*在下面的示例所示。 请注意，"模型名称 XYZ"设备描述会显示两次在[ **INF 制造商部分**](https://msdn.microsoft.com/library/windows/hardware/ff547454)。 在第一行中的硬件 ID 包括总线枚举器时在第二行的 ID 不在硬件。 两行保证级别 0 硬件 ID 匹配的在其安装打印机的总线类型无关。 请参阅[安装自定义插件和播放的打印机驱动程序](installing-a-custom-plug-and-play-printer-driver.md)有关详细信息。

```cpp
[Manufacturer]
%Company_Name%=Company_Name

; Section name for all drivers for Company_Name
[Company_Name]
"Model Name XYZ" = Install_Section_XYZ, LPTENUM\Company_NameModelNam1234 ; plus any compatible IDs
"Model Name XYZ" = Install_Section_XYZ, Company_NameModelNam1234 ; plus any compatible IDs

; The install section for the XYZ model
[Install_Section_XYZ]

[Strings]
Company_Name="Company Name"
```

![并行端口打印机插](images/pnppar01.png)

共享的打印机及其*设备 ID* INF 文件应与其他模型，如下所示：

```cpp
[Manufacturer]
%Company_Name%=Company_Name

; The section for all drivers for Company_Name
[Company_Name]
"Model Name XYA" = Install_Section_XYA, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs
"Model Name XYA" = Install_Section_XYA, Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs
"Model Name XYB" = Install_Section_XYB, LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234; plus any other compatible IDs
"Model Name XYB" = Install_Section_XYB, Company_NameModelNam1234, Company_NameModelNam1234 ; plus any other compatible IDs

; The install sections
[Install_Section_XYA]

[Install_Section_XYB]

[ControlFlags]
InteractiveInstall = LPTENUM\Company_NameModelNam1234, Company_NameModelNam1234

[Strings]
Company_Name = "Company Name"
```

如同上一示例中，每个模型中[ **INF 制造商部分**](https://msdn.microsoft.com/library/windows/hardware/ff547454)由几乎完全相同的行的一对表示。 对于给定的模型，对中的一行包括总线枚举器;其他却没有。 两行保证级别 0 硬件 ID 匹配的在其安装打印机的总线类型无关。 请参阅[安装自定义插件和播放的打印机驱动程序](installing-a-custom-plug-and-play-printer-driver.md)有关详细信息。

 

 




