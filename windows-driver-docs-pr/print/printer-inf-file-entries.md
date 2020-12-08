---
title: 打印机 INF 文件项
description: 打印机 INF 文件项
keywords:
- INF 文件 WDK 打印，条目
- 依赖文件 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee8bd2298fd3326c81d916d9e2e5d7cbd9c1aacf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807271"
---
# <a name="printer-inf-file-entries"></a>打印机 INF 文件项





对于安装应用程序以在打印服务器上安装打印机，它必须调用后台处理程序的 **AddPrinterDriverEx** 函数来加载驱动程序文件，然后调用后台处理程序的 **interactivesession.addprinter** 函数，使打印机在服务器上可用。

**AddPrinterDriverEx** 函数需要使用驱动程序 \_ 信息 \_ 3 结构作为输入，并且 **Interactivesession.addprinter** 函数需要将打印机 \_ info \_ 2 结构作为输入。 默认的 Windows 2000 或更高版本的打印机类安装程序 Ntprint.dll，读取打印机 INF 文件以获取在调用函数之前必须放入这些结构中的字符串值。


Microsoft Windows SDK 文档中介绍了 **AddPrinterDriverEx** 和 **interactivesession.addprinter** 函数以及驱动程序 \_ 信息 \_ 3 和打印机 \_ 信息 \_ 2 结构。

已定义 Ntprint.dll 识别的打印机驱动程序的一组 INF 文件项。 这些项的格式如下：

*EntryName*  = *值*

其中， *EntryName* 是标识条目的字符串，而 *值* 是分配给条目的字符串值。

下表列出了应包含在打印机 INF 文件中的 INF 文件条目。 对于每个条目，此表包括以下内容：

-   应分配给该项的值。

-   如果未定义该项，则 Ntprint.dll 使用的默认值。

-   结构成员，Ntprint.dll 在其中放置指向输入值的指针。

