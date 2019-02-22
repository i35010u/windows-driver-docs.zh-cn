---
title: 范围模板的数据类型问题
description: 范围模板的数据类型问题
ms.assetid: 36cc91dc-5edc-4786-b3c9-f60bff06997d
keywords:
- 数据类型 WDK GDL，模板的数据类型的问题
- 范围的数据类型 WDK GDL
- ArraySize 指令 wDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8292723f8de35874b3fb72b374c79bd500221e21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544040"
---
# <a name="range-template-data-type-issues"></a>范围模板的数据类型问题


\*ArraySize 指令接受一个整数范围。 (一个范围是由连字符 （-） 分隔的 （可选） 括在圆括号和方括号的两个整数\[例如， \*ArraySize:\[1-15\]\]). 可以使用 GPD 通配符 (\*) 来表示任何整数值。 例如，若要定义任何大小的数组，可以使用\*ArraySize: \*。

 

 




