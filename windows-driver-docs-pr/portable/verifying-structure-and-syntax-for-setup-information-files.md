---
Description: 验证安装程序信息文件的结构和语法
title: 验证安装程序信息文件的结构和语法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b90b8eab6a30fa8cfe43b42bb955a769410c44ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370441"
---
# <a name="verifying-structure-and-syntax-for-setup-information-files"></a>验证安装程序信息文件的结构和语法


Windows Driver Kit (WDK) 提供了一组称为 ChkINF 工具的 Perl 脚本。 这些脚本验证结构和语法的安装程序信息 (.inf) 文件。 有关这些脚本的详细信息，请参阅 WDK 文档中的驱动程序开发工具部分。

所有 WPD.inf 文件必须都调用 UMDF 共同安装程序。 这意味着，每当声明共同安装程序部分， \[CopyFiles\]指令必须存在。 如果您的驱动程序不需要任何其他共同安装程序二进制文件 （并因此不需要 CopyFiles 指令），您可以通过声明一个空的 CopyFiles 部分并共同安装程序部分中引用它从满足要求。

 

 




