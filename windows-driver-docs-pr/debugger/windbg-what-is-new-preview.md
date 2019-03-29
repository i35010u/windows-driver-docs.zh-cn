---
title: WinDbg 预览版 - 新增功能
description: 本主题提供有关 WinDbg 预览调试器的新增 inofmration。
ms.date: 05/23/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 4cc2957dcd4ad25304c7dfa47e81425c9bd554aa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563976"
---
# <a name="windbg-preview---whats-new"></a>WinDbg 预览版 - 新增功能

本主题提供在 WinDbg 预览调试器中新增的信息。 

有关调试器版本的详细信息，请参阅调试器工具团队博客[ https://blogs.msdn.microsoft.com/windbg/ ](https://blogs.msdn.microsoft.com/windbg/)。


## <a name="10120"></a>1.0.12.0

此版本是 WinDbg Preview 的第一个版本。 有关一般信息在 WinDbg 预览版中提供的功能[调试使用 WinDbg 预览版](debugging-using-windbg-preview.md)。


## <a name="10130"></a>1.0.13.0

此版本添加了时间旅行跟踪。 时间旅行调试，使你可以记录过程中，然后更高版本同时向前和向后对其进行重播。 时间旅行调试 (TTD) 可帮助你调试问题更容易通过让你"后退"到调试器会话，而无需重现此问题，直到找到 bug。 有关详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。


## <a name="10140"></a>1.0.14.0

此版本包含这些更新。

- 启动调试页现在显示是否已连接到远程进程服务器 (DbgSrv) 并允许您从其断开连接。
- 查看功能区中的新预设的布局选项。
- 新时间旅行功能区时调试一次传输跟踪。
- 很多修补程序、 更新和更改 JSProvider api，请参阅完整的发行说明，有关详细信息。

已知问题
- SOS 不起在 x86 上的跟踪。


## <a name="11712150030"></a>1.1712.15003.0

此版本包含这些更新。

- 现在可以查询 TTD 跟踪中的内存
- 现在将在 WinDbg 预览会话之间保留设置
- 启动性能改进
- 附加 bug 修复程序

## <a name="10180418003"></a>1.0.1804.18003

此版本包含这些更新。

- 符号状态和取消改进
- 实验性说明窗口
- 实验性更快的源窗口
- JSProvider API 版本 1.2
- 细微的更改和 bug 修复


## <a name="10180517002"></a>1.0.1805.17002

此版本包含这些更新。

- 新反汇编窗口
- 更快的源窗口
- 细微的更改和 bug 修复

## <a name="10180711002"></a>1.0.1807.11002 

此版本包含这些更新。

- 自动保存和加载的断点
- 细微的更改和 bug 修复

## <a name="1018102001"></a>1.0.1810.2001 

此版本包含这些更新。

- 从文件菜单或在主页功能区访问的新设置对话框。 
- 事件和异常设置对话框
- 使用更好的性能改进的 TTD 索引器
- 新*debugArch*启动标记用于指定体系结构
- 细微的更改和 bug 修复

---
 
## <a name="see-also"></a>请参阅


[https://blogs.msdn.microsoft.com/windbg/](https://blogs.msdn.microsoft.com/windbg/)

[调试使用 WinDbg 预览](debugging-using-windbg-preview.md)
 





