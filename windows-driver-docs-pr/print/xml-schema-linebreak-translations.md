---
title: XML 架构换行符转换
description: XML 架构换行符转换
ms.assetid: c277984f-8e7a-4d17-98ab-66c3f6f80473
keywords:
- linebreak 序列 WDK GDL
- GDL WDK 架构
- 架构 WDK GDL
- 快照 WDK GDL，换行符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a7261ee2e7633f55fbfb286b81db1bc1c52ae45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390245"
---
# <a name="xml-schema-linebreak-translations"></a>XML 架构换行符转换


XML 快照表示换行符与以下两个字符序列：&lt;0d&gt;&lt;0a&gt; (CR LF)。 但是，在&lt;CDATA&gt;完全使用部分中，带引号的字符串值和本机 XML 数据类型值，GDL 源代码文件中的原始字符序列。 这种用法可以防止丢失任何可能包含在所选的 linebreak GDL 数据的作者使用的序列的信息。

 

 




