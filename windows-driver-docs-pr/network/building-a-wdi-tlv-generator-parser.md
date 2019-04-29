---
title: 将 WDI TLV 生成器/分析器添加到驱动程序
description: 若要添加到您的驱动程序 WDI TLV 生成器/分析器，请执行以下步骤。
ms.assetid: 625FDE43-7A42-4840-9AFD-B8F5850F845E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c14b1dc89b3b7f9882b858d61f0c5fbe1aa8536
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367675"
---
# <a name="adding-the-wdi-tlv-generatorparser-to-your-driver"></a>将 WDI TLV 生成器/分析器添加到驱动程序


若要添加到您的驱动程序 WDI TLV 生成器/分析器，请执行以下步骤。

1.  添加这包括 dot11wdi.h 和 wditypes.hpp 之后。

    `#include "TlvGeneratorParser.hpp"`

2.  将此库添加到链接器。

    `TLVGeneratorParser.lib`

3.  定义、 创建和写入您的内存 Api （重载运算符新建/删除）。

4.  开始调用 Api。

 

 





