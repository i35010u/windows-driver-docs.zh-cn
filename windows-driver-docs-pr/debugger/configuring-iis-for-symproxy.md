---
title: 为 SymProxy 配置 IIS
description: 为 SymProxy 配置 IIS
keywords:
- SymProxy、IIS
ms.date: 04/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: e749763ab92eb3d6c2480546ace798b6c06840cc
ms.sourcegitcommit: 119a8f0435127a41cd215063200f67cd6eb51ed1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218279"
---
# <a name="configuring-iis-for-symproxy"></a>为 SymProxy 配置 IIS

 (IIS) Internet Information Services 必须配置为使用 SymProxy 作为 Internet 服务器应用程序编程接口 (ISAPI) 筛选器。 此外，必须设置权限以使 IIS 能够获取符号。

有关自动执行此过程的信息和设置的摘要，请参阅 [SymProxy 自动安装](symproxy-automated-installation.md)。

确认示例安全设置适用于你的环境，并进行修改以遵守特定于你的组织的任何其他安全要求。

根据所运行的 IIS 的特定版本，配置选项将有所不同。 有关 IIS 的详细信息，请参阅 [Iis Web 服务器概述](/iis/get-started/introduction-to-iis/iis-web-server-overview)。

**配置应用程序池**

1.  打开“Internet Information Services (IIS)管理器” 。

2.  展开带有左侧计算机名称的条目，并找到 " **应用程序池**"。

3.  右键单击 " **应用程序池** "，然后选择 " **添加应用程序池**"。

4.  对于 " **名称** "，请键入 *SymProxy 应用池*。

5.  在 **.NET CLR 版本** 下，选择 "*无托管代码*"

6.  单击 **"确定"** 以创建应用程序池。

7.  接下来，右键单击新应用程序池的条目，然后选择 " **高级设置 ...**"。

8.  在 " **处理模型**" 下，将看到 " **标识**"。 单击标记为 "**...**" 的按钮。

    1.  如果作为网络服务进行身份验证，请选择 "**应用程序池标识** 的 **内置帐户**"，然后选择 "**网络服务**"，并单击 **"确定"**。

    2.  如果以域用户身份进行身份验证，请选择 " **自定义帐户** "，然后单击 " **设置** " 按钮。 键入有权访问远程符号服务器存储的帐户的凭据 (例如， *corp \\ SymProxyUser*) ，然后单击 **"确定"**。

9.  单击 **"确定"** 退出 " **应用程序池标识** " 对话框。

10. 单击 **"确定"** 退出 " **高级设置** " 对话框。

**示例虚拟目录配置**

1.  展开 " **站点**"。

2.  右键单击 "**默认** 网站"，然后选择 "**添加虚拟目录**"

3.  使用名称（如 **符号** ），并将其映射到所选位置。

3.  右键单击已创建的 " **符号** " 虚拟目录，然后选择 " **添加应用程序**"。

5.  从 " **应用程序池** " 下拉菜单中，选择 " **SymProxy 应用池** "，然后单击 **"确定"**。

**配置 ISAPI 筛选器**

1. 确认在 IIS 中安装了 ISAPI 选项。

2.  单击 " **默认** 网站"。

3.  双击 " **ISAPI 筛选器**"。

4.  右键单击列名下面的中心窗格， **然后选择** " **添加**"。

5.  对于 **筛选器名称** 类型 **SymProxy** 或其他有意义的名称。

6.  对于 **可执行文件** 类型 *c： \\ windows \\ system32 \\ inetsrv \\symproxy.dll*。

7.  若要退出 " **筛选器属性** " 对话框，请单击 **"确定"**。

8.  若要退出 **默认网站属性，请** 单击 **"确定"**。

**配置 MIME 类型和其他配置** 

所需步骤是 IIS 符号服务器和 symproxy 配置的一部分。 请参阅这些主题，了解有关配置 MIME 类型的信息，以及有关其他注意事项的信息。

[HTTP 符号存储](http-symbol-stores.md)

[缓存获取的符号文件](caching-acquired-symbol-files.md)

[SymProxy 自动安装](symproxy-automated-installation.md)
