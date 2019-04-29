---
title: PTP 事件
description: PTP 事件
ms.assetid: 69bbe1e1-46e7-4615-93ff-ecd640e7d56b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d90dec6990c76709d3f447c22de13859ee799815
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379619"
---
# <a name="ptp-events"></a>PTP 事件





当添加或移除对象时，其中包括响应**StoreAdded**或**StoreRemoved**触发事件 （PIMA 15740 标准中所述），WIA 事件。 WIA\_事件\_项\_时添加一个对象，激发已创建事件和 WIA\_事件\_项\_中移除对象时激发已删除事件。 （请参阅有关说明这些和其他 WIA 事件标识符的 Microsoft Windows SDK 文档。）PTP 驱动程序使用的其他 PTP 事件来更新内部结构，但这些事件不会报告给应用程序。 请注意 PTP 驱动程序监视的事件，仅当应用程序必须打开设备时。

 

 




