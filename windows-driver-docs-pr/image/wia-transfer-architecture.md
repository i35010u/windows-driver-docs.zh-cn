---
title: WIA 传输体系结构
description: WIA 传输体系结构
ms.assetid: d8a11440-efdb-4590-9261-2b424c11186d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4f0b79d4cb13965bd10b63444ffae490ce48ef3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533074"
---
# <a name="wia-transfer-architecture"></a>WIA 传输体系结构


Stream 基于传输简化驱动程序和驱动程序开发人员的传输。 对于内存中和文件传输，调用方必须指定，要使用的传输类型和驱动程序必须先执行不同的操作，具体取决于哪个传输选择类型。 与基于流的传输，调用方不需要指定内存或文件传输;调用方指定仅使用，哪些流和驱动程序行为方式相同，此流是文件流或内存流。 使用流还提供了与轻松集成[WIA 图像处理筛选器](wia-image-processing-filter.md)。

像其他 WIA 应用程序编程接口 (Api) 和设备驱动程序接口 (DDIs) **IStream**基于组件对象模型 (COM)。 若要确保流传输与其他流兼容**IWiaTransfer**必须公开接口。

**IWiaTransfer**接口已启用传输，传输取消的错误和状态报告，集成过程中显示进度的方法和上传和下载的设备中的数据。 **IWiaTransfer**接口目前仅通过**IWiaItem2**接口。 有关详细信息**IWiaItem2**或**IWiaTransfer**接口和类的方法，请参阅 Microsoft Windows SDK 文档。

本部分包括：

[IStream 数据传输驱动程序更改](istream-data-transfer-driver-changes.md)

[IStream 传输驱动程序示例](istream-transfer-driver-example.md)

 

 




