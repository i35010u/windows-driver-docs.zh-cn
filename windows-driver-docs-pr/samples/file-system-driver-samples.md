---
title: 文件系统驱动程序示例
description: 此目录中的驱动程序示例编写你的设备的自定义文件系统驱动程序提供一个起始点。
ms.assetid: 9F2F995E-EA20-4877-B96C-5FF082CE886D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4d87404dc5060cccff8358170a664a500375abc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345224"
---
# <a name="file-system-driver-samples"></a>文件系统驱动程序示例


此目录中的驱动程序示例编写你的设备的自定义文件系统驱动程序提供一个起始点。

## <a name="file-systems"></a>文件系统


| 示例名称      | 解决方案                                                           | 描述                                                                                                                                                                                                                                                                            |
|------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CDFS             | [cdfs](https://go.microsoft.com/fwlink/p/?LinkId=617642)            | CD-ROM 文件系统驱动程序 (cdfs) 示例是可移动介质的文件系统驱动程序。                                                                                                                                                                                               |
| FastFAT          | [fastfat](https://go.microsoft.com/fwlink/p/?LinkId=620305)         | 基于 Windows 收件箱 FastFAT 文件系统用作模型的新文件系统文件系统驱动程序。                                                                                                                                                                              |
| AVScan           | [avscan](https://go.microsoft.com/fwlink/p/?LinkId=617644)          | 此筛选器的事务感知文件扫描程序会检查文件中的数据。 防病毒软件可能在这种方式中操作。                                                                                                                                                                 |
| CancelSafe       | [cancelSafe](https://go.microsoft.com/fwlink/p/?LinkId=617645)      | 演示如何使用取消安全队列微筛选器。                                                                                                                                                                                                                              |
| CDO              | [cdo](https://go.microsoft.com/fwlink/p/?LinkId=617646)             | 举例说明了微筛选器中使用控件设备对象 (CDO)。                                                                                                                                                                                                                   |
| “更改”           | [change](https://go.microsoft.com/fwlink/p/?LinkId=617647)          | 一个识别事务的筛选器，用于监视在真实时间中的文件更改。                                                                                                                                                                                                                    |
| Ctx              | [ctx](https://go.microsoft.com/fwlink/p/?LinkId=617648)             | 演示如何将上下文附加到实例、 文件、 流和流中您微筛选器的句柄。                                                                                                                                                                               |
| DELETE           | [delete](https://go.microsoft.com/fwlink/p/?LinkId=617649)          | 演示如何检测删除操作的文件或流。                                                                                                                                                                                                                              |
| Metadata Manager | [MetadataManager](https://go.microsoft.com/fwlink/p/?LinkId=617650) | 为了举例说明如何使用用于存储对应于你微筛选器的元数据文件提供服务。 此示例的实现描述了可能具有对该文件的修改才会被阻止，或暂时关闭该文件可能需要微筛选器的情形。 |
| Minispy          | [minispy](https://go.microsoft.com/fwlink/p/?LinkId=617651)         | 用于监视和记录系统中发生任何 I/O 和事务活动的工具。                                                                                                                                                                                                  |
| NameChanger      | [NameChanger](https://go.microsoft.com/fwlink/p/?LinkId=617652)     | Grafts 从卷的命名空间的一部分与另一个部件使用的映射的目录。 微筛选器通过充当注入到目录枚举的项的名称提供程序维护这种错觉，并转发目录更改通知                             |
| NullFilter       | [nullFilter](https://go.microsoft.com/fwlink/p/?LinkId=617653)      | 只是演示如何使用筛选器管理器注册了微筛选器。                                                                                                                                                                                                            |
| PassThrough      | [passThrough](https://go.microsoft.com/fwlink/p/?LinkId=617654)     | 演示如何指定不同类型的 I/O 请求的回调函数。                                                                                                                                                                                                    |
| 扫描仪          | [scanner](https://go.microsoft.com/fwlink/p/?LinkId=617655)         | 一个文件数据的扫描程序示例。 通常情况下，防病毒筛选器都属于此类型。                                                                                                                                                                                                           |
| SimRep           | [simrep](https://go.microsoft.com/fwlink/p/?LinkId=617656)          | 演示如何文件系统筛选器可以模拟文件系统类似重分析点行为，将打开的文件重定向到备用路径。                                                                                                                                               |
| SwapBuffer       | [swapBuffers](https://go.microsoft.com/fwlink/p/?LinkId=617657)     | 演示如何切换之间读取和写入数据的缓冲区。 此方法会特别有用的加密筛选器。                                                                                                                                                     |

 

 

 




