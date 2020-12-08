---
title: 与图像处理筛选器集成
description: 与图像处理筛选器集成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009528ebb584b52341c91d06d6721f4a695e8f55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783913"
---
# <a name="integration-with-the-image-processing-filter"></a>与图像处理筛选器集成


基于流的数据传输使 [Wia 图像处理筛选器](wia-image-processing-filter.md) 可以轻松地与 wia 驱动程序集成，因为流由调用方提供，WIA 驱动程序无论目标流是什么，都将执行相同的操作。 也就是说，无论向驱动程序返回哪种类型的流，驱动程序都只要求提供流，然后向其写入。

要实现 **IStream**，需要 WIA 图像处理筛选器。 创建此筛选器后，将为其提供应用程序的目标流，然后它将 (或转发) 其对的调用。 换而言之，当对筛选器调用 **IStream：： write** 时，它应处理缓冲区，然后在目标流上调用具有已处理缓冲区的 **Istream：： write** 。

同样，图像处理筛选器可以向驱动程序传递流，以便可以将数据从驱动程序写入到图像处理筛选器，然后将数据写入到应用程序的目标流中。 请注意，如果不存在任何筛选器，则驱动程序将不会更改，但会继续写入到流中。

在下图中以图形方式显示了这种情况。 第一个图说明了在未使用图像处理筛选器时，基于流的数据传输。

![说明不使用图像处理筛选器的 istream 传输的关系图](images/streamtrans-no-filter.png)

第二个图演示了使用图像处理筛选器时的基于流的数据传输。

![说明使用图像处理筛选器的 istream 传输的关系图](images/streamtrans-with-filter.png)

请注意，驱动程序的行为不会更改;驱动程序接收流并向其写入流，无论流是由图像处理筛选器还是由应用程序提供。 因此，你可以单独发布值-添加图像处理组件。 例如，你可以提供内置的驱动程序，但当用户从 CD 安装图像处理组件时，可以提供更好的图像质量。 在这种情况下，不需要更改该驱动程序。

Microsoft Windows SDK 文档中介绍了 **IStream** 接口及其方法。

 

 




