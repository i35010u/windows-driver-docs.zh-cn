---
title: 蓝牙查询记录验证程序
description: 蓝牙查询记录验证工具显示蓝牙设备的查询记录，如 Microsoft Windows 将其解释。
ms.assetid: 3C48EEBA-3407-4A4A-91C2-EF001EFCDA6E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e1e90598ef52716cc164e6dedf01469366242cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577265"
---
# <a name="bluetooth-inquiry-record-verifier"></a>蓝牙查询记录验证程序


蓝牙查询记录验证工具显示蓝牙设备的查询记录，如 Microsoft Windows 将其解释。 此记录中显示服务发现协议的记录和获得的任何扩展查询响应数据的树格式显示。

此工具不能替代蓝牙 SIG 资格认证过程的任何部分或 Microsoft Windows 认证计划。 它提供 Windows 驱动程序工具包可帮助你解决设备和 Microsoft Windows 之间的交互。

蓝牙查询记录验证器有三个菜单：文件、 单选和视图。

使用**文件**菜单可保存和打开查询记录和蓝牙配置文件：

-   若要保存当前查询记录，请单击**文件&gt;导出**。

-   若要打开已保存的查询记录，请单击**文件&gt;导入**。

-   若要加载的配置文件说明，请单击**文件&gt;加载配置文件描述**。 默认情况下，Microsoft 提供并加载 12 公共配置文件的配置文件说明。

-   若要选择要加载哪个配置文件说明，请单击**管理配置文件说明**。

使用**单选**菜单可显示所有可发现和配对设备。

-   若要显示所有可发现和配对设备，请单击**单选&gt;查询和选择**。 选择要查看其查询记录的设备。

-   若要查询指定地址处蓝牙无线功能，请单击**单选&gt;输入地址**，并在选择 Bluetooth 设备对话框中键入蓝牙 MAC 地址。
-   若要刷新当前显示的 SDP 条记录，请单击**单选&gt;再次查询当前单选**。

使用**视图**菜单以显示结果并查看错误。

-   若要以十六进制格式显示结果，请单击**视图&gt;原始结果**。

-   若要显示其属性 Id 根据属性值，请单击**视图&gt;属性值为同级**。

-   若要跳转错误到错误，请单击**视图&gt;以前的错误**或**视图&gt;下一个错误**

## <a name="span-idknownissueswindows7spanspan-idknownissueswindows7spanspan-idknownissueswindows7spanknown-issues-windows-7"></a><span id="Known_Issues__Windows_7_"></span><span id="known_issues__windows_7_"></span><span id="KNOWN_ISSUES__WINDOWS_7_"></span>已知的问题 (Windows 7)


-   搜索针对远程设备上找到的所有任务会列出在初始查询过程。 查询完成后，我们具有一个友好名称的设备将保留。
-   扩展查询响应记录分析不起作用。
-   **LanguageBaseAttributeIDList**可能被错误地为无效标记。

 

 





