---
title: HTTP 站点和 UNC 共享
description: HTTP 站点和 UNC 共享
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94d1fbb67f8f39851bcc043d06d94039e757fffb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830757"
---
# <a name="http-sites-and-unc-shares"></a>HTTP 站点和 UNC 共享


可以使用 Srcsrv.ini 设置为 WinDbg 提供版本特定源的网站。 此类机制不会从版本控制中提供源文件的动态提取，但这是一项重要的功能，因为它允许您将 WinDbg 的源路径设置为提供多个模块的源的单个统一路径，而无需为每个调试方案设置单独的路径。 调试客户端对于直接访问实际版本控制系统并不需要这样做，但对于那些想要对远程位置中的源提供基于 HTTP 的安全访问权限的客户端，这并不是很感兴趣。 如果需要，可以通过 HTTPS 和智能卡保护相关网站。 这种方法可以通过简单的 UNC 共享来提供源文件。

本节包括：

[设置网站](setting-up-the-web-site.md)

[提取源文件](extracting-source-files.md)

[修改 .pdb 文件中的源索引流](modifying-the-source-indexing-streams-in-a--pdb-file.md)

[使用 UNC 共享](using-unc-shares.md)

[结合常规版本控制使用 HTTP 站点和 UNC 共享](using-http-sites-and-unc-shares-in-conjuction-with-regular-version-con.md)

 

 





