---
title: 打印机 INF 文件项
description: 打印机 INF 文件项
ms.assetid: 897072bb-e481-4c8d-a2bf-57b19c69ac0e
keywords:
- INF 文件 WDK 打印，条目
- 依赖文件 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 812dff15cb58d8d0901c33a73cd6c9044c8bfbe1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356048"
---
# <a name="printer-inf-file-entries"></a>打印机 INF 文件项





安装应用程序的打印服务器上安装打印机，它必须调用后台处理程序的**AddPrinterDriverEx**函数来加载驱动程序文件，然后调用后台处理程序的**AddPrinter**函数使打印机服务器上可用。

**AddPrinterDriverEx**函数需要一个驱动程序\_信息\_3 结构作为输入，并且**AddPrinter**函数需要打印机\_信息\_作为输入的 2 个结构。 默认值为 Windows 2000 或更高版本的打印机类安装程序 Ntprint.dll，读取打印机 INF 文件，以获取在调用函数之前必须放置在这些结构的字符串值。


**AddPrinterDriverEx**并**AddPrinter**函数，以及驱动程序\_信息\_3 和打印机\_信息\_2 结构Microsoft Windows SDK 文档中所述。

已定义 Ntprint.dll 可识别的打印机驱动程序的 INF 文件项的一组。 这些条目具有以下格式：

*EntryName* = *Value*

其中*EntryName*是用于标识该条目的字符串并*值*是分配给该条目的字符串值。

下表列出了应在打印机 INF 文件中包含的 INF 文件条目。 对于每个项，表包括以下组件：

-   应分配到条目的值。

-   如果未定义该条目 Ntprint.dll 则使用默认值。

-   结构成员 Ntprint.dll 将在其中放置指向条目值的指针。

| INF 文件条目       |值|默认值 （如果不指定项）|结构成员 |
|----------------------|-----|-------------|-----------------------------------------|
| ConfigFile           | 驱动程序的名称[打印机接口 DLL](printer-interface-dll.md)。 | 指定 DriverFile 的值。 | **pConfigFile**驱动程序的成员\_信息\_3 结构 （Windows SDK 文档中所述） |
| DataFile             | 驱动程序的关联的数据文件，如 PPD 文件的名称。 | 驱动程序的 INF 文件中的节名称。 | **pDataFile**驱动程序的成员\_信息\_3 结构 |
| DefaultDataType      | 不使用与 NT 基于操作系统的系统。 |||
| DriverCategory       | 请参阅**备注 1**，此表后面。 | 如果 INF 文件未指定驱动程序类别 （如大多数 v3 驱动程序），则假设条件是驱动程序的类别都**PrintFax.Printer**。 | 无 |
| DriverFile           | 驱动程序的名称[打印机图形 DLL](printer-graphics-dll.md)。 | 驱动程序的 INF 文件中的节名称。 | **pDriverPath**驱动程序的成员\_信息\_3 结构 |
| ExcludeFromSelect    | 请参阅**备注 2**，此表后面。 | 无 | 无 |
| HelpFile             | 接口 DLL 的帮助文件的名称。 | 无。 未指定帮助文件。 | **pHelpFile**驱动程序的成员\_信息\_3 结构 |
| LanguageMonitor      | 要与打印机驱动程序相关联的语言监视器的名称。 请参阅**LanguageMonitor 值格式**部分。 | 无。 未指定语言监视器。 | **pMonitorName**驱动程序的成员\_信息\_3 结构 |
| PrintProcessor       | 要与打印机队列相关联的打印处理器的名称。 请参阅**PrintProcessor 值格式**部分。 | 使用默认的打印处理器 (WinPrint)。 | **pPrintProcessor**驱动程序的成员\_信息\_2 结构 （Windows SDK 文档中所述） |
| VendorSetup          | 供应商提供的 DLL 中函数的名称，用于处理[自定义的打印机安装程序操作](customized-printer-setup-operations.md)。 | 无。 请参阅**备注 3**，此表后面。 | 无 |
| InboxVersionRequired | INF 引用的所有核心驱动程序的最低可接受的版本。 有关 InboxVersionRequired 详细信息，请参阅[INF InboxVersionRequired 指令](inf-inboxversionrequired-directive.md)。 | 无 | 无 |

 

 **请注意**  **1 (DriverCategory)** :如果 INF 文件指定一个类别，这些是允许的值 (0 到 5 分别) 为指定类别：
 
 
