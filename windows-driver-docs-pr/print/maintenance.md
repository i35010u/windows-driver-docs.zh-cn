---
title: 维护
description: 维护
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15af177d2161137f477911f02dac936342572c53
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807899"
---
# <a name="maintenance"></a>维护


架构路径： \\ 打印机。维护

节点类型：属性

维护属性包含有关打印设备维护的信息。

维护属性包含两个子值： **AlignHead** 和 **CleanHead**。

### <a name="span-idalignheadspanspan-idalignheadspan-alignhead"></a><span id="alignhead"></span><span id="ALIGNHEAD"></span> AlignHead

架构路径： \\ AlignHead

节点类型：值

数据类型：双向 \_ BOOL

说明：此值表示在设备上执行头对齐过程的命令。 此值为只写值。 尝试读取此值应被拒绝。 如果该值设置为1，则设备应执行命令。

### <a name="span-idcleanheadspanspan-idcleanheadspan-cleanhead"></a><span id="cleanhead"></span><span id="CLEANHEAD"></span> CleanHead

架构路径： \\ CleanHead

节点类型：值

数据类型：双向 \_ BOOL

说明：此值表示在设备上执行打印头清洗过程的命令。 此值为只写值。 尝试读取此值应被拒绝。 如果该值设置为1，则设备应执行命令。

 

 




