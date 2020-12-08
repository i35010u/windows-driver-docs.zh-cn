---
title: XML 架构换行符转换
description: XML 架构换行符转换
keywords:
- linebreak 序列 WDK GDL
- GDL WDK，架构
- 架构 WDK GDL
- 快照 WDK GDL，换行符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24e667e6d416795a38330e47960fc335b004f3a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785753"
---
# <a name="xml-schema-linebreak-translations"></a>XML 架构换行符转换


XML 快照表示换行符，其中包含以下两个字符序列： &lt; 0d &gt; &lt; 0A &gt; (CR LF) 。 但是，在 &lt; CDATA &gt; 节中，带引号的字符串值和本机 XML 数据类型值，会完全使用在 GDL 源文件中找到的原始字符序列。 此使用情况可防止任何可能包含在 GDL 数据作者使用的 linebreak 序列中的信息丢失。

 

 




