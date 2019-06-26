---
title: 编译驱动程序 MOF 文件
description: 编译驱动程序 MOF 文件
ms.assetid: 0a4ab163-3e2c-48e9-9659-756d35ad445f
keywords:
- WMI WDK 内核，发布架构
- 发布 WMI 架构 WDK
- 发布 WDK WMI 架构
- MOF 文件 WDK WMI
- 编译 MOF 文件
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03d163be6616e0d03ab665dafce2faa3b5184f3f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383332"
---
# <a name="compiling-a-drivers-mof-file"></a>编译驱动程序 MOF 文件





若要编译定义 WMI 数据和事件块的 MOF 文件，请使用 MOF 编译器，调用 Mofcomp，即包含与 Microsoft Windows 操作系统。 使用以下语法：

```cpp
 mofcomp -WMI -B:filename.bmf filename.mof
```

在前面的语法中显示以下项：

<a href="" id="-wmi"></a> **-WMI**  
验证中的所有类*filename.mof*与 WMI 一起使用。 如果任何类定义无效，Mofcomp 删除输出文件*filename.bmf*。 如果 **-WMI**是省略，则应运行[Wmimofck](using-wmimofck-exe.md)上*filename.bmf*验证类。 驱动程序必须使用 WMI 开关或运行 Wmimofck 验证 MOF。 如果不这样做可能导致到 WMI 架构不能正确加载 MOF 文件。

<a href="" id="-b-filename-bmf"></a> **-B:** <em>filename.bmf</em>  
请求编译器创建的 MOF 文件中的独立于平台的二进制版本*filename.bmf*而无需对 CIMOM 对象储存库进行任何修改。

<a href="" id="filename-mof"></a>*filename.mof*  
指定输入的 MOF 文件的名称。

若要了解有关如何使用 Mofcomp 的详细信息，请打开命令提示符窗口并键入**mofcomp /？** 。

Mofcomp 有关详细信息，请参阅[MofComp](https://go.microsoft.com/fwlink/p/?linkid=51316)和 Windows SDK 中的其他主题。

若要为驱动程序的二进制映像中的资源包含已编译的 MOF 文件，请将以下行添加到驱动程序的资源脚本 (RC) 文件：

**MofResource MOFDATA** *filename.bmf*

驱动程序的注册请求的响应中指定其 MOF 资源名称 ( [ **IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)或者[ **IRP\_MN\_REGINFO\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)请求**Parameters.WMI.DataPath**设置为 WMIREGISTER):

-   如果该驱动程序使用 WMI 库例程来处理 WMI Irp，它指定 MOF 资源名称在其[ *DpWmiQueryReginfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_reginfo_callback)例程。

-   如果该驱动程序直接处理 WMI Irp，它指定在 MOF 资源名称[ **WMIREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmireginfow)驱动程序将传递给 WMI 的结构。

有关处理的详细信息**IRP\_MN\_REGINFO**并**IRP\_MN\_REGINFO\_EX**请求，请参阅[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)。

有关处理 WMI Irp 使用 WMI iibrary 例程的详细信息，请参阅[处理 WMI 请求](handling-wmi-requests.md)。

有关定义和可执行文件中包括的资源的详细信息，请参阅 Microsoft Windows SDK。

 

 




