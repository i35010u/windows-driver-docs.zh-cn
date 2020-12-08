---
title: 安装制造商的页面
description: 安装制造商的页面
keywords:
- 安装自定义的打印网页 WDK
- 自定义的打印网页 WDK，安装
- 制造商特定的打印机安装 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a846dcfcaf5060d2354d33c6320f8d3b7024912d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796713"
---
# <a name="installing-pages-for-a-manufacturer"></a>安装制造商的页面





对于使用标准 TCP/IP 端口监视器的制造商的所有打印机类型，可以安装制造商特定的打印机详细信息页。 为此，请将页面的 ASP 文件以及所有从属文件（如 .gif 文件或) 的链接页的 ASP 文件） (为制造商的子目录 (\\ % windir% \\ web \\ 打印机 \\ &lt; 制造商 &gt;) 。 必须提供自定义的安装程序才能实现此目的。

页面的初始 ASP 文件必须命名为 Page1. .asp。 Microsoft 保留所有格式为 Page *n.*.ASP 的 asp 文件名，其中 *N* 为1、2、3等。

制造商特定的页面将用于使用标准 TCP/IP 端口监视器的制造商的所有打印机类型，并且没有特定于打印机类型的页面。

系统在安装时阅读打印机的 INF 文件，以确定打印机的制造商。 当用户尝试查看打印机详细信息页时，系统首先检查名为 Page1 的文件是否存在于 &lt; 根 &gt; \\ &lt; 制造商 &gt; \\ &lt; 打印机类型中 &gt; 。 如果找不到文件，则系统会检查 &lt; 根 &gt; \\ &lt; 制造商 &gt; 。

 

 




