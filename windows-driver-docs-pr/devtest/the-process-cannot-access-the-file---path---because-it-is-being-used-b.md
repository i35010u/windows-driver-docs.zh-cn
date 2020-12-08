---
title: 进程无法访问文件路径，因为另一个进程正在使用该文件
description: 进程无法访问文件路径，因为另一个进程正在使用该文件路径。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce80d41aa6d408aaf27dbaa9e820523652d5b527
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817421"
---
# <a name="the-process-cannot-access-the-file-ltpathgt-because-it-is-being-used-by-another-process"></a>进程无法访问文件 " &lt; 路径 &gt; "，因为另一个进程正在使用该文件


当 SDV 尝试删除文件以响应 **staticdv/clean**、 **staticdv/clean/force** 或 **staticdv/cleanalllibs** 命令时，将显示此消息，但它无法访问文件，因为其他应用程序正在访问这些文件。 若要解决此问题，请关闭可能使用文件的所有应用程序，然后重新提交命令。

 

 





