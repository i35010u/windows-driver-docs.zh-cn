---
title: 图像几何属性
description: 图像几何属性
ms.assetid: d1343ad4-3a54-414c-bc08-e07e0fb079cd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bafa66387e115d1c75bd05b8227aa8133edcf32a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352147"
---
# <a name="image-geometry-properties"></a>图像几何属性





（请参阅 PIMA 15740 标准） 的 ImgPixHeight 和 ImgPixWidth 映像 geometry 属性是 PTP 中可选的。 对于未实现这些属性的照相机，Microsoft PTP 微型驱动程序下载整个图像，并计算这些属性的正确值。 您可以防止此情况发生通过实现这些可选 PTP 属性。

 

 




