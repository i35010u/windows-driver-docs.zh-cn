---
title: 为 SymProxy 配置 IIS
description: 为 SymProxy 配置 IIS
keywords:
- SymProxy、IIS
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b731ca9254e17e31eff213e1300ef6f485e7dd9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788841"
---
# <a name="configuring-iis-for-symproxy"></a>为 SymProxy 配置 IIS


 (IIS) Internet Information Services 必须配置为使用 SymProxy 作为 Internet 服务器应用程序编程接口 (ISAPI) 筛选器。 此外，必须设置权限以使 IIS 能够获取符号。

**配置应用程序池**

1.  从 " **管理工具** " **Internet Information Services (IIS) 管理器** 打开。

2.  展开带有左侧计算机名称的条目，并找到 " **应用程序池**"。

3.  右键单击 " **应用程序池** "，然后选择 " **添加应用程序池**"。

4.  对于 " **名称** "，请键入 *SymProxy 应用池*。

5.  " **.Net Framework 版本**" 下选择 "*无*"

6.  单击 **"确定"** 以创建应用程序池。

7.  接下来，右键单击新应用程序池的条目，然后选择 " **高级设置 ...**"。

8.  在 " **处理模型**" 下，将看到 " **标识**"。 单击标记为 "**...**" 的按钮。

    1.  如果作为网络服务进行身份验证，请选择 "为 **应用程序池标识****预定义**"，然后选择 "**网络服务**"。

    2.  如果以域用户身份进行身份验证，请选择 " **自定义帐户** "，然后单击 " **设置** " 按钮。 键入有权访问远程符号服务器存储的帐户的凭据 (例如， *corp \\ SymProxyUser*) ，然后单击 **"确定"**。

9.  单击 **"确定"** 退出 " **应用程序池标识** " 对话框。

10. 单击 **"确定"** 退出 " **高级设置** " 对话框。

**设置虚拟目录**

1.  展开 **"网站"**。

2.  选择 " **默认** 网站"。

3.  右键单击 **符号** 虚拟目录，然后选择 " **属性**"。

4.  在 " **虚拟目录** " 选项卡中，单击 " **创建**"。

5.  从 " **应用程序池** " 下拉菜单中，选择 " **SymProxy 应用程序池**"。

6.  若要退出 **符号属性**，请单击 **"确定"**。

**配置 ISAPI 筛选器**

1.  右键单击 " **默认** 网站"，然后选择 " **属性**"。

2.  双击 " **ISAPI 筛选器**"。

3.  右键单击列名下面的中心窗格， **然后选择** " **添加**"。

4.  对于 **筛选器名称** 类型 **SymProxy** 或其他有意义的名称。

5.  对于 **可执行文件** 类型 *c： \\ windows \\ system32 \\ inetsrv \\symproxy.dll*。

6.  若要退出 " **筛选器属性** " 对话框，请单击 **"确定"**。

7.  若要退出 **默认网站属性，请** 单击 **"确定"**。

 

 





