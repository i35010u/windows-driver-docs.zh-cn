---
title: AVStream 测试和调试
description: AVStream 测试和调试
ms.assetid: 7a3eeeb5-1ff4-4110-9168-c716cd7776b8
keywords:
- 测试流媒体 AVStream WDK
- AVStream WDK 测试
- 调试 WDK AVStream
- AVStream WDK 调试
- AMCap2
- GraphEdt
- KsStudio 实用程序
- MCStream
- UVCView
- 活动的影片捕获 WDK AVStream
- AVStream WDK 工具
- 流式处理开发 Studio WDK AVStream 的内核
- 多渠道的流式处理工具 WDK AVStream
- USB 视频类描述符查看器 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6070f20dea1f73b5beafd05dba108cf5b3784b4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392722"
---
# <a name="avstream-testing-and-debugging"></a>AVStream 测试和调试


从 Windows 7 WDK 开始，三个工具中提供了*WDKPath\\工具\\avstream*文件夹层次结构。 本主题介绍的用途和每个工具的基本用法。 在某些情况下，文件夹层次结构中包含的其他文档。

### <a name="graphedt"></a>**GraphEdt**

*GraphEdt.exe*是开发工具，用于以可视方式构建功能多媒体筛选器关系图使用 DirectShow 应用程序编程接口。

GraphEdt 包括三个二进制组件：*GraphEdt.exe* （应用程序）， *GraphEdt.chm* （帮助文档），和*Proppage.dll* （帮助程序筛选器）。 *Proppage.dll*公开筛选器在中注册后使用命令"regsvr32 proppage.dll"的操作系统的其他属性设置。 必须在提升的权限级别运行 regsvr32 命令。

为基于 x86 和基于 x64 的体系结构提供了 GraphEdt 二进制文件。 GraphEdt 在 Microsoft Windows 2000、 XP、 Windows 2003 Server、 Windows Vista 和 Windows 7 上运行。

### <a name="ksstudio"></a>**KsStudio**

*KsStudio.exe* (内核流式处理 Development Studio) 是一种开发工具用于检查多媒体驱动程序属性，插针，且支持媒体。

Windows 7 WDK 包括 KsStudio 适用于基于 x86 和基于 x64 的体系结构的二进制文件。 此外，还有一个版本的 Windows XP 和 Windows 2003 Server XP 文件夹中 （适用于 x86 和 x64）。 适用于 Windows 7 二进制文件都*KsStudio.exe* （应用程序）， *KsStudio.chm* （帮助文档），并且*KsMon.sys* （帮助程序设备驱动程序）。 XP 和 Windows 2003 Server，还有 S*ndAnlyz.dll* （帮助程序文件）。

KsStudio 内核的开发工具，因此应谨慎使用。 *KsStudio.exe*必须将摘要日志写入到的开始目录，其必须具有写访问权限的用户。 尝试加载其帮助程序的驱动程序 KsStudio *KsMon.sys*。 这种加载是可选的才会成功*KsMon.sys*位于启动目录中，在提升的权限级别运行命令。 通常情况下，KsStudio 会显示一个名为"KS Studio 筛选器选项"允许用户指定参数，其中最重要的是要枚举的类对话框。 使用**类**any，选择无，该对话框或所有类上的按钮。

这是一个复杂，但简洁且非常方便的开发工具，多媒体设备作者。 有关详细信息，请参阅*KsStudio.chm*帮助文件。

### <a href="" id="uvcview"></a>**USBView**

*USBView.exe* （USB 视频类描述符查看器） 是一个开发工具，使用户可以检查任何附加的 USB 设备上的描述符。 USBView 作为 USB 部分中的示例提供 Windows Driver Kit (WDK) 中。 USBView 添加多媒体 USB 音频和视频类设备的描述性描述符信息。

**请注意**  Windows 7 WDK 中，此工具的标题为 UVCView。

 

USBView 包括一个二进制组件：*USBView.exe*。 WDK 中，在此可执行文件位于*工具\\avstream*文件夹层次结构。 文档，请参阅中的 USBView 示例*WDKPath\\src\\usb\\usbview*。

为基于 x86 和基于 x64 的体系结构提供了 USBView 二进制文件。 USBView 在 Microsoft Windows 2000、 XP、 Windows 2003 Server、 Windows Vista 和 Windows 7 上运行。

以下工具的 Windows 的早期版本中提供，并不建议用于 Windows 7 及更高版本：

### <a name="amcap2"></a>**AMCap2**

*AMCap2.exe* （Active 电影捕获） 是枚举和使用 Microsoft DirectShow 应用程序编程接口使用音频和视频捕获设备的应用程序。

AMCap2 包括一个二进制组件：*AMCap2.exe*。

为基于 x86 和基于 x64 的体系结构提供了 AMCap2 二进制文件。 AMCap2 在 Microsoft Windows 2000、 XP、 Windows 2003 服务器和 Vista 上运行。

AMCap2 初始化时，它枚举可用音频和视频捕获设备在其设备菜单。 您可以选择无或 1 个音频和/或视频设备。 在设置菜单中，可以选择特定的设备属性。

DirectShow，有关详细信息[DirectShow 文档](https://go.microsoft.com/fwlink/p/?linkid=68207)。

*AMCap2.exe*工具将显示在 Windows Server 2008 WDK 和早期版本的 WDK 中。 该工具已从基于 x86 和基于 x64 的平台的 Windows 7 WDK 中删除。

AMCap2 的所有功能都都在 Windows 7 WDK 中包含的现有 GraphEdt 工具中仍然可用。

### <a name="mcstream"></a>**MCStream**

*MCStream.exe* （多通道流式处理工具） 是一个开发工具，允许用户生成并呈现批拨号音的多个通道。 MCStream 是直接使用 KS，而不是 DirectShow 或媒体基础的较旧工具。

**警告**  MCStream 并不适用于所有音频的呈现器。

 

MCStream 包括两个二进制组件：*MCStream.exe* （应用程序） 和*MCStream.txt* （帮助文档）。

为基于 x86 和基于 x64 的体系结构提供了 MCStream 二进制文件。 MCStream 在 Microsoft Windows 2000、 XP、 Windows 2003 服务器和 Vista 上运行。

*MCstream.exe*工具不包含在 Windows 7 WDK 的基于 x86 和基于 x64 的平台中。

此工具使用传统技术，不再建议使用 Windows 7 和更高版本操作系统中的驱动程序开发。

 

 




