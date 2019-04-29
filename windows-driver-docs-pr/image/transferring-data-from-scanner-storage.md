---
title: 从扫描仪存储传输数据
description: 从扫描仪存储传输数据
ms.assetid: 6fc9c825-509c-4c18-a859-e1f5504879b8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6ce69d59e36bd43e2c8d0d4d9d777332266e439
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383712"
---
# <a name="transferring-data-from-scanner-storage"></a>从扫描仪存储传输数据


若要从扫描程序存储项传输数据，WIA 应用程序应枚举存储文件夹和所包含的根存储项和作为传输源使用每个单独的文件项 （若要将所包含的数据传输的文件项特定的项）。

有关**WiaItemTypeImage**文件项，该应用程序可能会读取现有 WIA\_IPS\_*Xxx*或 WIA\_IPA\_*Xxx*（或两者） 描述图像格式 （如果支持） 的属性。 应用程序还可能会使用此信息来选择要从扫描程序存储下载图像。

将数据传输到扫描程序存储文件夹项之一，WIA 应用程序应枚举可用的存储文件夹项、 选择的文件夹或创建新的文件夹选项，和将数据上传到它。

**请注意**  外的根存储文件夹应不允许此枚举操作。

 

 

 




