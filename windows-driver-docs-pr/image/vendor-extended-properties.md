---
title: 供应商扩展的属性
description: 供应商扩展的属性
ms.assetid: bcc89272-c14d-4d46-a2ca-7da0fb188111
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15937fdd0040d87217fc01ff00a73741951d5976
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356145"
---
# <a name="vendor-extended-properties"></a>供应商扩展的属性





一个**PropCode**中的条目**DeviceData** INF 文件部分 (请参阅中的示例[Vendor-Extended 功能](vendor-extended-features.md)) 列出了所有供应商扩展的属性代码，以分隔逗号。 对于每个属性的代码，窗体的一个条目 **PropCode * * * XXXX*必须存在，其中 XXXX 是大写十六进制代码值。 该条目应列出 WIA 属性代码和文本说明 （它不需要进行本地化） 用引号括起来。

WIA 属性代码应在 0x9802 和 0x11802，是为供应商定义 WIA 设备属性定义的范围之间。 可以通过访问的属性**IWiaPropertyStorage::GetPropertyStream**并**IWiaPropertyStorage::SetPropertyStream** Microsoft Windows SDK 中介绍的方法文档。

 

 




