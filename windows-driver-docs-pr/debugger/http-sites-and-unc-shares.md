---
title: HTTP 站点和 UNC 共享
description: HTTP 站点和 UNC 共享
ms.assetid: a1b79242-41ba-4c95-89fd-dbb7f70b24eb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10446bc395970f4998593182340ea9b4089484da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567704"
---
# <a name="http-sites-and-unc-shares"></a>HTTP 站点和 UNC 共享


就可以设置使用 SrcSrv WinDbg 到提供特定于版本的源的网站。 这样一种机制并不提供从版本控制中的动态提取源代码文件，但它是有价值的功能，因为它允许您将 WinDbg 源路径设置为提供从多个版本的多个模块的源的单个统一路径而无需设置为每个调试方案不同的路径。 这不是调试客户端直接访问实际的版本控制系统，但可以帮助那些想提供安全的基于 HTTP 的访问，以从远程位置源为感兴趣。 如果需要，可以通过 HTTPS 和智能卡保护相关的网站。 这种方法可以用于提供通过简单的 UNC 共享的源文件。

本部分包括：

[设置 Web 站点](setting-up-the-web-site.md)

[解压缩源代码文件](extracting-source-files.md)

[修改源索引中的.pdb 文件的流](modifying-the-source-indexing-streams-in-a--pdb-file.md)

[使用 UNC 共享](using-unc-shares.md)

[使用 HTTP 站点和 UNC 共享中连同常规版本控制](using-http-sites-and-unc-shares-in-conjuction-with-regular-version-con.md)

 

 





