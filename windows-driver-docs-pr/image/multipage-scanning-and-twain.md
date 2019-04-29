---
title: 多页扫描和 TWAIN
description: 多页扫描和 TWAIN
ms.assetid: 02b5ef48-413d-403b-8c42-caecd9521067
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 921006eaed7cc236ddfc30f4fee701745478c260
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379671"
---
# <a name="multipage-scanning-and-twain"></a>多页扫描和 TWAIN





从 Windows XP，TWAIN 兼容性层支持多页扫描从滚动馈送的设备，前提是所有扫描的页是长度相同。 这样做的原因是该 TWAIN 获取从调用应用程序仅在第一页上的页面长度有关的信息。 TWAIN 不需要调用应用程序寻求页之间的图像信息。 此外，TWAIN 应用到所有后续页面收到从应用程序的第一页有关的信息。

 

 




