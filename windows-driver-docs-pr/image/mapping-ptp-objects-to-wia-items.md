---
title: 将 PTP 对象映射到 WIA 项
description: 将 PTP 对象映射到 WIA 项
ms.assetid: 3ee88c09-7f36-403a-ae7b-41d08c11c52f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96901a278a42459a96629486aec6f8dd0b0ab8bc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380381"
---
# <a name="mapping-ptp-objects-to-wia-items"></a>将 PTP 对象映射到 WIA 项





为每个设备上存在的 PTP 对象创建 WIA 项。 因为中未报告，该驱动程序相同的层次结构中显示的对象。 例如，如果在名为"XYZ"的文件夹下报告中的所有对象，图片将显示在资源管理器在名为"XYZ"的文件夹下。

此规则的例外是报告其 FilesystemType 为 DCF StorageInfo 数据集内的设备。 在这种情况下，最高级别文件夹名为"DCIM"（如果存在），和下一级别的向下的文件夹隐藏的 Microsoft PTP 类 WIA 微型驱动程序。 所有子文件夹中的对象被提升到最高级别。 文件扩展名 （例如，。JPG) 会在发送到 WIA 前被剥离从对象名称。

 

 




