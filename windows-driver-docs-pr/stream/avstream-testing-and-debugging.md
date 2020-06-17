---
title: AVStream 测试和调试
description: AVStream 测试和调试
ms.assetid: 7a3eeeb5-1ff4-4110-9168-c716cd7776b8
keywords:
- 测试 AVStream WDK 流式处理媒体
- AVStream WDK，测试
- 调试 WDK AVStream
- AVStream WDK，调试
- AMCap2
- GraphEdt
- KsStudio 实用程序
- MCStream
- UVCView
- 活动电影捕获 WDK AVStream
- AVStream WDK，工具
- 内核流式处理开发工作室 WDK AVStream
- 多通道流工具 WDK AVStream
- USB 视频类描述符查看器 WDK AVStream
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4e71b904557b117ec73cfa96153803a7751c28b8
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812436"
---
# <a name="avstream-testing-and-debugging"></a>AVStream 测试和调试

从 Windows 7 WDK 开始， *WDKPath \\ tools \\ avstream*文件夹层次结构中提供了三种工具。 本主题说明每个工具的用途和基本用法。 在某些情况下，附加文档包含在文件夹层次结构中。

## <a name="graphedt"></a>GraphEdt

*GraphEdt.exe*是一种开发工具，用于以可视方式使用 DirectShow 应用程序编程接口来构建功能多媒体筛选器图形。

GraphEdt 包括三个二进制组件： *GraphEdt.exe* （应用程序）、 *GraphEdt* （帮助文档）和*Proppage.dll* （helper 筛选器）。 当使用命令 "regsvr32 proppage.dll" 向操作系统注册时， *Proppage.dll*会公开筛选器的其他属性设置。 Regsvr32 命令必须以提升的特权级别运行。

GraphEdt 二进制文件是针对基于 x86 和基于 x64 的体系结构而提供的。 GraphEdt 在 Microsoft Windows 2000、XP、Windows 2003 Server、Windows Vista 和 Windows 7 上运行。

## <a name="ksstudio"></a>KsStudio

*KsStudio.exe* （内核流式处理开发工作室）是一个用于检查多媒体驱动程序属性、pin 和支持的媒体的开发工具。

Windows 7 WDK 包含基于 x86 和基于 x64 的体系结构的 KsStudio 二进制文件。 此外，XP 文件夹中的 Windows XP 和 Windows 2003 服务器的版本（适用于 x86 和 x64）。 对于 Windows 7，二进制文件*KsStudio.exe* （应用程序）、 *KsStudio* （帮助文档）和*KsMon.sys* （帮助器设备驱动程序）。 对于 XP 和 Windows 2003 服务器，还提供了 S*ndAnlyz.dll* （helper 文件）。

KsStudio 是一种内核开发工具，因此应该谨慎使用。 *KsStudio.exe*必须将摘要日志写入到必须对用户具有写入权限的起始目录。 KsStudio 尝试加载其 helper 驱动程序*KsMon.sys*。 此加载是可选的，并且只有在*KsMon.sys*位于起始目录中并且命令以提升的特权级别运行时，才会成功。 通常，KsStudio 会显示一个标题为 "KS Studio 筛选器选项" 的对话框，该对话框允许用户指定参数，其中最重要的参数是要枚举的类。 使用该对话框中的 "**类**" 按钮，可以选择 "无"、"任何" 或 "所有" 类。

对于多媒体设备创作者来说，这是一个复杂而又精致且非常便利的开发工具。 有关详细信息，请参阅*KsStudio*帮助文件。

## <a name="usbview"></a>USBView

*USBView.exe* （USB 视频类描述符查看器）是一个开发工具，它允许用户在任何连接的 USB 设备上检查描述符。 USBView 在 Windows 驱动程序工具包（WDK）中随附，作为 USB 部分中的示例。 USBView 为多媒体 USB 音频和视频类设备添加描述性描述符信息。

> [!NOTE]
> 在 Windows 7 WDK 中，此工具的标题为 "UVCView"。

USBView 包括一个二进制组件： *USBView.exe*。 在 WDK 中，此可执行文件位于*tools \\ avstream*文件夹层次结构中。 有关文档，请参阅*WDKPath \\ src \\ usb \\ USBView*中的 USBView 示例。

USBView 二进制文件是针对基于 x86 和基于 x64 的体系结构而提供的。 USBView 在 Microsoft Windows 2000、XP、Windows 2003 Server、Windows Vista 和 Windows 7 上运行。

以下工具在 Windows 的早期版本中提供，不建议在 Windows 7 和更高版本中使用：

## <a name="amcap2"></a>AMCap2

*AMCap2.exe* （活动电影捕获）是一个应用程序，用于通过 Microsoft DirectShow 应用程序编程接口枚举和使用音频和视频捕获设备。

AMCap2 包括一个二进制组件： *AMCap2.exe*。

AMCap2 二进制文件是针对基于 x86 和基于 x64 的体系结构而提供的。 AMCap2 在 Microsoft Windows 2000、XP、Windows 2003 服务器和 Vista 上运行。

当 AMCap2 初始化时，它会枚举其设备菜单上可用的音频和视频捕获设备。 您可以选择 "无" 或一个音频和/或视频设备。 在 "设置" 菜单上，可以选择特定设备属性。

有关详细信息，请参阅[DirectShow 文档](https://docs.microsoft.com/previous-versions//ms783323(v=vs.85))。

*AMCap2.exe*工具显示在 Windows SERVER 2008 wdk 和更早版本的 wdk 中。 对于基于 x86 和基于 x64 的平台，该工具已从 Windows 7 WDK 中删除。

AMCap2 的所有功能在现有的 GraphEdt 工具中仍可用，该工具包含在 Windows 7 WDK 中。

## <a name="mcstream"></a>MCStream

*MCStream.exe* （多通道流工具）是一种开发工具，它允许用户生成和呈现多个频道波形音。 MCStream 是一个较旧的工具，它直接使用 KS，而不是 DirectShow 或媒体基础。

> [!WARNING]
> MCStream 不适用于所有音频呈现器。

MCStream 包括两个二进制组件： *MCStream.exe* （应用程序）和*MCStream.txt* （帮助文档）。

MCStream 二进制文件是针对基于 x86 和基于 x64 的体系结构而提供的。 MCStream 在 Microsoft Windows 2000、XP、Windows 2003 服务器和 Vista 上运行。

对于基于 x86 和基于 x64 的平台，Windows 7 WDK 中不包含*MCstream.exe*工具。

此工具使用的是 Windows 7 及更高版本操作系统中的驱动程序开发不再推荐使用的旧技术。
