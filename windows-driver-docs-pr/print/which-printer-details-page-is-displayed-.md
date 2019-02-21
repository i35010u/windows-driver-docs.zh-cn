---
title: 此时将显示哪些打印机的详细信息页
description: 此时将显示哪些打印机的详细信息页
ms.assetid: f7824350-a6de-45ca-8d72-859edf77e86d
keywords:
- 自定义打印网页 WDK，查看特定页
- 查看打印机的详细信息页
- 显示打印机的详细信息页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76ee8a17f7f05bff893d255ad4f4ef469f2d7791
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523083"
---
# <a name="which-printer-details-page-is-displayed"></a>将显示哪些打印机的详细信息页？





当用户尝试查看打印机的详细信息页上时，服务器将使用以下算法来确定要读取的 ASP 文件。

-   如果与打印机一起使用的标准 TCP/IP 端口监视器：
    1.  在服务器首先检查以查看是否已安装的打印机类型特定于 ASP 文件集。 如果是这样，它们用于。
    2.  如果打印机特定于类型的 ASP 文件不可用，服务器将检查以查看是否已安装的一组特定于制造商的 ASP 文件。 如果是这样，它们用于。
    3.  如果特定于制造商的 ASP 文件不可用，并且如果打印机支持 SNMP 打印机 MIB (RFC 1759)，则会使用 Microsoft 的默认 ASP 文件。
    4.  如果不支持 SNMP，未提供打印机详细信息页。
-   如果未随打印机一起使用的标准 TCP/IP 端口监视器，服务器将检查以查看是否安装了一组特定于监视器的 ASP 文件。 如果是这样，它们用于。 如果没有，未提供打印机详细信息页。

有关详细信息，请参阅[安装自定义打印网页](installing-customized-print-web-pages.md)。

 

 




