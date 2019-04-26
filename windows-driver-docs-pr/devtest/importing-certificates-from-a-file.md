---
title: 从文件导入证书
description: 从文件导入证书
ms.assetid: 17596119-6b31-4a69-b83c-cec1dfd55572
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c565d3e753cc44abdc7af9879411a89295007aa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330633"
---
# <a name="importing-certificates-from-a-file"></a>从文件导入证书


增强型存储证书管理工具可用于从文件导入证书。 该文件必须包含以可分辨编码规则 (DER) 二进制格式进行编码的 X.509 证书。

可以使用以下方法之一来创建此文件：

-   可以通过 IEEE 1667 合规 USB 存储设备中的增强型存储证书管理工具中导出证书。 该工具将证书保存在执行该工具时指定的文件中。

    有关详细信息，请参阅[ **/Export 开关**](-export-switch.md)的增强型存储证书管理工具。

-   可以使用创建证书[ **MakeCert** ](makecert.md)实用程序，并已保存的文件中。

-   可以使用任何应用程序都可以生成 DER 二进制格式进行编码的 X.509 证书创建证书。 然后，证书将保存在文件中。

有关如何将证书从文件导入 IEEE 1667 合规 USB 存储设备的详细信息，请参阅**的文件**的参数[ **/add** ](enhstor-add-switch.md)和[ **/替换**](-replace-switch.md)增强存储证书管理工具的开关。

 

 





