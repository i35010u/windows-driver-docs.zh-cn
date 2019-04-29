---
title: 安装制造商的页面
description: 安装制造商的页面
ms.assetid: 637b265f-9138-4696-b52a-ce63cd1f2c01
keywords:
- 安装自定义打印网页 WDK
- 自定义打印网页 WDK，安装
- 制造商特定于打印机安装 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41b4b9ef2c8eac102fefef5b8530e60005aadd69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366573"
---
# <a name="installing-pages-for-a-manufacturer"></a>安装制造商的页面





你可以安装打印机详细信息页面制造商指定，使用标准 TCP/IP 端口监视器的制造商的打印机类型。 为此，请将页面的 ASP 文件，以及 （如.gif 文件或链接的网页的 ASP 文件） 的所有从属文件放入制造商的子目录 (\\%windir%\\web\\打印机\\&lt;制造商&gt;)。 必须提供自定义的安装程序来实现此目的。

页面的初始 ASP 文件必须命名为 Page1.asp。 所有 ASP 文件的名称格式为页*N*.asp，其中*N*是 1、 2、 3，依此类推，microsoft 保留。

制造商特定的页上将用于所有制造商的打印机类型，使用标准 TCP/IP 端口监视器，但没有打印机特定于类型的页。

系统通过在安装时读取打印机的 INF 文件来确定打印机的制造商。 当用户尝试查看打印机的详细信息页上时，系统首先检查名为 Page1.asp 的文件是否存在于&lt;根&gt;\\&lt;制造商&gt;\\&lt;打印机类型&gt;。 如果找不到一个文件，系统会检查&lt;根&gt;\\&lt;制造商&gt;。

 

 




