---
title: 显示的打印机详细信息页
description: 显示的打印机详细信息页
keywords:
- 自定义的打印网页 WDK，查看特定页面
- 查看打印机详细信息页
- 显示打印机详细信息页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 810c27c9dba97eb56ce7c8927ee128c592975166
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785805"
---
# <a name="which-printer-details-page-is-displayed"></a>显示哪个打印机详细信息页？





当用户尝试查看打印机的详细信息页时，服务器将使用以下算法来确定要读取的 ASP 文件。

-   如果打印机使用的是标准 TCP/IP 端口监视器，请执行以下操作：
    1.  服务器首先检查是否安装了一组特定于打印机类型的 ASP 文件。 如果是这样，将使用它们。
    2.  如果打印机类型特定的 ASP 文件不可用，则服务器将检查是否安装了一组特定于制造商的 ASP 文件。 如果是这样，将使用它们。
    3.  如果未提供制造商特定的 ASP 文件，并且打印机支持使用适用于 SNMP 的 (RFC 1759) ，则使用 Microsoft 的默认 ASP 文件。
    4.  如果不支持 SNMP，则不提供打印机详细信息页。
-   如果没有将标准 TCP/IP 端口监视器与打印机一起使用，则服务器将检查是否安装了一组特定于监视器的 ASP 文件。 如果是这样，将使用它们。 如果没有，则不提供打印机详细信息页。

有关详细信息，请参阅 [安装自定义的打印网页](installing-customized-print-web-pages.md)。

 

 