| INF 文件条目       |“值”|如果未指定条目 (默认值) |结构成员 |
|----------------------|-----|-------------|-----------------------------------------|
| ConfigFile           | 驱动程序的 [打印机接口 DLL](printer-interface-dll.md)的名称。 | 为 DriverFile 指定的值。 | **pConfigFile** \_ \_ Windows SDK 文档中所述的驱动程序信息3结构 (pConfigFile 成员)  |
| DataFile             | 驱动程序的关联数据文件（如 PPD 文件）的名称。 | INF 文件中的驱动程序的部分名称。 | **pDataFile** 驱动程序 \_ 信息 \_ 3 结构的 pDataFile 成员 |
| DefaultDataType      | 不用于基于 NT 的操作系统。 |||
| DriverCategory       | 请参阅此表后面的 **注释 1**。 | 如果 INF 文件未指定 (如大多数 v3 驱动程序) 的驱动程序类别，则假定驱动程序的类别为 **PrintFax**。 | 无 |
| DriverFile           | 驱动程序的 [打印机图形 DLL](printer-graphics-dll.md)的名称。 | INF 文件中的驱动程序的部分名称。 | **pDriverPath** 驱动程序 \_ 信息 \_ 3 结构的 pDriverPath 成员 |
| ExcludeFromSelect    | 请参阅此表后面的 **注释 2**。 | 无 | 无 |
| HelpFile             | 接口 DLL 的帮助文件的名称。 | 无。 未指定帮助文件。 | **pHelpFile** 驱动程序 \_ 信息 \_ 3 结构的 pHelpFile 成员 |
| LanguageMonitor      | 要与打印机驱动程序关联的语言监视器的名称。 请参阅 **LanguageMonitor 值格式** 部分。 | 无。 未指定语言监视器。 | **pMonitorName** 驱动程序 \_ 信息 \_ 3 结构的 pMonitorName 成员 |
| PrintProcessor       | 要与打印机队列关联的打印处理器的名称。 请参阅 **PrintProcessor 值格式** 部分。 | 使用 (WinPrint) 的默认打印处理器。 | **pPrintProcessor** \_ \_ Windows SDK 文档中所述的驱动程序信息2结构的成员 ()  |
| VendorSetup          | 供应商提供的 DLL 中用于处理 [自定义打印机设置操作](customized-printer-setup-operations.md)的函数的名称。 | 无。 请参阅此表后面的 **注释 3**。 | 无 |
| InboxVersionRequired | INF 引用的所有核心驱动程序可接受的最低版本。 有关 InboxVersionRequired 的详细信息，请参阅 [INF InboxVersionRequired 指令](inf-inboxversionrequired-directive.md)。 | 无 | 无 |

 

 **注意**  **1 (DriverCategory)**：如果 INF 文件指定类别，则这些值) 分别是 (0 到5之间的值，用于指定类别：
 
 
| 驱动程序类别          | “值” | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------|-------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PrintFax.Printer         | 0     | 一种打印队列，它代表连接到计算机的打印机 (通过本地或网络协议) 或另一台计算机上的物理打印机的代理。 当用户打印到物理打印机时，结果为纸张，其中打印了文档。                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| PrintFax.Fax             | 1     | 表示物理或虚拟传真计算机的打印队列。 当用户打印到传真打印机时，结果 (可能在进一步用户交互之后) 为发送传真。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| PrintFax    | 2     | 一种打印队列，用于生成软复制文档。 用户打印到文件打印机时，用户必须首先输入文件名，然后后台处理程序会将打印输出发送到该文件。 文件打印机始终需要文件名，但不需要其他用户输入。 如果用户没有提供文件名的选项，应用程序将生成一个可用于后台处理程序的文件名。 文件打印机的常见示例包括 Microsoft XPS 文档编写器 (MXDW) 和 PDF 编写器。                                                                                                                                                                                                                                                 |
| PrintFax | 3     | 一种打印队列，其中包含对打印后台处理程序不透明的打印数据执行某种操作。 当用户打印到虚拟打印机时，某些可能的结果包括保存在计算机上某个位置的打印文档、发送到其他应用程序或通过电子邮件发送。 打印到虚拟打印机的一个常见示例是将打印文档发送到 Microsoft Office OneNote 打印机的情况。 当用户选择打印到虚拟打印机时，可能需要进一步的用户交互，由驱动程序或某个其他驱动程序组件启动。 有关详细信息，请参阅 [打印机 INF 文件中的虚拟打印机](virtual-printers-in-printer-inf-files.md)。 |
| PrintFax | 4     | 表示打印服务的打印队列。 当用户选择打印到服务时，结果 (可能在进一步的用户交互之后) 是第三方打印服务接收到打印内容。 然后，用户可以在物理业务位置上选择打印输出。                                                                                                                                                                                                                                                                                                                                                                                                                            |
| PrintFax.Printer.3D      | 5     | 表示三维打印机数据流的打印队列。 如果为二维打印机指定了意外的类别 (常规打印机) ，则2D 打印机只会输出数据流的2D 内容。 如果为3D 打印机指定了正确的类别，但将2D 数据流发送到3D 打印机，则3D 打印机不会生成任何输出。                                                                                                                                                                                                                                                                                                                                                                |

 

另请注意，v4 打印驱动程序使用清单文件。 有关详细信息，请参阅 [V4 驱动程序清单](v4-driver-manifest.md)。

 

**注意****2 (ExcludeFromSelect)**：不应显示在 "**选择设备**" 对话框或 "添加打印机" 向导中的设备的 *设备 ID* 。   对于打印机，这包括 INF 文件中具有重复设备说明的设备的所有 PnP 条目;例如，具有多个用于红外和并行枚举的条目的设备，或其他总线的设备。 与此表中的所有其他项不同，ExcludeFromSelect 项必须出现在 INF 文件的 "控件标志" 部分中。 有关详细信息，请参阅 [**INF ControlFlags 部分**](../install/inf-controlflags-section.md) 。

 

**注意**  **3 (VendorSetup)**：如果未指定 VendorSetup 项，则不会执行自定义安装操作。 具体而言，打印处理器、打印监视器或打印机驱动程序安装期间不允许用户界面，除非使用 VendorSetup INF 条目。 有关此项的详细信息，请参阅 [自定义打印机设置操作](customized-printer-setup-operations.md)。

 

**重要说明**  ： VendorSetup 现已弃用，不应由你开发的任何 *新* v3 或 v4 驱动程序使用。 仅提供有关 VendorSetup 的信息以供参考，或用于维护已使用此 INF 指令的现有 v3 驱动程序。

 

打印机 INF 文件条目通常在 " [打印机 inf 文件数据" 部分](printer-inf-file-data-sections.md)中指定。 有关示例，请参阅 [打印机 INF 文件示例](sample-printer-inf-files.md)。

