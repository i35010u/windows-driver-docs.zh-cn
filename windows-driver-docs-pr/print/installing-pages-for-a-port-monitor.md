---
title: 安装端口监视器的页面
description: 安装端口监视器的页面
ms.assetid: acb1a6f9-65d1-4097-b702-28dc4da8e4cf
keywords:
- 安装自定义打印网页 WDK
- 自定义打印网页 WDK，安装
- 端口监视 WDK 打印、 自定义 Web 页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9912601babe39bcdc84a5e0fe19010fe48f0a60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366570"
---
# <a name="installing-pages-for-a-port-monitor"></a>安装端口监视器的页面





用于不使用标准 TCP/IP 端口监视器的打印机，可以提供自定义的打印机的详细信息页。 将页面的 ASP 文件，以及所有从属文件 （如.gif 文件或链接的网页的 ASP 文件） 放入监视器的子目录 (&lt;根&gt;\\&lt;监视器&gt;，其中&lt;监视&gt;监视器名称返回为在端口中匹配\_信息\_2 结构; 有关详细信息，请参阅 Microsoft Windows SDK 文档)。 监视器的安装程序必须执行此任务。

页面的初始 ASP 文件必须命名为 Page1.asp。 所有 ASP 文件的名称格式为页*N*.asp，其中*N*是 1、 2、 3，依此类推，microsoft 保留。

 

 




