---
title: 安装端口监视器的页面
description: 安装端口监视器的页面
keywords:
- 安装自定义的打印网页 WDK
- 自定义的打印网页 WDK，安装
- 端口监视 WDK 打印，自定义网页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24254f565a44f43debe2b0da79179bce864f6edd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835653"
---
# <a name="installing-pages-for-a-port-monitor"></a>安装端口监视器的页面





你可以提供自定义的打印机详细信息页，以便与不使用标准 TCP/IP 端口监视器的打印机一起使用。 将页面的 ASP 文件以及所有从属文件 (如) 的链接页的 .gif 文件或 ASP 文件）放置在监视器子目录 (&lt; 根 &gt; \\ &lt; 监视器中 &gt; ，其中的 &lt; 监视器 &gt; 与端口信息2结构中返回的监视器名称匹配 \_ \_ ; 有关详细信息，请参阅 Microsoft Windows SDK 文档) 。 监视器的安装程序必须执行此任务。

页面的初始 ASP 文件必须命名为 Page1. .asp。 Microsoft 保留所有格式为 Page *n.*.ASP 的 asp 文件名，其中 *N* 为1、2、3等。

 

 




