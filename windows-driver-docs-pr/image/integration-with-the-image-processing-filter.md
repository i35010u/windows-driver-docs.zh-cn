---
title: 与图像处理筛选器集成
description: 与图像处理筛选器集成
ms.assetid: ae5c6209-c95a-424c-9151-caeb8e6b3f8c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe43207a391e1d9793737e3b04ae861e76502d68
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563338"
---
# <a name="integration-with-the-image-processing-filter"></a>与图像处理筛选器集成


基于 Stream 的数据传输允许的简单集成[WIA 图像处理筛选器](wia-image-processing-filter.md)使用 WIA 驱动程序由于流提供的调用方和 WIA 驱动程序将需要相同的操作，无论目标流。 也就是说，该驱动程序只需询问对于流，然后编写，无论哪种类型的流返回到该驱动程序。

实现所需的 WIA 图像处理筛选器**IStream**。 创建此筛选器时，将为其给定应用程序的目标流，它应然后委托 （或转发） 对其调用。 换而言之，当**IStream::Write**称为筛选器，它应处理缓冲区，然后调用**IStream::Write**与已处理的缓冲区的目标流。

同样，图像处理筛选器可让流驱动程序，以便可以将数据写入从驱动程序图像处理筛选器，然后将写入到应用程序的目标流。 请注意，是否存在任何筛选器，不则该驱动程序不会更改但继续写入到流。

以下各图以图形方式显示这种情况。 第一个图说明了基于流的数据传输方法时不使用图像处理筛选器。

![说明不包含图像处理筛选器 istream 传输的关系图](images/streamtrans-no-filter.png)

使用图像处理筛选器时，第二个图说明了基于流的数据传输。

![使用图像处理筛选器说明 istream 传输的关系图](images/streamtrans-with-filter.png)

请注意，驱动程序的行为不会更改;该驱动程序接收的流，并向其中写入是否流直接提供的图像处理筛选器或应用程序。 因此，您可以将发布的增值图像处理组件分开。 例如，您可以提供的正常运行，但在用户安装图像处理组件从 CD 时，可以提供更好的高质量图像的现成驱动程序。 该驱动程序不需要在此情况下更改。

**IStream**接口和其方法 Microsoft Windows SDK 文档中所述。

 

 




