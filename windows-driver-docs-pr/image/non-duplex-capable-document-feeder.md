---
title: 支持非双工的文档送纸器
description: 支持非双工的文档送纸器
ms.assetid: e22ec1bb-623e-45c6-88f4-d3b6a45fa175
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b19996c226a8fd2a5b8b08f40410ad9e9fce8a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379668"
---
# <a name="non-duplex-capable-document-feeder"></a>支持非双工的文档送纸器





下图说明了支持简单 （非双工） 文档送纸器扫描平板扫描仪 WIA 项树。

![说明支持非双工文档送纸器扫描平板扫描仪 wia 项树的关系图](images/wia-feeder-tree4.png)

送纸器 （或自动文档送纸器） 使用扫描程序不需要具有平板。 下图说明了不带平板或双面打印器送纸器扫描程序项树。

![说明而无需平板或双面打印器送纸器扫描程序项树的关系图](images/wia-feeder-tree2.png)

仅当没有平板扫描仪上存在时，可以省略平板项。 同样，送纸器项必须存在项树中的任何扫描程序已送纸器。 送纸器项用于控制设置，例如基本扫描 （不进行双面打印或单纯形）、 简单双工 （相同的前端和后的项） 和高级双工扫描 （独立于前端和后的项）。

### <a name="scanning"></a>扫描

应用程序导航到要执行文档送纸器扫描的送纸器项。 此项目中，应用程序配置页扫描和每个页的设置的数量。 请注意，扫描三个页面中的三个文档结果。

### <a name="image-acquisition"></a>图像采集

在标准的购买和文件夹获取，WIA 送纸器项目属性设置用于前端的所有页面。 有关标准采集和文件夹获取详细信息，请参阅[高级 ' 双工能力的文档送纸器](advanced-duplex-capable-document-feeder.md)。

 

 




