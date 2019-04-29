---
title: 送纸器扫描仪子项的要求
description: 送纸器扫描仪子项的要求
ms.assetid: 069ce228-ac73-42b5-9f1b-528ee6fe6a92
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27ded327c2d7402fccabea27fd99bc5a0a75ce5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356233"
---
# <a name="requirements-for-feeder-scanners-child-items"></a>送纸器扫描仪子项的要求


送纸器扫描程序项树 （即，前端和后端项目） 中的子项支持所需的大多数项属性和送纸器项 （即，前端和后端项目的父项） 支持的标志。

### <a name="item-flags"></a>项标志

子项目必须支持所有父项中，除支持的所需的项目标志**WiaItemTypeTransfer**。 **WiaItemTypeTransfer**标志可能会根据需要受支持; 但是，从自动文档送纸器的数据传输将完成从送纸器项而不是子项目。

### <a name="item-properties"></a>项属性

支持的大多数项属性的父送纸器项支持所需的送纸器扫描程序项树 （或前端和后端项目） 中的子项。 子项目必须支持[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)及其所有 WIA\_IP\_*Xxx*和 WIA\_IPA\_*Xxx*送纸器项支持相关扫描在当前文档端的配置参数的属性。 这些属性包括送纸器项上的必需和可选属性。 当扫描仪执行高级双工扫描时，使用的图像质量设置 （或扫描配置参数） 的子项目上设置和送纸器项中设置将被忽略。

**请注意**  子项目的属性项设置必须与匹配的父项属性的设置。 唯一的例外是[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)属性的子项; 此属性必须设置为 WIA\_类别\_送纸器\_正面或 WIA\_类别\_送纸器\_而不是回 WIA\_类别\_送纸器。

 

 

 




