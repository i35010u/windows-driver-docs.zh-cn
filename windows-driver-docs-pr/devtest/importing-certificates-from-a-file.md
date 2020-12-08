---
title: 从文件导入证书
description: 从文件导入证书
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baf76aab64f3654a0cea16480685d1ef50c6f96d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837323"
---
# <a name="importing-certificates-from-a-file"></a>从文件导入证书


你可以使用增强的存储证书管理工具从文件中导入证书。 文件必须包含以可辨别编码规则 (DER) 二进制格式编码的 x.509 证书。

可以使用以下方法之一创建此文件：

-   此证书可由符合 IEEE 1667 的 USB 存储设备中的增强型存储证书管理工具导出。 工具将证书保存在执行此工具时指定的文件中。

    有关详细信息，请参阅增强的存储证书管理工具的 [**/export 开关**](-export-switch.md) 。

-   可以使用 [**MakeCert**](makecert.md) 实用工具创建证书，并将其保存在文件中。

-   可以通过使用任何可生成以 DER 二进制格式编码的 x.509 证书的应用程序来创建证书。 然后，将证书保存到文件中。

有关如何将证书从文件导入到符合 IEEE 1667 的 USB 存储设备的详细信息，请参阅增强的存储证书管理工具的 [**/add**](enhstor-add-switch.md)和 [**/Replace**](-replace-switch.md)开关的 **-file** 参数。

 

 





