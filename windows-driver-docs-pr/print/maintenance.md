---
title: 维护
description: 维护
ms.assetid: 228759ed-f6de-4680-adf2-ca88b83ff4a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82e2c387c5d20d4233ae63f13b192180d85d15b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390922"
---
# <a name="maintenance"></a>维护


架构路径：\\Printer.Maintenance

节点类型： 属性

维护属性包含有关维护的打印设备的信息。

维护属性包含两个对子值：**AlignHead**并**CleanHead**。

### <a name="span-idalignheadspanspan-idalignheadspan-alignhead"></a><span id="alignhead"></span><span id="ALIGNHEAD"></span> AlignHead

架构路径：\\Printer.Maintenance.AlignHead

节点类型：ReplTest1

数据类型：BIDI\_BOOL

说明：此值表示要在设备上执行打印头校准过程的命令。 此值是只写值。 尝试读取此值应被拒绝。 如果值设置为 1，则设备应执行该命令。

### <a name="span-idcleanheadspanspan-idcleanheadspan-cleanhead"></a><span id="cleanhead"></span><span id="CLEANHEAD"></span> CleanHead

架构路径：\\Printer.Maintenance.CleanHead

节点类型：值

数据类型：BIDI\_BOOL

说明：此值表示一个命令来执行打印头清洗在设备上的过程。 此值是只写值。 尝试读取此值应被拒绝。 如果值设置为 1，则设备应执行该命令。

 

 