| 驱动程序类别          | 值 | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|--------------------------|-------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PrintFax.Printer         | 0     | 表示任一打印机的打印队列连接到计算机 (通过本地或网络协议)，或为另一台计算机上的物理打印机的代理。 当用户打印到物理打印机时，则结果为在纸张上打印的文档的。                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| PrintFax.Fax             | 1     | 表示物理或虚拟传真机的打印队列。 当用户打印到传真打印机时，（可能是在后面进一步的用户交互） 的结果是发送传真。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| PrintFax.Printer.File    | 2     | 生成软复制文档打印队列。 当用户打印到文件打印机时，用户必须先输入一个文件名，并将后台处理程序然后将打印的输出发送到该文件。 文件打印机始终需要文件名称，但需要其他用户输入。 如果没有为用户提供一个文件名的选项，应用程序生成提供给后台处理程序的文件名。 文件的打印机的常见示例包括 Microsoft XPS 文档编写器 (MXDW) 和 PDF 的编写器。                                                                                                                                                                                                                                                 |
| PrintFax.Printer.Virtual | 3     | 执行某个操作上的驱动程序的打印队列打印对打印后台处理程序是不透明的数据。 当用户打印到的虚拟打印机时，一些可能的结果将包括打印的文档某处保存在计算机、 发送到另一个应用程序或通过电子邮件发送。 打印到的虚拟打印机，一个常见示例是其中打印的文档发送到 Microsoft Office OneNote 打印机的方案。 当用户选择要打印到的虚拟打印机时，可能有进一步的用户交互，启动驱动程序或某些其他驱动程序组件的需要。 有关详细信息，请参阅[打印机 INF 文件中的虚拟打印机](virtual-printers-in-printer-inf-files.md)。 |
| PrintFax.Printer.Service | 4     | 表示打印服务的打印队列。 当用户选择要打印到的服务时，然后 （可能是在后面进一步的用户交互） 结果将是第三方打印服务接收所打印的内容。 然后，用户可以转到要选取打印输出的实际业务位置。                                                                                                                                                                                                                                                                                                                                                                                                                            |
| PrintFax.Printer.3D      | 5     | 表示数据流 3D 打印机的打印队列。 如果无意中 2D 打印机 （正则打印机） 指定此类别，2D 打印机只需将输出 2D 流内容的数据。 如果此类别正确指定用于 3D 打印机，但 2D 数据流发送到 3D 打印机，3D 打印机将不生成任何输出。                                                                                                                                                                                                                                                                                                                                                                |

 

另请注意 v4 打印驱动程序使用的清单文件。 有关详细信息，请参阅[V4 驱动程序清单](v4-driver-manifest.md)。

 

**请注意**  **2 (ExcludeFromSelect)** :*设备 ID*的设备不会显示在**选择设备**对话框或添加打印机向导中。 对于打印机，这包括 INF 文件中; 中具有重复的设备描述的设备的所有即插即用条目例如，有多个条目红外和并行枚举或另一个总线的设备。 控制标志一部分 INF 文件中必须出现 ExcludeFromSelect 条目，与此表中的所有其他不同。 请参阅[ **INF ControlFlags 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)有关详细信息。

 

**请注意**  **3 (VendorSetup)** :如果指定没有 VendorSetup 条目，则不执行自定义安装程序操作。 具体而言，没有用户界面允许打印处理器、 打印监视器或打印机驱动程序安装在除通过 VendorSetup INF 条目使用。 有关此项的详细信息，请参阅[自定义的打印机安装程序操作](customized-printer-setup-operations.md)。

 

**重要**  :VendorSetup 现已弃用，不能由任何*新*v3 或 v4 驱动程序开发的。 仅或现有的 v3 驱动程序已使用此 INF 指令的维护的引用提供了有关 VendorSetup 此信息。

 

内通常指定打印机 INF 文件条目[打印机 INF 文件的数据部分](printer-inf-file-data-sections.md)。 有关示例，请参阅[示例打印机 INF 文件](sample-printer-inf-files.md)。

### <a href="" id="ddk-languagemonitor-value-format-gg"></a>LanguageMonitor 值格式

如果打印机 INF 文件中包含 LanguageMonitor 条目，则这些值的格式如下所示：

LanguageMonitor=" *MonitorName* , *MonitorDLLName* "

其中*MonitorName*是文本字符串，表示监视器的显示的名称，并*MonitorDLLName*是监视器 DLL 的文件名。

### <a href="" id="ddk-printprocessor-value-format-gg"></a>PrintProcessor 值格式

如果打印机 INF 文件中包含 PrintProcessor 条目，则这些值的格式如下所示：

PrintProcessor=" *PrintProcessorName* , *PrintProcessorDLLName* "

其中*PrintProcessorName*是文本字符串，表示打印处理器的显示的名称，并*PrintProcessorDLLName*是 DLL 的文件名。

### <a href="" id="ddk-dependent-files-gg"></a>依赖文件

Windows 2000 和更高版本，依赖文件是包含在打印机驱动程序文件[打印机 INF 文件安装部分](printer-inf-file-install-sections.md)与[dirid](printer-dirids.md) 66000，但未分配到 DriverFile，数据文件，ConfigFile或帮助文件条目。

下面的示例显示了部分内容摘自一个 INF 文件，通过将其复制到的打印机驱动程序目录 （即，为目录指定 dirid 66000） 安装三个相关文件：

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

在此示例中，Contoso.ini 是打印机 INI 文件、 Contoso.xml 是 bidi 扩展文件，和 Contoso.dll 是自定义的组件。 有关打印机 INI 文件、 bidi 扩展文件和自定义的组件的详细信息，请参阅[安装自定义驱动程序组件](installing-customized-driver-components.md)并[双向通信架构](bidirectional-communication-schema.md)。

[点--打印](introduction-to-point-and-print.md)操作安装的驱动程序和驱动程序相关的客户端上的文件。

可以为每个打印机型号指定最多为 64 依赖文件。

## <a name="related-topics"></a>相关主题
[双向通信架构](bidirectional-communication-schema.md)  
[**INF ControlFlags 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-controlflags-section)  
[安装自定义驱动程序组件](installing-customized-driver-components.md)  
[Point-and-print](introduction-to-point-and-print.md)  
[打印机 INF 文件安装部分](printer-inf-file-install-sections.md)  
[V4 驱动程序清单](v4-driver-manifest.md)  



