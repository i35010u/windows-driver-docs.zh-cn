---
title: 送纸器扫描仪体系结构
description: 送纸器扫描仪体系结构
ms.assetid: 02157a88-fccd-4a23-a4ee-174755c8d3aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cab56f84b9053530b82c669ca4457615d4cb6bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323455"
---
# <a name="feeder-scanner-architecture"></a>送纸器扫描仪体系结构





如果任何映像生成放置在文档送纸器中的文档中，具有文档送纸器单位的扫描程序设备必须在其 WIA 项树中实现送纸器项。 送纸器项表示的可编程数据源，并生成放置在扫描程序的文档送纸器扫描单元，此项从请求数据传输时的文档中的映像。 扫描程序送纸器项应位于直接关闭 WIA 根项目，并可能包含一个或多个子项表示正面和背面的文档页。

下面的主题介绍支持文档送纸器扫描平板扫描仪的示例：

[非双工能力文档送纸器](non-duplex-capable-document-feeder.md)

[简单的双工能力文档送纸器](simple-duplex-capable-document-feeder.md)

[高级的双工能力文档送纸器](advanced-duplex-capable-document-feeder.md)

 

 




