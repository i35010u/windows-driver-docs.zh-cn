---
title: 编译驱动程序的 MOF 文件
description: 编译驱动程序的 MOF 文件
ms.assetid: 0a4ab163-3e2c-48e9-9659-756d35ad445f
keywords:
- WMI WDK 内核，发布架构
- 发布 WMI 架构 WDK
- 架构发布 WDK WMI
- MOF 文件 WDK WMI
- 编译 MOF 文件
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0264ba541a23d46335eb95f8cf0eacaf9f421ef8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189837"
---
# <a name="compiling-a-drivers-mof-file"></a>编译驱动程序的 MOF 文件





若要编译定义 WMI 数据和事件块的 MOF 文件，请使用 Microsoft Windows 操作系统随附的 MOF 编译器（称为 Mofcomp.exe）。 使用以下语法：

```cpp
 mofcomp -WMI -B:filename.bmf filename.mof
```

以下各项显示在前面的语法中：

<a href="" id="-wmi"></a>**-WMI**  
验证 *filename* 中的所有类，以便与 WMI 一起使用。 如果任何类定义无效，Mofcomp.exe 会删除输出文件 *bmf*。 如果省略 **-WMI** ，则应在*Bmf*上运行[Wmimofck](using-wmimofck-exe.md)来验证类。 驱动程序必须使用 WMI 开关或运行 Wmimofck 来验证 MOF。 如果不这样做，可能会导致 MOF 文件未正确加载到 WMI 架构。

<a href="" id="-b-filename-bmf"></a>**-B：**<em>bmf</em>  
请求编译器在 *bmf* 中创建一个独立于平台的二进制版本的 MOF 文件，而不会对 CIMOM 对象存储库进行任何修改。

<a href="" id="filename-mof"></a>*filename。 mof*  
指定输入 MOF 文件的名称。

若要了解有关如何使用 Mofcomp.exe 的详细信息，请打开命令提示符窗口，然后键入 **mofcomp.exe/？**。

有关 Mofcomp.exe 的详细信息，请参阅 "Windows SDK 中的" [mofcomp.exe](https://go.microsoft.com/fwlink/p/?linkid=51316) "和其他主题。

若要将编译的 MOF 文件包含为驱动程序的二进制图像中的资源，请将以下行添加到驱动程序的资源脚本 (RC) 文件：

**MOFRESOURCE MOFDATA** *bmf*

驱动程序指定其 MOF 资源名称来响应注册请求 ([**IRP \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 或 [**irp \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) 请求 **，并将** 设置为数据路径) ：

-   如果驱动程序使用 WMI 库例程来处理 WMI Irp，它将在其 [*DpWmiQueryReginfo*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback) 例程中指定 MOF 资源名称。

-   如果驱动程序直接处理 WMI Irp，它将在 [**WMIREGINFO**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow) 结构中指定该驱动程序传递给 WMI 的 MOF 资源名称。

有关处理 **irp \_ MN \_ REGINFO** 和 **irp \_ MN \_ REGINFO \_ EX** 请求的详细信息，请参阅 [注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)。

有关使用 WMI iibrary 例程处理 WMI Irp 的详细信息，请参阅 [处理 Wmi 请求](handling-wmi-requests.md)。

有关在可执行文件中定义和包含资源的详细信息，请参阅 Microsoft Windows SDK。

 

