---
title: 属性数据类型标识符
description: 属性数据类型标识符
ms.assetid: 8deb96d8-c18c-48f2-be5d-1a3fc8ba8508
keywords:
- 设备属性 WDK 设备安装，属性数据类型标识符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef4e2da61affe00817048d5a336821d27d2afec3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380473"
---
# <a name="property-data-type-identifiers"></a>属性数据类型标识符


属性数据类型标识符[ **DEVPROPTYPE**](https://docs.microsoft.com/previous-versions/ff543546(v=vs.85))-类型化值，该值表示属性的数据格式。 一般情况下，属性数据类型标识符为的按位 OR [**基本数据类型标识符**](https://docs.microsoft.com/previous-versions/ff537793(v=vs.85))和一个[**属性数据类型修饰符**](https://docs.microsoft.com/previous-versions/ff549770(v=vs.85)). 属性数据类型标识符可以表示单个固定长度数据的基本类型值、 单个的可变长度数据的基本类型值、 固定长度数据的基本类型值的数组或可变长度数据的基本类型值的列表。

中定义的受支持系统的基本数据类型标识符和属性数据类型修饰符*Devpropdef.h*。

Windows 将强制属性数据类型标识符的以下要求：

-   基本数据类型标识符是一个 DEVPROP_TYPE_*Xxx*标识符。

-   如果基本数据类型标识符[ **DEVPROP_TYPE_EMPTY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-empty)或[ **DEVPROP_TYPE_NULL**](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-type-null)，属性数据类型标识符不能包含属性数据类型修饰符。

-   属性数据类型修饰符的属性数据类型标识符包含属性数据类型修饰符时，如果是一个 DEVPROP_TYPEMOD_*Xxx*标识符。

-   [ **DEVPROP_TYPEMOD_ARRAY** ](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-typemod-array)属性数据类型修饰符可以仅使用固定长度的基本数据类型进行组合。

-   [ **DEVPROP_TYPEMOD_LIST** ](https://docs.microsoft.com/windows-hardware/drivers/install/devprop-typemod-list)属性数据类型修饰符可以仅使用长度可变的基本数据类型进行组合。

除了强制实施的属性数据类型标识符的要求，Windows 还加强[属性值要求](property-value-requirements.md)依赖属性数据类型。

SetupAPI 属性函数用于检索和设置属性值采用*PropertyType*参数。 检索属性值，函数*PropertyType*是接收属性的属性数据类型标识符的输出参数。 设置属性值，函数*PropertyType*是输入的参数提供的设备属性的属性数据类型标识符。

有关详细信息，请参阅[以访问设备的属性 （Windows Vista 和更高版本） 使用 SetupAPI](using-setupapi-to-access-device-properties--windows-vista-and-later-.md)。

 

 





