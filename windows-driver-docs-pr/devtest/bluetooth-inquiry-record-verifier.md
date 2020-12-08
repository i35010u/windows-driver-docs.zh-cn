---
title: 蓝牙查询记录验证程序
description: 当 Microsoft Windows 解释蓝牙设备的查询记录时，蓝牙查询记录验证器将显示该记录。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78a0a7537a5fc1a2e5cc47174d5194f47caac81c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793995"
---
# <a name="bluetooth-inquiry-record-verifier"></a>蓝牙查询记录验证程序


当 Microsoft Windows 解释蓝牙设备的查询记录时，蓝牙查询记录验证器将显示该记录。 此记录以树格式显示，其中显示了服务发现协议的记录以及获得的任何扩展的查询响应数据。

此工具不能替代蓝牙 SIG 的任何部分，也不能替代 Microsoft Windows 认证计划。 它在 Windows 驱动程序工具包中提供，可帮助你解决设备和 Microsoft Windows 之间的交互问题。

蓝牙查询记录验证程序具有三个菜单： "文件"、"广播" 和 "视图"。

使用 " **文件** " 菜单保存并打开查询记录和蓝牙配置文件：

-   若要保存当前的查询记录，请单击 " **文件 &gt; 导出**"。

-   若要打开已保存的查询记录，请单击 " **文件 &gt; 导入**"。

-   若要加载配置文件说明，请单击 "文件" " **&gt; 加载配置文件说明**"。 默认情况下，Microsoft 提供并加载12个常见配置文件的配置文件说明。

-   若要选择要加载的配置文件说明，请单击 " **管理配置文件说明**"。

使用 " **单选** 菜单" 显示所有可发现和配对的设备。

-   若要显示所有可发现和配对的设备，请单击 "广播"， **&gt; 并选择**。 选择一个设备以查看其查询记录。

-   若要在指定地址查询蓝牙广播，请单击 " **无线电 &gt; 输入地址**"，然后在 "选择蓝牙设备" 对话框中键入蓝牙 MAC 地址。
-   若要刷新当前显示的 SDP 记录，请单击 " **单选 &gt; Requery 当前收音机**"。

使用 " **视图** " 菜单可显示结果和查看错误。

-   若要以十六进制显示结果，请单击 " **查看 &gt; 原始结果**"。

-   若要以行属性 Id 的形式显示属性值，请单击 "以 **&gt; 同级方式查看属性值**"。

-   若要从错误跳转到错误，请单击 " **查看 &gt; 上一个错误** " 或 " **查看 &gt; 下一个错误**

## <a name="span-idknown_issues__windows_7_spanspan-idknown_issues__windows_7_spanspan-idknown_issues__windows_7_spanknown-issues-windows-7"></a><span id="Known_Issues__Windows_7_"></span><span id="known_issues__windows_7_"></span><span id="KNOWN_ISSUES__WINDOWS_7_"></span>Windows 7 (的已知问题) 


-   搜索远程设备时，在初始查询期间会列出找到的所有内容。 完成查询后，只能保留具有友好名称的设备。
-   扩展查询响应记录分析不起作用。
-   **LanguageBaseAttributeIDList** 可能标记为 "无效"。

 

 





