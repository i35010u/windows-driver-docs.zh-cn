---
title: 连接到 LPT 端口的打印机
description: 连接到 LPT 端口的打印机
ms.assetid: fbc71ae8-9b63-4667-b9d6-fdff9100d70b
keywords:
- LPT 枚举器 WDK 打印机
- 并行端口 WDK，打印机连接
- 并行枚举器 WDk 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e749520ed0942c0f1538f2b9ffb8216db8b55dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840440"
---
# <a name="printer-connected-to-an-lpt-port"></a>连接到 LPT 端口的打印机





LPT 枚举器是[总线驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)的一个示例。 LPT 枚举器能够从 LPT 端口硬件获取符合*IEEE 1284 扩展功能端口协议和 ISA 接口标准*的标识信息。

当 Windows 2000 或更高版本的系统启动时，配置管理器将调用 LPT 枚举器来枚举连接到 LPT 端口的与 IEEE 1284 兼容的设备。 对于找到的每个设备，配置管理器将调用打印机类安装程序。 打印机类安装程序调用**SetupDi**前缀的[设备安装功能](https://docs.microsoft.com/previous-versions/ff541299(v=vs.85))，该功能将从[打印机 INF 文件](printer-inf-files.md)中获取信息。

对于并行连接的打印机，并行枚举器使用从打印机接收的1284字符串生成的唯一*硬件 ID*创建*devnode* 。

示例1284字符串是：

```cpp
"MANUFACTURER:Hewlett-Packard;COMMAND SET:PJL,MLC,PCL,POSTSCRIPT;MODEL:HP Color LaserJet 550;CLASS:PRINTER;COMMENT:HP LaserJet;"
```

从此1284字符串，并行枚举器生成以下硬件 ID：

```cpp
LPTENUM\Hewlett-PackardHP_Co3115
```

硬件 ID 由枚举器前缀组成，后跟制造商名称、型号名称和循环冗余检查（CRC）代码。 CRC 代码是硬件 ID 的最后四位数字，是从制造商和模型字符串生成的。 字符串中的空格将替换为下划线。

若要从设备读取 1284 ID 字符串，请发送[**IOCTL\_PAR\_QUERY\_设备\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_device_id)。 请注意，后台处理程序将 LPT*x*符号链接（其中*x*是 lpt 号1、2或3）重定向到后台处理程序的命名管道，这意味着，如果后台处理程序正在运行，则 parport 永远看不到发送到 LPTx 的 IOCTLs。

并行连接即插即用打印机的 devnode 置于**HKLM\\SYSTEM\\CurrentControlSet\\枚举\\LPTENUM** ，并具有以下格式的单个硬件 ID：

```cpp
LPTENUM\Company_NameModelNam1234
```

驱动程序堆栈显示在下一个代码示例中。

下面的示例显示了可正确地 "即插即用" 的硬件 ID 为 LPTENUM\\*Company\_NameModelNam1234*的 INF 代码。 请注意，"模型名称 XYZ" 设备说明在[**INF 制造商部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)出现了两次。 第一行中的硬件 ID 包含总线枚举器，而第二行中的硬件 ID 则不包含。 无论安装打印机的总线类型如何，这两行均可保证1级硬件 ID 匹配。 有关详细信息，请参阅[安装自定义即插即用打印机驱动程序](installing-a-custom-plug-and-play-printer-driver.md)。

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

![用于并行端口打印机的即插即用](images/pnppar01.png)

对于与其他模型共享其*设备 ID*的打印机，INF 文件应如下所示：

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

正如前面的示例中一样，" [**INF 制造商" 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)中的每个模型均由一对几乎相同的行来表示。 对于给定的模型，该配对中的一行包含总线枚举器;另一种情况不是。 无论安装打印机的总线类型如何，这两行均可保证1级硬件 ID 匹配。 有关详细信息，请参阅[安装自定义即插即用打印机驱动程序](installing-a-custom-plug-and-play-printer-driver.md)。

 

 




