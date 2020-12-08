---
title: WIA 传输体系结构
description: WIA 传输体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5b9afb3e9c210aa0210a9dab86fbd61deda548f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826401"
---
# <a name="wia-transfer-architecture"></a>WIA 传输体系结构


基于流的传输简化了驱动程序和驱动程序开发人员的传输。 使用内存中和文件传输时，调用方必须指定要使用的传输类型，并且驱动程序必须根据选择的传输类型执行不同的操作。 对于基于流的传输，调用方不需要指定内存或文件传输;调用方仅指定要使用的流，驱动程序的行为方式与此流是文件流还是内存流相同。 使用流还可以轻松地与 [WIA 图像处理筛选器](wia-image-processing-filter.md)集成。

与其他 WIA 应用程序编程接口 (Api) 和设备驱动程序接口 (DDIs) ， **IStream** 基于组件对象模型 (COM) 。 若要确保流传输与其他流兼容，必须公开 **IWiaTransfer** 接口。

**IWiaTransfer** 接口具有一些方法，这些方法可在传输期间显示进度、取消传输、错误和状态报告集成以及从设备上传和下载数据。 **IWiaTransfer** 接口仅通过 **IWiaItem2** 接口提供。 有关 **IWiaItem2** 或 **IWiaTransfer** 接口及其方法的详细信息，请参阅 Microsoft Windows SDK 文档。

本节包括：

[IStream 数据传输驱动程序更改](istream-data-transfer-driver-changes.md)

[IStream 传输驱动程序示例](istream-transfer-driver-example.md)

 

 




