---
title: 将 PTP 对象映射到 WIA 项
description: 将 PTP 对象映射到 WIA 项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac39ea7e1d0248e0cad78fbc484e3bf9545bd1d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796191"
---
# <a name="mapping-ptp-objects-to-wia-items"></a>将 PTP 对象映射到 WIA 项





为设备上存在的每个 PTP 对象创建 WIA 项。 该驱动程序将显示与报告在同一层次结构中的对象。 例如，如果所有对象都是在名为 "XYZ" 的文件夹下报告的，则图片将显示在资源管理器中名为 "XYZ" 的文件夹下。

此规则的一个例外是，将其 FilesystemType 在 StorageInfo 数据集中作为 DCF 报告的设备。 在这种情况下，顶级文件夹称为 "DCIM" (如果它存在) ，下一级文件夹将被 Microsoft PTP 类 WIA 微型驱动程序隐藏。 子文件夹中的所有对象都提升为顶级。 文件扩展名 (例如，。在将 JPG) 发送到 WIA 之前，会将其从对象名称中去除。

 

 




