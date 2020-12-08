---
title: 送纸器扫描仪体系结构
description: 送纸器扫描仪体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c973bbad60566dfcf8e2e3e879ce767b6416427a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822403"
---
# <a name="feeder-scanner-architecture"></a>送纸器扫描仪体系结构





如果要从放置在文档送纸器中的文档生成任何图像，则具有文档送纸器单位的扫描程序设备必须在其 WIA 项树中实现一个送纸器项。 "进纸器" 项表示一个可编程数据源，并从该项目请求数据传输时，从位于扫描仪文档送纸器扫描单元中的文档生成图像。 扫描仪进纸器项应直接位于 WIA 根项的位置，并且可以包含一个或多个子项来表示文档的正面和背面。

以下主题介绍了支持文档送纸器扫描的平板扫描仪的示例：

[支持非双工的文档送纸器](non-duplex-capable-document-feeder.md)

[支持简单双工的文档送纸器](simple-duplex-capable-document-feeder.md)

[支持高级双工的文档送纸器](advanced-duplex-capable-document-feeder.md)

 

 