### <a name="languagemonitor-value-format"></a><a href="" id="ddk-languagemonitor-value-format-gg"></a>LanguageMonitor 值格式

当打印机 INF 文件中包含 LanguageMonitor 项时，值格式如下所示：

LanguageMonitor = " *了* ， *MonitorDLLName* "

其中， *了* 是表示监视器显示名称的文本字符串，而 *MONITORDLLNAME* 是监视器 DLL 的文件名。

### <a name="printprocessor-value-format"></a><a href="" id="ddk-printprocessor-value-format-gg"></a>PrintProcessor 值格式

当打印机 INF 文件中包含 PrintProcessor 项时，值格式如下所示：

PrintProcessor = " *PrintProcessorName* ， *PrintProcessorDLLName* "

其中， *PrintProcessorName* 是表示打印处理器显示名称的文本字符串， *PrintProcessorDLLName* 是 DLL 的文件名。

### <a name="dependent-files"></a><a href="" id="ddk-dependent-files-gg"></a>依赖文件

对于 Windows 2000 和更高版本，依赖文件是一个打印机驱动程序文件，该文件包含在 dirid 为66000的 "[打印机 INF 文件安装" 部分](printer-inf-file-install-sections.md)中，但未分配给 "DriverFile"、"数据文件"、" [dirid](printer-dirids.md) " 或 "帮助项" 条目。

下面的示例演示了一个 INF 文件中的摘录，该文件通过将三个从属文件复制到 dirid 66000) 指定的目录，将这些文件复制到打印机驱动程序目录中 (：

```cpp
[Contoso]
%PRINTER_MODEL_123%=Contoso_Install_Section,LPTENUM\Contoso_1284.4_P29C5
...
[Contoso_Install_Section]
CopyFiles=@Contoso.ini,@Contoso.xml,@Contoso.dll
...
[DestinationDirs]
DefaultDestDir=66000
...
[Strings]
PRINTER_MODEL_123 = "Contoso Printer Model 123"
```

在此示例中，Contoso.ini 是打印机 INI 文件，Contoso.xml 是一个双向扩展文件，Contoso.dll 是一个自定义的组件。 有关打印机 INI 文件、双向扩展文件和自定义组件的详细信息，请参阅 [安装自定义驱动程序组件](installing-customized-driver-components.md) 和 [双向通信架构](bidirectional-communication-schema.md)。

[点和打印](introduction-to-point-and-print.md) 操作会在客户端上安装与驱动程序和驱动程序相关的文件。

最多可为每个打印机型号指定64个依赖文件。

## <a name="related-topics"></a>相关主题
[双向通信架构](bidirectional-communication-schema.md)  
[**INF ControlFlags 节**](../install/inf-controlflags-section.md)  
[安装自定义的驱动程序组件](installing-customized-driver-components.md)  
[点和-打印](introduction-to-point-and-print.md)  
[打印机 INF 文件安装部分](printer-inf-file-install-sections.md)  
[V4 驱动程序清单](v4-driver-manifest.md)
