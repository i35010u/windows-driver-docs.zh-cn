---
title: 管理对象的生存期
description: 管理对象的生存期
ms.assetid: 55ad8133-a70a-462f-87cd-6aeaffb0aec8
keywords:
- UMDF 对象 WDK、 生存期
- framework 对象 WDK UMDF、 生存期
- 生存期 WDK UMDF
- 回调对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93901287175746f3104d6cc1b57beccc62fd7400
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371727"
---
# <a name="managing-the-lifetime-of-objects"></a>管理对象的生存期


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF 使用引用计数方案来管理生存期[回调对象](creating-callback-objects.md)并[framework 对象](framework-objects.md)。

## <a name="managing-references-to-driver-supplied-callback-objects"></a>管理对驱动程序提供的回调对象的引用


在大多数情况下，驱动程序不需要保留对回调对象的引用。 如果仅由框架和对象的生存期取决于回调对象和回调对象的配对的 framework 对象通过调用回调对象接口的方法，该驱动程序不必保留的引用。 换而言之，驱动程序或框架可以安全地调用方法的对象的对象层次结构中较高的接口。

## <a name="managing-references-to-framework-objects"></a>管理对 Framework 对象的引用


在 UMDF，一般的 COM 生存期原则和特定于 WDF 的生命周期模型确定 framework 对象的生存期。 您的驱动程序必须满足这两种模型的条件，以便在适当时候从内存释放 framework 对象。

### <a name="com-lifetime-management"></a>COM 生存期管理

在 COM 中，调用方通常保留对对象的引用对象正在使用，而不再需要对象时，调用方然后释放的引用。 但是，UMDF 驱动程序不需要保持对 framework 对象的引用。 事实上，该驱动程序可以驱动程序创建的 framework 对象后立即释放 framework 对象引用。

例如，UMDF 示例发布的设备对象后调用[ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)。 尽管早期释放的引用，但设备对象将继续存在设备删除因为 WDF 对象树中保存对它的引用之前。

因为 UMDF 跟踪的对象树中的所有框架对象，该驱动程序不必保留对 framework 对象的引用。

但是，如果您的驱动程序对 framework 对象的引用，该驱动程序必须释放该引用，当它不再需要对象时一样。 循环引用保留在原位，直到该驱动程序释放它的引用。 若要避免循环引用，该驱动程序通常应不保留对 framework 对象的显式引用。

如果该驱动程序必须保持对 framework 对象的引用，该驱动程序的回调对象还必须实现[IObjectCleanup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iobjectcleanup)接口。 当驱动程序调用[ **IWDFObject::DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject) framework 对象上的 framework 对象调用其相应的回调对象[ **IObjectCleanup::OnCleanup** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iobjectcleanup-oncleanup)方法。 实现**IObjectCleanup::OnCleanup**必须释放对 framework 对象，若要启用完成拆解的 framework 取 framework 对象的引用。

### <a name="wdf-lifetime-management"></a>WDF 生存期管理

如果要创建允许你重写默认父类型的对象，则应选择匹配对象的生存期的生存期的父。 有关默认父对象和驱动程序可以重写默认父级的详细信息，请参阅中的表[Framework 对象](framework-objects.md)。

如果匹配对象生存期，框架会删除父对象时删除您的对象。 如果不匹配对象生存期，并且你想要删除的默认父之前先删除的对象，你可以显式删除该对象通过调用[ **DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)对象时没有不再需要。

例如，如果创建一个新的请求对象，然后调用[ **IWDFDriver::CreateWdfMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createwdfmemory)若要创建此请求的内存对象，可以指定请求对象作为父级的新内存对象。 由于 WDF 删除父对象时删除子对象，该驱动程序不需要调用[ **DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)删除内存对象。

但是，如果没有父其生存期符合对象的生存期，并且如果你想要删除的默认父之前先删除的对象，则必须使用显式删除。 例如，驱动程序可以创建多个用于在短时间内的请求对象。 在这种情况下，该驱动程序可以通过显式删除请求，在不再需要时节省内存。

同样，如果要创建一个对象，不允许你重写默认父并且你想要删除的默认父之前先删除的对象，该驱动程序必须显式删除该对象。

 

 





