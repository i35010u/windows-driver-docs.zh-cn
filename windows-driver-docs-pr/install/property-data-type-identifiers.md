---
title: 属性数据类型标识符
description: 属性数据类型标识符
ms.assetid: 8deb96d8-c18c-48f2-be5d-1a3fc8ba8508
keywords:
- 设备属性 WDK 设备安装，属性数据类型标识符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 628f3f09144dfbf57754a60165c792c09f4de04d
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095673"
---
# <a name="property-data-type-identifiers"></a>属性数据类型标识符


属性数据类型标识符是 [**DEVPROPTYPE**](/previous-versions/ff543546(v=vs.85))类型的值，它表示属性的数据格式。 一般情况下，属性数据类型标识符是 [**基本数据类型标识符**](/previous-versions/ff537793(v=vs.85)) 和 [**属性数据类型修饰符**](/previous-versions/ff549770(v=vs.85))的按位 "或"。 属性数据类型标识符可以表示单个固定长度的基本数据类型值、单个可变长度的基本数据类型值、固定长度的基本数据类型值的数组或可变长度的基本数据类型值的列表的值。

*Devpropdef*中定义了系统支持的基本数据类型标识符和属性数据类型修饰符。

Windows 在属性数据类型标识符上强制实施以下要求：

-   基本数据类型标识符是 DEVPROP_TYPE_*Xxx* 标识符之一。

-   如果基本数据类型标识符 [**DEVPROP_TYPE_EMPTY**](./devprop-type-empty.md) 或 [**DEVPROP_TYPE_NULL**](./devprop-type-null.md)，则属性数据类型标识符不能包含属性数据类型修饰符。

-   如果属性数据类型标识符包含属性数据类型修饰符，则属性数据类型修饰符是 DEVPROP_TYPEMOD_*Xxx* 标识符之一。

-   [**DEVPROP_TYPEMOD_ARRAY**](./devprop-typemod-array.md)的属性数据类型修饰符只能与固定长度的基本数据类型组合。

-   [**DEVPROP_TYPEMOD_LIST**](./devprop-typemod-list.md)的属性数据类型修饰符只能与可变长度的基本数据类型组合。

除了对属性数据类型标识符强制要求外，Windows 还强制实施依赖于属性数据类型的 [属性值要求](property-value-requirements.md) 。

检索和设置属性值的 Setupapi.log 属性函数采用 *PropertyType* 参数。 对于检索属性值的函数， *PropertyType* 是一个输出参数，用于接收属性的属性数据类型标识符。 对于设置属性值的函数， *PropertyType* 是一个输入参数，它提供设备属性的属性数据类型标识符。

有关详细信息，请参阅 [使用 Setupapi.log 访问设备属性 (Windows Vista 和更高版本) ](using-setupapi-to-access-device-properties--windows-vista-and-later-.md)。

 

