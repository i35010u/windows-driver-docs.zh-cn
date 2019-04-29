---
title: 为 SymProxy 配置 IIS
description: 为 SymProxy 配置 IIS
ms.assetid: 66f1d05c-2572-4dda-a9d9-766561ebd491
keywords:
- SymProxy, IIS
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53281f8f0193a019e6158966b851be4b799fd7d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375051"
---
# <a name="configuring-iis-for-symproxy"></a>为 SymProxy 配置 IIS


必须配置 Internet 信息服务 (IIS) 为 SymProxy 用作 Internet 服务器应用程序编程接口 (ISAPI) 筛选器。 此外，必须设置权限，以便 IIS 可以获取符号。

**若要配置的应用程序池**

1.  从**管理工具**打开**Internet Information Services (IIS) Manager**。

2.  展开左侧的计算机名称的项并找到**应用程序池**。

3.  右键单击**应用程序池**，然后选择**添加应用程序池**。

4.  有关**名称**类型*SymProxy 应用池*。

5.  下 **.Net Framework 版本**选择*None*

6.  单击**确定**创建应用程序池。

7.  接下来，右键单击新的应用程序池的条目，然后选择**高级设置...**.

8.  下**过程模型**，你将看到**标识**。 单击右侧按钮标记为"**...**".

    1.  如果进行身份验证作为网络服务，请选择**预定义**有关**应用程序池标识**，然后选择**网络服务**。

    2.  如果进行身份验证以作为域用户，请选择**自定义帐户**，然后单击**设置**按钮。 键入有权访问远程符号服务器存储区的帐户的凭据 (例如， *corp\\SymProxyUser*)，然后单击**确定**。

9.  单击**确定**退出**应用程序池标识**对话框。

10. 单击**确定**退出**高级设置**对话框。

**若要设置虚拟目录**

1.  展开**网站**。

2.  选择**默认网站**。

3.  右键单击**符号**虚拟目录，然后选择**属性**。

4.  在中**虚拟目录**选项卡上，单击**创建**。

5.  从**应用程序池**下拉列表菜单中，选择**SymProxy 应用池**。

6.  若要退出**符号属性**，单击**确定**。

**配置 ISAPI 筛选器**

1.  右键单击**Default Web Site** ，然后选择**属性**。

2.  双击**ISAPI 筛选器**。

3.  右键单击列下的中心窗格**名称**单击，然后选择**添加**。

4.  有关**筛选器名称**类型**SymProxy**或某些其他有意义的名称。

5.  有关**可执行文件**类型*c:\\windows\\system32\\inetsrv\\symproxy.dll*。

6.  若要退出**筛选器属性**对话框中，单击**确定**。

7.  若要退出**默认网站属性**单击**确定**。

 

 





