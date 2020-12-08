---
title: 各种外形规格的实现需求
description: 本主题介绍各种外形规格的实现要求。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 742a141c0a61c13dafb44d2f0c77238efee62eba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824165"
---
# <a name="implementation-requirements-for-various-form-factors"></a>各种外形规格的实现需求

本主题介绍各种外形规格的实现要求。

|外形规格|外形规格名称|定义|GPIO 指标实现要求|
|----|----|----|----|
|![石板外形规格](images/slate.jpg)|平板|无附加键盘的 Tablet 外形规格|如果有固定的插接附件，则必须实现坞指示器。|
|![便携式计算机外形规格](images/laptop.jpg)|便携式计算机|永久连接的键盘，始终可以键入。|以静态方式将模式设置为便携式计算机。|
|![可转换外形规格](images/convertible.jpg)|敞篷车|可用作平板或平板电脑的系统。 可以分离、翻转或 swivelled 键盘。|实现笔记本电脑/石板指示器。</br>如果有固定的插接附件，则还必须实现坞指示器。|
|![一体型外形规格](images/allinone.jpg)|一体|中型台式机/半便携系统，具有作为附件连接的键盘。|不需要实现，因为键盘是可选的附件。|
