---
title: 筛选器驱动程序的加载顺序组和高度
description: 介绍筛选器驱动程序的加载顺序组和高度
ms.assetid: be8f18fe-c80b-44a3-b0c3-f2f630142180
keywords:
- 海拔 WDK 文件系统微筛选器
- 海拔 WDK 文件系统筛选器驱动程序
- 加载顺序组 WDK 文件系统
- 启动类型 WDK 文件系统
- 驱动程序启动类型 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e15a144f6089b78aef1f78e9497aa8dbbfb0263a
ms.sourcegitcommit: 9e13d3fbc74bb75335c4d2927c55b0085e46b0ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2020
ms.locfileid: "94639033"
---
# <a name="load-order-groups-and-altitudes-for-filter-drivers"></a>筛选器驱动程序的加载顺序组和高度

## <a name="about-load-order-groups-and-altitudes"></a>关于加载顺序组和高度

Windows 对文件系统筛选器驱动程序和在系统启动时加载的旧筛选器驱动程序使用一组专用的 *加载顺序组* 。

每个加载顺序组都有一组已定义的 *高度* 。 每个筛选器驱动程序都必须具有唯一的海拔标识符。 在加载筛选器时，筛选器的高度定义其相对于其他筛选器驱动程序的位置。 海拔高度是被解释为十进制数的无限精度字符串。 如果筛选器驱动程序的数字高度较低，则会将该筛选器驱动程序加载到值较高的筛选器驱动程序的下面。

海拔分配由 Microsoft 管理。 若要请求筛选器驱动程序的海拔高度，请参阅 [筛选器高度请求](minifilter-altitude-request.md)。

筛选器驱动程序的海拔值在 [筛选器驱动程序的 INF 文件中的 **字符串** 部分](creating-an-inf-file-for-a-minifilter-driver.md)的 **实例** 定义中指定。 还可以在 [**FLT_REGISTRATION**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)结构中对 [**InstanceSetupCallback**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)例程的调用中指定实例定义。 可以定义筛选器驱动程序的多个实例和高度。 这些实例定义适用于所有卷。

## <a name="table-of-load-order-groups-and-altitude-ranges"></a>加载顺序组和海拔范围的表

下表列出了筛选器驱动程序的系统定义的负载顺序组和海拔范围。 对于每个加载顺序组，"加载顺序组" 列包含应在 [筛选器 INF 文件的 **ServiceInstall** 部分](creating-an-inf-file-for-a-minifilter-driver.md)的 **LoadOrderGroup** 项中为该组指定的值。 海拔范围列包含特定加载顺序组的海拔范围。

请注意，"加载顺序组" 和 "高度" 范围将在堆栈上列出，这与它们的加载顺序相反。

加载顺序组 | 海拔范围 | 说明 |
| -------------- | -------------- | ----------- |
| “筛选器” | 420000-429999 | 此组与 Windows 2000 及更早版本上提供的筛选器加载顺序组相同。 此组最后加载，因此从文件系统中最远附加。 |
| FSFilter 顶部 | 400000-409999 | 此组适用于必须附加到所有其他 FSFilter 类型之上的筛选器驱动程序。 |
| FSFilter 活动监视器 | 360000-389999 | 此组包括观察和报告文件 i/o 的筛选器驱动程序。 |
| FSFilter 删除 | 340000-349999 | 此组包括用于恢复已删除文件的筛选器。 |
| FSFilter 防病毒 | 320000-329999 | 此组包括在文件 i/o 过程中检测和杀毒病毒的筛选器驱动程序。 |
| FSFilter 复制 | 300000-309999 | 此组包括将文件数据复制到远程服务器的筛选器驱动程序。 |
| FSFilter 连续备份 | 280000-289999 | 此组包括将文件数据复制到备份媒体的筛选器驱动程序。 |
| FSFilter 内容筛选程序 | 260000-269999 | 此组包括阻止创建特定文件或文件内容的筛选器驱动程序。 |
| FSFilter 配额管理 | 240000-249999 | 此组包括提供增强的文件系统配额的筛选器驱动程序。 |
| FSFilter 系统恢复 | 220000-229999 | 此组包括执行操作以维护操作系统完整性的筛选器驱动程序，如系统还原 (SR) filter。 |
| FSFilter 群集文件系统 | 200000-209999 | 此组包括在提供跨网络的文件服务器元数据的产品中使用的筛选器驱动程序。 |
| FSFilter HSM | 180000-189999 | 此组包括执行分层存储管理的筛选器驱动程序。 |
| FSFilter 图像 | 170000-175000 | 此组包含可提供虚拟命名空间的类似于 ZIP 的筛选器驱动程序。 |
| FSFilter 压缩 | 160000-169999 | 此组包括执行文件数据压缩的筛选器驱动程序。 |
| FSFilter 加密 | 140000-149999 | 此组包括在文件 i/o 过程中对数据进行加密和解密的筛选器驱动程序。 |
| FSFilter 虚拟化 | 130000-139999 | 此组包括用于虚拟化文件路径的筛选器驱动程序，如 Windows Vista 中添加的 (LUA) 筛选器驱动程序的最低授权用户。 |
| FSFilter 物理配额管理 | 120000-129999 | 此组包括使用物理块计数来管理配额的筛选器驱动程序。 |
| FSFilter 打开文件 | 100000-109999 | 此组包括提供已打开文件的快照的筛选器驱动程序。 |
| FSFilter Security 不得不一直 | 80000-89999 | 此组包括筛选器驱动程序，用于将锁定和增强的访问控制列表 (Acl) 。 |
| FSFilter 复制保护 | 60000-69999 | 此组包括用于检查介质上的带外数据的筛选器驱动程序。 |
| FSFilter 底部 | 40000-49999 | 此组是为必须附加到所有其他 FSFilter 类型的筛选器驱动程序而提供的。 |
| FSFilter 系统 | 20000-29999 | 保留以供内部使用。 |
| FSFilter 基础结构 | 保留以供内部使用。 此组首先加载，因此附加最接近文件系统。 |
